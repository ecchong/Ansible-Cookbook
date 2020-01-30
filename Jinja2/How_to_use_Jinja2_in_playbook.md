### How to use Jinja2 inside a playbook

1. To create variables
```yaml
- set_fact:
    foo: |
      {% set aks_modified = dict() %}
      {% for ak in activation_keys %}
      {{ aks_modified.update({ak:[]}) }}
      {% endfor %}
      {{ aks_modified | to_json }}
```

2. To loop in range
```yaml
  - debug:
      msg: |
       {%- for i in range(0,10) -%}
          {{ i }}
       {%- endfor -%}
```

3. To dynamically assign variables
```yaml
  vars:
    foo: 'hello'
    bar: 'byebye'
    x: "{{ 'foo' if ansible_distribution_major_version == '7' else 'bar' }}"
```
