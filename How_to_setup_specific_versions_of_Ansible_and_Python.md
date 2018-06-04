### How to install a virtual environment with specific versions of Python and Ansible
```shell
download python-2.7.5
./configure --prefix=/home/echong/PYTHON-2.7.5
make
make install
virtualenv --python=PYTHON-2.7.5/bin/python venv-azure
source venv-azure/bin/activate
pip install ansible[azure]==2.5.0
```
