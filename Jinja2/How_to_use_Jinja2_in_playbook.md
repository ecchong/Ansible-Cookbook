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