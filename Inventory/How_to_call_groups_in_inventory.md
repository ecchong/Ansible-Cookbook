#
### To see all hosts in the inventory
```yaml
ansible all -i inventory --list-hosts
ansible '*' -i inventory --list-hosts
```
### To see all hosts by wild cards
```yaml
ansible '*.example.com' -i inventory --list-hosts
ansible '192.168.1.*' -i inventory --list-hosts
```
### To see hosts in groups 'lab' or 'datacenter1'
```yaml
ansible lab:datacenter1 -i inventory --list-hosts
```
### To see hosts in groups 'lab' and 'datacenter1'
```yaml
ansible 'lab:&datacenter1' -i inventory --list-hosts
```
need single quote because of special character '&'
### To see all hosts in group 'datacenter' except test2.example.com
```yaml
ansible 'datacenter:!test2.example.com' -i inventory --list-hosts
```
