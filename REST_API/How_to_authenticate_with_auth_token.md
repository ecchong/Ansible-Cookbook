## How to authenticate with server and retrieve a token.  Then submit a JSON file via REST API.

To login and obtain a token.  Then submit a payload file using the given token.

```yaml
---
- hosts: localhost
  gather_facts: no
  connection: local

  vars:
    username: user1
    domain: dev
    auth_url: http://server1/SysInfo/auth/login
    api_url:  http://server1/SysInfo/api/hw/v1/
    json_file: payload.json

  vars_prompt:
  - name: password
    prompt: password
  
  tasks:
  - name: Set password
    set_fact:
      login_info:
        password: '{{ password }}'
        username: '{{ username }}'
        domain: '{{ domain }}'
    
  - name: Get authentication token
    uri:
      url: '{{ auth_url }}'
      method: POST
      headers:
        Content-Type: "application/json"
      body: "{{ login_info | to_json }}"
      body_format: json
      return_content: yes
      status_code: 200
    register: auth_token

  - debug:
      msg: "{{ auth_token.json.token }}"

  - name: Submit payload
    uri:
      url: '{{ api_url }}'
      method: POST
      headers:
        Authorization: "Bearer {{ auth_token.json.token }}"
        Content-Type: "application/json"
        Accept: '*/*'
      body: "{{ lookup('file', '{{ json_file }}') | replace('\n','') }}"
      body_format: json
      return_content: yes
      status_code: 201,200
    register: submit_output
```

Noted that newer version of Tower (3.4) supported personal authentication token.  User can create a personal token via the GUI and use it in their scripts.