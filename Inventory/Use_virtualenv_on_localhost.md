### Force to use virtualenv python
When running modules that require virtualenv, such as Azure, local_action or localhost connection sometimes still  use the  default /usr/bin/python

```yaml
localhost ansible_python_interpreter=python
```
now localhost will run python from the activated virtualenv.
[See this](http://www.zigg.com/2014/using-virtualenv-python-local-ansible.html)