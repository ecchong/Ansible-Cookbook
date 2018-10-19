### How to enable or disable a host during import

We want to able to control the available of a managed host that is imported from dynamic inventory script.  Default behavior only allow disabling manually created host.  Host imported with dynamic inventory is always enabled.

To change this behavior:
1. Create a .py file under /etc/tower/conf.d  For example, hostvar-enabler.py
2. Insert into the file the following:
      SCM_ENABLED_VAR = 'isenabled'
      SCM_ENABLED_VALUE = 'true'
3. Restart Tower host

Now whenever a host is imported with variable 'isenabled': 'true' or without 'isenabled', it will be imported as enabled.  Anythingelse is set on variable 'isenabled', the host will be imported as disabled.  The variable name and value is arbitrary.

[https://access.redhat.com/solutions/3387661](https://access.redhat.com/solutions/3387661)