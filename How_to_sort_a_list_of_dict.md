### How to sort a list of dict objects

Example data from list of datastores from vCenter:
```shell
        "datastores": [
            {
                "accessible": true,
                "capacity": 444797550592,
                "datastore_cluster": "N/A",
                "freeSpace": 426470539264,
                "maintenanceMode": "normal",
                "multipleHostAccess": false,
                "name": "hqdev-esx1_local",
                "provisioned": 18327011328,
                "type": "VMFS",
                "uncommitted": 0,
                "url": "ds:///vmfs/volumes/524aa72f-de223a5e-b4f1-78e3b50b2d88/"
            },
            {
                "accessible": true,
                "capacity": 733634101248,
                "datastore_cluster": "N/A",
                "freeSpace": 731786510336,
                "maintenanceMode": "normal",
                "multipleHostAccess": false,
                "name": "hqdev-esx2_local",
                "provisioned": 1847590912,
                "type": "VMFS",
                "uncommitted": 0,
                "url": "ds:///vmfs/volumes/530f0ac5-1366daac-9611-ac162db1d8c0/"
            },
            {
                "accessible": true,
                "capacity": 2198754820096,
                "datastore_cluster": "3PAR7200TempMigrationAreaNL",
                "freeSpace": 1371663237120,
                "maintenanceMode": "normal",
                "multipleHostAccess": true,
                "name": "vmfs-3par7200-tempdev-ds1",
                "provisioned": 1561292056309,
                "type": "VMFS",
                "uncommitted": 734200473333,
                "url": "ds:///vmfs/volumes/5a6b821b-647c8196-cfaa-78e3b50b2d88/"
            },
        ]
```
We want to sort the list of datastores by the available freeSpace
```yaml
  - name: Print the list of datastores sorted by freeSpace
    debug:
      msg: "{{ datastore_facts.datastores | sort(attribute='freeSpace') }}"
```
How about just the one with most freeSpace?  Reverse the sort and first item is the one with most freeSpace.
```yaml
  - name: Print the list of datastores sorted by freeSpace
    debug:
      msg: "{{ datastore_facts.datastores | sort(attribute='freeSpace', reverse=true) | list | first }}"
```
