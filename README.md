# EX407-Ansible-Automation
Red Hat Certified Specialist in Ansible Automation (EX407) Preparation Course

- [Understanding Core Components of Ansible](#understanding-core-components-of-ansible)
    - [Understanding Core Components of Ansible Part 1](#understanding-core-components-of-ansible-part-1)
    - [Understanding Core Components of Ansible Part 2](#understanding-core-components-of-ansible-part-2)
    - [A Brief Tour of the Ansible Configuration File](#a-brief-tour-of-the-ansible-configuration-file)


## Understanding Core Components of Ansible
### Understanding Core Components of Ansible Part 1
This series of lessons lays the foundation for the remainder of the course content. Through a combination of lecture and command line demonstration, Students will gain a broad overview of Ansible. This particular lesson, focuses on Ansible inventories.
  
- Overview
  - Invetories
  - Modules
  - Variables
  - Facts 
  - Plays 
  - Playbooks
  - Configuration files

##### Inventories
![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img1.png)

- Inventory files may simply consist of a list of hostnames but can be much more robust

- It is also possible to define groups of hosts, host or group level variables, and groups of groups withing the inventory

- There are a number of variables that may be used within the inventory to control how ansible connects to and interacts with target hosts

- Commands to call ansible with `ping` module:
    - ```ansible innaghiyev1c.mylabserver.com -m ping -k``` - call ping module on `innaghiyev1c.mylabserver.com` host. Where `-m ping` is ping module
    and `-k` is key for asking password
    - ```ansible all -m ping -k``` - call all defined hosts in your inventory list `/etc/ansible/hosts/`
    - ```ansible -i inv.ini httpd -m ping -k``` - where `-i` - inventory file place, `httpd` hosts group name inside of `inv.ini` file
  
Output:
```
innaghiyev1c.mylabserver.com | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
```

### Understanding Core Components of Ansible Part 2
This series of lessons lays the foundation for the remainder of the course content. Through a combination of lecture and command line demonstration, Students will gain a broad overview of Ansible. This particular lesson covers the following topics at a very high level: modules, variables, facts, plays, playbooks, and configuration files.
  
- Modules
  - Modules are essentially tools for particular tasks
  - Modules can take (and usually do) take parameters
  - They return JSON
  - Can run from the command line or within a playbook
  - There are a significant number of modules for many kinds of work
  - Custom modules can be written
  
- Variables
  - Variable names should be letters, numbers and underscores
  - Variables should always start with a letter
  - Can be scoped by a group, host, or even ini a playbook
  - Typically used for configuration values and various parameters 
  - Variables can also be used to store the return value of executed commands
  - Ansible variables may also be dictionaries
  - There are a number of predefined variables used by Ansible 
  
- Facts
  - Facts provide certain information about given target host
  - Facts are discovered by Ansible automatically when it reaches out to a host
  - Fact gathering may be disabled
  - Facts may be cached between playbook executions, but this is not default behavior

```
innaghiyev1c.mylabserver.com | SUCCESS => {
    "ansible_facts": {
        "ansible_all_ipv4_addresses": [
            "172.31.37.72"
        ],
        "ansible_all_ipv6_addresses": [
            "2a05:d01c:2c7:d802:4db1:18cc:f13f:a1cf",
            "fe80::9e:19ff:fe1e:7376"
        ],
        "ansible_apparmor": {
            "status": "enabled"
        },
        "ansible_architecture": "x86_64",
        "ansible_bios_date": "10/16/2017",
        "ansible_bios_version": "1.0",
```

- Plays and playbooks
  - The goal of a play is to map a group of hosts to some well-defined roles
  - A play may use one or more modules to achieve a desired end state on a group of hosts
  - A playbook is a series of plays
  - A playbook may deploy new web servers, install a new application to existing application servers, and run SQL against some database servers to support the new application
  
- Configuration Files
  - Several possible locations (in order processed):
    - ANSIBLE_CONFIG (an environment variable)
    - ansible.cfg (in the current directory)
    - .ansible.cfg (in the home directory)
    - /etc/ansible/ansible.cfg (master configuration)
  - Configuration can also be set in environment variables
  - Some commonly used settings:
    - ansible_managed
    - forks
    - Inventory

### A Brief Tour of the Ansible Configuration File
The Ansible master configuration file is reviewed on a live system in this demonstration. Key configuration values are discussed as well as how to modify those values.
  
- Let's see some default values of *ansible.cfg* file located by `/etc/ansible/ansible.cfg` directory
```
[defaults]

# some basic default values...

#inventory      = /etc/ansible/hosts
#library        = /usr/share/my_modules/
#module_utils   = /usr/share/my_module_utils/
#remote_tmp     = ~/.ansible/tmp
#local_tmp      = ~/.ansible/tmp
#plugin_filters_cfg = /etc/ansible/plugin_filters.yml
#forks          = 5
#poll_interval  = 15
#sudo_user      = root
#ask_sudo_pass = True
#ask_pass      = True
#transport      = smart
#remote_port    = 22
#module_lang    = C
#module_set_locale = False
```
  
- Another handy block is following
```
[privilege_escalation]
#become=True
#become_method=sudo
#become_user=root
#become_ask_pass=False
```

