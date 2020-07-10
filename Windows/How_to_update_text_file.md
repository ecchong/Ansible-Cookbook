### How to update text file

1. Need to add account ansible_acct_name to SYS_ADMIN group in sudo file if it is not already there.  
```yaml
  - name: Add svc_ansible to sudo file
    lineinfile:
      path: /etc/sudoers
      state: present
      backrefs: yes
      regex: '(^User_Alias\s+SYS_ADMIN\s+)=(((?!{{ ansible_acct_name }}).)*)$'
      line: '\1=\2, {{ ansible_acct_name }}'
      validate: /usr/sbin/visudo -cf %s
```