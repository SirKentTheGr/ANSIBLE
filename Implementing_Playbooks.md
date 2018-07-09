# Implementing Playbooks

The real power of Ansible is learning how to use Playbooks to run multiple, complex tasks against a set of targeted hosts.

A play is an ordered set of tasks which should be run against hosts selected from your inventory. A Playbook is a text file that contains a list of one or more plays to run in order.

take this adhoc command for example:

`ansible -m user -a "name=newbie uid =4000 state=present" \ servera.lab.example.com`

this can be rewritten as a simple single-task play and saved ina playbook. The resulting playbook might look like this:

```
---
- name: Configure important user consistently
  hosts: servera.lab.example.command
  become: true
  tasks:
    - name: newbie exists with UID 4000
      user:
        name: newbie
        uid: 4000
        state: present
```

A playbook is text file written in YAML format, and is normally saved with the extension yml.

**A quick trick for setting your machine to auto edit .yml's with the correct format.**

`autocmd FileType yaml setlocal ai ts=2 sw=2 et`

this will change the spacing automatically for files recognized as .yml

To execute a playbook you would type

`ansible-playbook playbook.yml`

also please note that there is a syntax check

`ansible-playbook --syntax-check playbook.yml`


## Implementing Mulitple plays
