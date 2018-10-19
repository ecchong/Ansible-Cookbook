### How to use Azure REST API.

Use azure_rm_resource module.  Install the Azure REST for Ansible extension for VSCode to help create the skeleton Ansible task.  It works best with Ansible 2.7.  Below version 2.7, it seems to require to uncomment the url line.

For example, to run command on VM

```yaml
- hosts: localhost
  connection: local
  gather_facts: no

  vars:
    resource_group: eric-rg-test
    vmname: eric-winvm-1

  tasks:
    - name: Sample for Azure REST API - VirtualMachines_RunCommand
      azure_rm_resource:
        #url: /subscriptions/{{ lookup('env','AZURE_SUBSCRIPTION_ID') }}/resourceGroups/{{ resource_group }}/providers/Microsoft.Compute/virtualMachines/{{ vmname }}/runCommand
        api_version: '2018-10-01'
        method: POST
        resource_group: "{{ resource_group }}"
        provider: compute
        resource_type: virtualmachines
        resource_name: "{{ vmname }}"
        subresource:
          - type: runcommand
        body:
          commandId: RunPowerShellScript
          script:
          - $url = "https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1"
          - $file = "c:\temp\ConfigureRemotingForAnsible.ps1"
#          - $file = "$env:temp\ConfigureRemotingForAnsible.ps1"
          - (New-Object -TypeName System.Net.WebClient).DownloadFile($url, $file)
          - powershell.exe -ExecutionPolicy ByPass -File $file
      register: output

    - debug:
        msg: "{{ output }}"
```