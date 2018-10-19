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

### No space in any search string.