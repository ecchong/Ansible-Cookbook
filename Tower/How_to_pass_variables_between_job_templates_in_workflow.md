## How to pass variables between job templates in a workflow template

Use the **set_stats** module to store variables in one job template and then retrive them as variables in following job templates.

```yaml
  - name: Set stats
    set_stats:
      data:
        myvar: first template status
```

Check Ansible doc for other options of **set_stats**