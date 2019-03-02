## How to launch a job template or workflow template via REST API call

```yaml
  tasks:
  - name: Launch Tower Job
    uri:
      url: '{{ tower_url }}/job_templates/{{ template_id }}/launch/'
      return_cotent: yes
      method: POST
      user: admin
      password: password
      headers:
        Content-Type: 'application/json'
      body: "{\"extra_vars\":{\"sleep_time\":\"5\"}}"
      status_code: 201
    register: output

  - name: Get job status
    uri:
      url: '{{ tower_url }}/jobs/{{ output.json.id }}/'
      return_cotent: yes
      method: GET
      user: admin
      password: password
      headers:
        Content-Type: 'application/json'
      status_code: 200
    register: job_status
    until: job_status.status == 'successful'
    retries: 2
    delay: 120
```
Noted that extra_vars need to be set to prompt on launch in order to allow passing extra variables thru the REST API call.  Current version of Tower (3.4) does not allow prompt on launch for workflow template.  So we need to create a survey form with the intended extra variables name.