# How to set persistent fact in Tower?

The playbook set_fact task must set "cacheable: true"
```yaml
  - name: set cached fact
    set_fact:
      my_var1: 'this is a fact'
      my_var2: 'it is cacheable'
      cacheable: true
```
In Tower, check option "Use Fact Cache" for the job template.  The facts will be store with the host.

To retrieve the stored facts, recall the hostvars.
```yaml
  - name: Get cached fact
    debug:
      msg: "The cached fact are:  {{ hostvars[inventory_hostname].my_var1 }} {{ hostvars[inventory_hostname]['my_var2'] }}"
```