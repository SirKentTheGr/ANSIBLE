# Managing Variables

Ansible supports variables that can be used to store values that can be reused throughout files in an entire ansible project.

Varilables provide a convenient way to manage dynamic values for a given environment in your Ansible project. Some examples of calues that variables might contain include

* Users to create

* Packages to install

* Services to Restart

* Files to remove

* Archives to retrieve from the internet

### Naming variables

Variables have names which consist of a string that must start with a letter that can only baontain letters, numbers, and underscores.

i.e (web_server) (remote_file) (file_1) (remote_server_1)

Defining Variables: Three basic scope levels

* Global scope: Variables from the command line or ANsible configuration
* Play Scope:  Variables set in the play and related structures
* Host scope: Variables set on host groups and individual hosts by the inventory, fact gathering, or registered tasks

### Variables in Playbooks

Playbook variables cand be defined at the beginning of a playbook:

```
- hosts: all
  vars:
    user: joe
    home: /home/joe
```

It is also possible to define playbook variables in external files. In this case instead of using **vars** is to used **vars_files**

```
- hosts: all
  vars_files:
    -vars/users.yml

```


Once variables have been declared, administrators can use the variables in tasks. in this case by placing
name: "{{ user }}"


the recommended practice is to create a directory /group_vars and place files there and declare all of your variables there. 
