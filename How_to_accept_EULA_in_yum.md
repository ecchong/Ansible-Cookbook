### How to accept EULA when yum installing something?

```
- name: Install mssql-tools and msodbcsql
  yum:
    name: "{{ item }}"
    state: present
  with_items:
    - mssql-tools
    - msodbcsql
  environment:
    ACCEPT_EULA: 'y'
  become: true
  become_user: root
```
