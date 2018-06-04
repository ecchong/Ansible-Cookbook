## How to set fact on another host?

Use delegate_to and delegate_fact together

```yaml
- name: Store some fact on host B
  set_fact:
    server_description: This is host B
  delegate_to: host_B
  delegate_facts: true
```
Otherwise, fact will not be associate with delegate_to host.
