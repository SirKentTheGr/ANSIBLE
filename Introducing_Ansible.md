# Introducing Ansible

Starting with some basic virtual machine management. We have a classroom specific ctl command set for reseting and starting VM's.

`rht-vmctl status all`
`rht-vmctl start server`
`rht-vmctl view server`
`rht-vmctl reset server`

### ANSIBLE
* The difference with Ansible and other automation tools like puppet is that ANSIBLE is 'Agentless'. This means that nothing special needs to be installed on distant machines in order to configure it.

* ANSIBLE is written in python. Go figure.

* Introducing the term - **ANSIBLE PLAYBOOK**: - a list of tasks - that are text bases - and are typically human readable.

* Ansible PLAYBOOK is defined in the syntax of YAML

* remember - Complexity Kills Productivity. Simpler is better. ANSIBLE is designed so that its tools are simple to use.

* Optimize for Readability: The ANSIBLE automation is built around simple, declarative, text-based files.

* Think Declaratively: Trying to treat ANSIBLE like a scripting language is not the right approach. ANSIBLE's goal is to put your systems into a desired state, only making changes that are necessary.

### INTRO ANSIBLE VOCABULARY:

* Configuration Management: Centralizing configuration file management and deployment is a common use case for ANSIBLE, and it's howmany power users are first introduced to the ANSIBLE automation platform.

* Application Deployment: When you define your application with ANSIBLE, and manage the deployment with ANSIBLE Tower, teams can effectively manage the entire application life cycle from the development to production.

* Provisioning: Applications have to be deployed or installed on systems. Ansible and Ansible Tower can help streamline the process of provisioning systems, whether you're PXE boothing and kickstarting bare-metal servers or virtual machines, or creating virtual machines or cloud instances from templates.

* Continuous Delivery: Creating a CI/CD pipeline requires coordination and buy-in from numerous teams. You can't do it without a simple automation platform that everyone in your organization can use. Ansible Playbooks keep your applications properly deployed (and managed) throughout their entire life cycle.

* Security and Compliance: When your security policy is defined in ANSIBLE, scanning and remediation of site-wide security policies can be integrated into other automated processes. Instead of being an afterthought, it is an integral part of everything that is deployed.

* Orchestration: Configurations alone don't define your environment. You need to define how multiple configurations interact, and ensure the disparate pieces can be managed as a whole.

## Installing ANSIBLE

Python 2 version 2.6 or later needs to be installed on the control node. To see whether the appropriate version of Python is installed:
`yum list installed python`

Python 2 Version 2.4 or later is required for most modules to work on mangaed hosts. If the version of Python installed on the managed host is earlier than Python 2.5, then the python-simplejson package must also be installed.

Most of the modules specifically designed for Microsoft Windows managed hosts require PowerShell 3.0 or higher on the managed hosts rather than Python. In addition the managed hosts need to have PowerShell remoting configured.


Install ANSIBLE:


using the command ansible and ansible-playbook are going to be a couple of commands introduced with this tool.

`ansible --help`

`ansible-playbook --help`

```
yum list installed python
sudo yum install ansible
mkdir /home/student/dep-install
cd /home/student/dep-install
```

use a text editor to create `/home/student/dep-install/inventory` containing the following lines:

Note this can a file or even an entire directory (being the inventory)

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
