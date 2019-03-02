## How to expand a variables using Jinja2 template

Problem:
We want to generate a list of VMs and past it to our VM creation role that will take a list as input.  Each VM in the list could be a little different, for example, different disk size or definitely different IP address.  A loop or with_item won't be able to do that. Jinja2 template can do that, but we don't want to generate a vars file before executing the VM creation role.

We will use lookup template plugin to generate a var from our Jinja2 template during runtime.

```yaml
  vars_files:
    - common_vars_for_all_vms.yml

  vars:
    run_vars: "{{ lookup('template','custom_vms.j2') | from_yaml }}"
```

- Store all variables that are common in a separated vars file and import it before Jinja2 file is parsed.
- Lookup returns a string and need to specfied as a yaml format.  Also need to verify the template is generating valid yaml format
- Assign it to a variable and now it becomes a dict that we can use

```yaml
  - name: Create all availability sets
    include_role:
      name: av_set
    vars:
      av_set: "{{ run_vars.av_set }}"

  - name: Create all VMs
    include_role:
      name: vm
    vars:
      vm: "{{ run_vars.vm }}"
```

This is what in the custom_vms.j2
```jinja2
av_set:
{% for func in func_list %}
{% if func.use_av %}
- name: "{{ prefix }}{{ env }}-{{ func.name }}"
  resource_group: "{{ prefix }}{{ env }}-{{ func.name }}"
  location: "{{ location }}"
  fault_domain_count: 3
  update_domain_count: 2
  tags: "{{ tags }}"
{% endif %}
{% endfor %}

vm:
{% set x = [] %}
{% for func in func_list %}
{% for i in range(func.count) %}
- name: "{{ prefix }}{{ env }}{{ func.name }}{{ i+1 }}"
  resource_group: "{{ prefix }}{{ env }}-{{ func.name }}"
{% if func.use_av %}
  av_set: "{{ prefix }}{{ env }}-{{ func.name }}"
{% endif %}
  size: "{{ size }}"
  location: "{{ location }}"
  admin_username: "{{ admin_username }}"
  admin_password: "{{ admin_password }}"
  ip_address: {{ starting_ip | ipmath( x | length - 1 ) }}
{% if x.append('1') %}{% endif %}
  managed_disk_type: "{{ managed_disk_type }}"
  os_style: Windows
  image: "{{ windows_image }}"
  tags: "{{ tags }}"
{% endfor %}
{% endfor %}
```

This is what in the common_vars_for_all_vms.yml
```yaml
subscription_id: put_you_own_here
prefix: dev
env: et

size: Standard_DS2v3
location: eastus2
admin_username: administrator
admin_password: some_vaulted_secret
windows_image:
  offer: WindowsServer
  publisher: MicrosoftWindowsServer
  version: latest
  sku: '2012-R2-Datacenter'
tags:
  project: "development"
managed_disk_type: Standard_LRS
virtualnetwork:
  resourcegroup: "{{ prefix }}{{ env }}-gateway"
  name: "{{ prefix }}{{ env }}-vnet"
  prefix: "10.0.0.0/24"
  subnet:
    name: "{{ prefix }}{{ env }}-subnet"
    prefix: "10.0.0.0/24"
starting_ip: 10.0.0.100
func_list:
- name: db
  count: 2
  use_av: true
- name: ap
  count: 2
  use_av: true
- name: fs
  count: 1
  use_av: false
```