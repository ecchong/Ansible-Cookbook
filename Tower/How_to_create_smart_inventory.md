### Smart inventory filter examples

#### Hosts with a cached fact "some_fact" with value "some_value"
```shell
ansible_facts.some_fact:"some_value"
```

```shell
ansible_facts.facter_os.name:"RedHat"
ansible_facts.facter_os.release.full:"7.6"
ansible_facts.facter_os.release.major:"7"
ansible_facts.facter_dmi.product.name:"VMware Virtual Platform"
```
