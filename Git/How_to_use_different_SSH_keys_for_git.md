### How to use different SSH keys for different GIT repos

Each GIT repo is assigned with it's own deploy key.  We can configure the .ssh/config file to use different keys for each repo.  Modify the config file "Host" field with a unique name, e.g. adding "-repo_name" after the hostname.

```shell
$ more ~/.ssh/config
Host github.com-Role1
   User ecchong
   IdentityFile ~/.ssh/github_deploy_key_1
   StrictHostKeyChecking no
   HostName github.com

Host github.com-Role2
   User ecchong
   IdentityFile ~/.ssh/github_deploy_key_2
   StrictHostKeyChecking no
   HostName github.com
```

In the requirements.yml file, append the same identifier string after server name.

```shell
$ more requirements.yml
- src: git@github.com-Role1:ecchong/Role1.git
  scm: git
  version: master

- src: git@github.com-Role2:ecchong/Role2.git
  scm: git
  version: master
```
Now running "ansible-galaxy" should pull both repoes using it's own key
```shell
ansible-galaxy install -r requirements.yml -p roles
```
[Reference](https://medium.com/@xiaolishen/use-multiple-ssh-keys-for-different-github-accounts-on-the-same-computer-7d7103ca8693)
