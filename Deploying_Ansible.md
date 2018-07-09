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

### Running Ad Hoc Commands

An ad hoc command is a way to execute a single Ansible task quickly, on that you don't need to save to run again later. They're simple, one-line operations that can be run without writing a playbook.

They're useful for quick tests and changes. THis is a useful tool to quickly perform simple tasks with Ansible. Although they do have their limits.

Syntax:

`ansible hosts-pattern -m module [-a 'module arguments'][-i inventory]`

Example:(-b means sudo)

`ansible  all -m command -a 'id' -b`

`ansible -m yum -a 'name=httpd state=latest' -b`

`ansible all -m command -a 'whoami' -b`

`ansible-doc -l` command lists all the modules that are installed on the system. you can then use `ansible-doc` to view the documentation of particular modules by name and find information about the arguments the modules take as options. Example `ansible-doc ping`

Ansible Command Line options

Inventory           -i

remote_user         -u

become              --become, -b

become_method       --become-method

become_user         --become-user

become_ask_pass     --ask-become-pass, -k







### Generating Inventories Dynamically

Static Inventory files are easy to write and are convenient for managing small infrastructures. When working with a large number of machines, it can be hard  to keep the static inventory files up to date.

Contributed scripts to the ansible project reside at:

 https://github.com/ansible/ansible/tree/devel/contrib/inventory
