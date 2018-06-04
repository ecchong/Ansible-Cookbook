## How to run task only on first node in group

Check the group array

For example
```yaml
- name: Ping first node listed in group "tower"
  ping:
  when: inventory_hostname == groups['tower'][0]
```
