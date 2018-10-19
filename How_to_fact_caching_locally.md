### How to cache facts locally when not using Tower

Default running ansible from command line only cache facts in memory. 
To store them locally in a file, change the following in local or global 
ansible.cfg

```ini
#fact_caching = memory
# Cache facts to local file 
fact_caching = yaml
fact_caching_connection = "/some_dir/ansible_cached_facts"
```
