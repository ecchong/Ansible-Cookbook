### Start the asynchronous task and check start later
```yaml
  - name: Run sleep
    shell: sleep 30
    async: 30
    poll: 0
    register: async_output

  - debug:
      msg: "Started an async job {{async_output}}"

  - name: check async status
    async_status:
      jid: "{{ async_output.ansible_job_id }}"
    register: async_result
    until: async_result.finished
    retries: 50
    delay: 5
```