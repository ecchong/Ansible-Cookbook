### How to check async task status

```yaml
Asynchronous Task Status
To check task status, use async_status module

Required parameter: Job or task identifier:

---
\# Async status - fire-forget.yml
- name: Async status with fire and forget task
  hosts: demoservers
  remote_user: devops
  become: true
  tasks:

    - name: Download big file
      get_url: url=http://demo.example.com/bigfile.tar.gz
      async: 3600
      poll: 0
      register: download_sleeper

    - name: Wait for download to finish
      async_status: jid={{ download_sleeper.ansible_job_id }}
      register: job_result
      until: job_result.finished
      retries: 30
```