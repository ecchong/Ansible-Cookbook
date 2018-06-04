### How to replace a substring in variable with regex

For example, we nee to reconstruct the path to the .vmx file of a VM.  The information is pull from vmware_guest_facts task into a list called hw_files.

The list of strings look like this
```yaml
"hw_files": [
                "[1node_vsan] bdf3125b-a135-fd6b-c56c-f44d3068826f/2-tet.vmx",
                "[1node_vsan] bdf3125b-a135-fd6b-c56c-f44d3068826f/2-tet.nvram",
                "[1node_vsan] bdf3125b-a135-fd6b-c56c-f44d3068826f/2-tet.vmsd",
                "[1node_vsan] bdf3125b-a135-fd6b-c56c-f44d3068826f/2-tet.vmdk"
            ]
```
We need to reconstruct the string into an actual file path that can be used in following tasks.

```yaml
  - name: Set vmx file path
    set_fact:
      vmx_path: "{{ item | regex_replace ('\\[(.*)\\]\\s*(.*\\.vmx)', '/vmfs/volumes/\\1/\\2') }}"
      lck_path: "{{ item | regex_replace ('\\[(.*)\\]\\s*(.*)\\.vmx', '/vmfs/volumes/\\1/\\2.lck') }}"
    when: item is match(".*\.vmx$") and inventory_hostname != esxi_host.name
    with_items: "{{ hw_files }}"
```