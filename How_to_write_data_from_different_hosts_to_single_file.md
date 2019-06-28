### How to write data from multiple hosts to a single file

We need to gather information from multiple hosts and store them to a single file.  Possibly email it to someone as an attachment.

We can use lineinfile or blockinfile module with delegate_to localhost to write the information to a single file.  However, both modules do not handle concurrent write probably.  The file will be overwritten by the same task of different host.

**Solution 1:  Use Serial**
```yaml
---
- hosts: all
  gather_facts: no
  serial: 1

  tasks:
  - shell: hostname
    register: hostname_output

  - shell: lslogin
    register: lslogin_output

  - name: Write to single file
    blockinfile:
      path: "/tmp/ansible_temp_one_big_file.txt"
      create: true
      marker: "# {mark} ANSIBLE MANAGED BLOCK  {{ hostname_output.stdout }}"
      block: |
        {{ hostname_output.stdout }}
        {{ lslogin_output.stdout }}
    delegate_to: localhost
    run_once: true
```
This will execcute the blockinfile task one at a time.  However, it might not be possible if other tasks need to be run concurrently.

**Solution 2: Use facts and loop**
```yaml
---
- hosts: all
  gather_facts: no

  tasks:
  - shell: hostname
    register: hostname_output

  - name: Store hostname
    set_fact:
      my_hostname: "{{ hostname_output.stdout }}"

  - shell: " ps -ef "
    register: lslogin_output

  - name: Store lslogin
    set_fact:
      my_lslogin: "{{ lslogin_output.stdout }}"

  - name: Write to single file
    blockinfile:
      path: "/tmp/ansible_temp_one_big_file.txt"
      create: true
      marker: "# {mark} ANSIBLE MANAGED BLOCK  {{ hostvars[host].my_hostname }}"
      block: |
        {{ hostvars[host].my_hostname }}
        {{ hostvars[host].my_lslogin }}
    loop: "{{ ansible_play_hosts_all }}"
    loop_control:
      loop_var: host
    delegate_to: localhost
    run_once: true
```
The information will be stored as facts.  The blockinfile task will loop thru the list of play hosts and execute one a time.