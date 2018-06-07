### How to append facts to a dictionary and append it to a list

We need to store some facts using set_fact, but we want to store them in a dictionary format.

For example, we want to store dictionary user information into a list accounts
```yaml
  tasks:
  - name: Create account
    set_fact:
      account: "{{ accunt | default ({}) | combine( {'name':'john', 'phone':'123-123-1234'}) }}"

  - name: Append list
    set_fact:
      accounts: "{{ accounts | default ([]) + [ account ] }}"

  - name: Append dict 2
    set_fact:
      account: "{{ accunt | default ({}) | combine( {'name':'peter', 'phone':'212-222-4567'}) }}"

  - name: Append list
    set_fact:
      accounts: "{{ accounts | default ([]) + [ account ] }}"

  - debug:
      msg: "{{ accounts }}"
```

The output will looks like
```yaml
TASK [debug] ***********************************************************************************************************************************************
ok: [localhost] => {
    "msg": [
        {
            "name": "john",
            "phone": "123-123-1234"
        },
        {
            "name": "peter",
            "phone": "212-222-4567"
        }
    ]
}
```
