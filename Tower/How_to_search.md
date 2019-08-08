## Some examples to use the search box in Tower to filter or create smart inventory

see https://docs.ansible.com/ansible-tower/latest/html/towerapi/filtering.html
### Find disabled hosts
```bash
enabled:false
```

### Find hosts with hostvar defined
```bash
variables.icontains:myvar
```

### Use as host filter on tower-cli
```bash
tower-cli host list --host-filter 'variables__icontains=application'
```

### Find hosts with ansible facts equal a value
```bash
ansible_facts.ansible_os_family:RedHat
```

### Find hosts in organization
```bash
organization.name:Default
```

### Find hosts in a group belongs to an inventory
First we need to find the group number using the api URL.
For example, to list groups info for inventory id 18
https://tower-host.com/api/v2/inventories/18/groups/
Then use the group id in the filter
```bash
groups:482
```

### Find hosts in a group name from any inventory
```bash
groups.name:mygroup
```

### Find hosts that failed the last job
```bash
has_active_failures:true
```
### Find hosts by name
```bash
name.startswith:dev
name.exact:devhost4
name.istartwith:dev
name.endswith:4
name.regex:^dev.*4$
```

### Using the host filter on tower-cli
```bash
tower-cli host list --host-filter name__endswith=80 -vvv
tower-cli host list --host-filter name__startswith=RN
tower-cli host list --host-filter 'name__regex=fedora[0-9]'
tower-cli host list --host-filter 'name__startswith=RN and name__regex=01$'
```

### Find dev hosts that are marked as 'd' on the 6th characters
```bash
name.regex:^.{5}d
```


### No space in any search string.
