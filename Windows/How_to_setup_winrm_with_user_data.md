### How to use user data to setup WinRM on AWS

```shell
user_data: |
  <powershell>
  $url = "https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1"
  $file = "$env:temp\ConfigureRemotingForAnsible.ps1"
  (New-Object -TypeName System.Net.WebClient).DownloadFile($url, $file)
  powershell.exe -ExecutionPolicy ByPass -File $file -EnableCredSSP
  $Password = ConvertTo-SecureString "Password" -AsPlainText -Force
  New-LocalUser "local_ansible" -Password $Password -FullName "Ansible User" -Description "For running Ansible"
  Add-LocalGroupMember -Group Administrators -Member local_ansible
  </powershell>
```
