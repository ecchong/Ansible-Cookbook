### Using python yaml module
```shell
python -c 'import yaml, sys; print yaml.load(sys.stdin);' < my_playbook.yml
```
If no syntax error exists, Python prints the contents of the YAML file to stdout in JSON format.

The example here shows the use of the Python method on a YAML file with valid syntax.

### Use --syntax-check option
```shell
ansible-playbook --syntax-check my_playbook.yml
```