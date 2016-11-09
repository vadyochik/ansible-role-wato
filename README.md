# Ansible role for managing chack_mk hosts via WATO webapi

Role can be used for adding, deleting, getting info about or discovering services of the specified hosts via WATO webapi.

Was tested on OMD.

Required variables:
  - wato_webapi_user
  - wato_webapi_password
  - wato_webapi_base_url

Playbook advanced example (note: "wato_user", "wato_password", "wato_base_url" can be used in Rundeck or command line via "-e"):

```yaml
---
- hosts: all
  gather_facts: False
  vars:
    wato_webapi_user: "{{ lookup('consul_kv', 'secrets/wato_webapi_user') }}"
    wato_webapi_password: "{{ lookup('consul_kv', 'secrets/wato_webapi_password') }}"
    wato_webapi_base_url: "{{ lookup('consul_kv', 'secrets/wato_webapi_base_url') }}"
  pre_tasks:
    - set_fact: wato_webapi_user="{{ wato_user }}"
      when: wato_user is defined and not (wato_user is none or wato_user|trim == '')
    - set_fact: wato_webapi_password="{{ wato_password }}"
      when: wato_password is defined and not (wato_password is none or wato_password|trim == '')
    - set_fact: wato_webapi_base_url="{{ wato_base_url }}"
      when: wato_base_url is defined and not (wato_base_url is none or wato_base_url|trim == '')
  roles:
    - role: wato
```
