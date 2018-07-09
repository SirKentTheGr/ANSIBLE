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
