### Wait until a lock file is removed by other process
```yaml
  - name: Wait until lock file is
    stat:
      path: "{{ lck_path }}"
    register: lck_file
    until: lck_file.stat.exists == False
    retries: 10
    delay: 5
    when: inventory_hostname != esxi_host.name
    delegate_to: "{{ esxi_host.name }}"
```