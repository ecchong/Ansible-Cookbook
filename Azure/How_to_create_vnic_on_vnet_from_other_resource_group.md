### How to create a virtual NIC on vnet from a different resource group.

Specify the full path of the vnet
https://github.com/ansible/ansible/issues/29607

```yaml
  - name: Create virtual NIC 
    azure_rm_networkinterface:
      resource_group: "{{ rg_name }}"
      virtual_network: "/subscriptions/{{ subscription_id }}/resourceGroups/{{ vnet_rg_name }}/providers/Microsoft.Network/virtualNetworks/{{ vnet_name }}"
      subnet: "{{subnet_name}}"
      name: "{{vnic_name}}"
```
