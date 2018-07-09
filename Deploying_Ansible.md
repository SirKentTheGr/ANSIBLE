The example below is a **Static Inventory**

```
[dev]
servera.lab.example.com
serverb.lab.example.com

[prod]

[class]
serverb.lab.example.com

[servers:children]
dev
prod
```
this is a static inventory file: [dev] is the group name and below is the host/hosts: NOTE: this can also be an IP address. This is not required for the install steps per say - but it is part of the lab hosted by RHEL and will not work so well outside of the lab environment:

Test the inventory file:

`ansible dev -i inventory --list-hosts`

`ansible prod -i inventory --list-hosts`

etc etc

**Dynamic Inventory**

Utilizing information provided by external databases. there are a number of dynamic inventory scripts


=====================================================

## Configuring ANSIBLE

The behavior of an ANSIBLE installation can be customized by modiying settings in the ansible configuration file

`/etc/ansible/ansible.cfg`

This file is used if no other configuration file is found.

using this ansible looks for ~/.ansible.cfg in the user/s home directory. This configuration is used instead of the /etc/ansible/ansible.cfg.

If an ansible.cfg file exists in the directory in which the ansible command is executed, it is used instead of the global file or the user's personal file.

The recommened practice is to create an ansible.cfg file in a directory from which you run ansible commands. This directory would also contain any files used by your ansible project, such as a playbook.

You can also use different configuration files by placing them in different directories and then executing Ansible commands from the appropriate directories, but this method can be restrictive and hard to manage as the number of configuration files grows. A more flexible option is to define the location of the configuration file withe **$ANSIBLE_CONFIG** environment variable.

==================================================
Guided Exercise: Mangaging Ansible Configuration Files:

create `/home/student/dep-manage` directory

`cd /home/student/dep-manage`

in your  `/home/student/dep-manage` directory use a text editory to start editing a new file `ansible.cfg`.

create a [defaults] section in that file. In that section, add a line which uses the **inventory** directive to specify the **./inventory** file as the default inventory.

```

vi /home/student/dep-manage/ansible.cfg

[defaults]
inventory = ./inventory
```
:wq

in the `/home/student/dep-manage` directory, use a text editory to start editing the new static inventory file, **inventory**

```
vi /home/student/dep-manage/inventory

[myself]
localhost

[intranetweb]
servera.lab.example.com

[everyone:children]
myself
intranetweb

:wq
```

Use Ansible with the --list-hosts option to test the configuration:

`ansible myself --list-host`

etc - test all three:

Next: create the ansible.cfg file to automatically use sudo to switch from student to root when running tasks on the managed hosts:

```
vi /home/student/dep-manage/ansible.cfg

[defaults]
inventory = ./inventory

[privilege_escalation]
become = true
become_method = sudo
become_user = root
become_ask_pass = true
```

now run the ansible --list-hosts command again to verify that you are now prompted for the sudo password. Add the -v option to see the location of the current configuration file being used.
`ansible intranetweb --list-hosts -v`

confirm that you can run Ansible tasks on the managed hosts. Run an ansible command targeting the everyone group, but replace --list-hosts with -m ping. that will run the ping module, which confirms  that you can successfully run Ansible modules that use Python on the managed hosts. This should work, assuming that the stundent user can log into the managed hosts using the SSH key-based authentication.

`ansible everyone -m ping`


=====================================================
