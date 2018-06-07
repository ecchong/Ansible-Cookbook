### How to append facts to a dictionary and append it to a list

We need to store some facts using set_fact, but we want to store them in a dictionary format.

For example, we want to store dictionary user information into a list accounts
```yaml
  tasks:
  - name: New dict
    set_fact:
      account: "{{ {} | combine( {'name':'john', 'phone':'123-123-1234'}) }}"

  - name: Add some more info
    set_fact:
      account: "{{ account | default ({}) | combine( {'gender':'male', 'age':'55'}) }}"

  - name: Append list
    set_fact:
      accounts: "{{ accounts | default ([]) + [ account ] }}"

  - name: New dict
    set_fact:
      account: "{{ {} | combine( {'name':'peter', 'phone':'212-222-4567'}) }}"

  - name: Append list
    set_fact:
      accounts: "{{ accounts | default ([]) + [ account ] }}"

  - debug:
      msg: "{{ accounts }}"
```

The result will looks like
```yaml
TASK [debug] ***********************************************************************************************************************************************
ok: [localhost] => {
    "msg": [
        {
            "age": "55",
            "gender": "male",
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
