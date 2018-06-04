# How to create a host in Tower via REST API call?

First we need to get the inventory id.

```shell
curl -k -X GET -u admin:ar2iis! https://dvnv-rhans01.dev.iisl.com/api/v2/inventories/
```
To create a host under inventory ID 15.

```shell
curl -X POST \
  https://<Tower hostname>/api/v2/hosts/ \
  -H 'authorization: Basic XXXXXXXXXXXXXXXX’ \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -d '{
    "name": "test_host",
    "description": "from REST API",
    "enabled": true,
    "inventory": "15",
    "variables": ""
}'
```




