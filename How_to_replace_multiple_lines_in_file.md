### Replacing multiple lines in file
```yaml
- name: Set some kernel parameters
  lineinfile:
    dest: /etc/sysctl.conf
    regexp: "{{ item.regexp }}"
    line: "{{ item.line }}"
  with_items:
    - { regexp: '^kernel.shmall', line: 'kernel.shmall = 2097152' }
    - { regexp: '^kernel.shmmax', line: 'kernel.shmmax = 134217728' }
    - { regexp: '^fs.file-max', line: 'fs.file-max = 65536' }
```

### Replacing a block of text
```yaml
    blockinfile:
      path: inventory.test
      block: |
         [isolated_group_{{ group_name }}]
         {{ host_name }}
         [isolated_group_{{ group_name }}:vars]
         controller=tower
      state: present
```