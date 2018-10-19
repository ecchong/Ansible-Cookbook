### How to test connection to host

We need to test connection to hosts, and run tasks on hosts that are online.  Hosts that are offline will be marked unreachable.  We need to clear them and continue next tasks on all hosts no matter they are online or off.

```yaml
- name: Test connections and run tasks
  block:
  - name: Check if host is online
    wait_for_connection:
      timeout: 3
  - name: Run some task on hosts that are reachable
    setup:
  rescue:
  - name: Reset hosts list.  Continue on all hosts after this block
    meta: clear_host_errors
```