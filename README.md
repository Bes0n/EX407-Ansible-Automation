# EX407-Ansible-Automation
Red Hat Certified Specialist in Ansible Automation (EX407) Preparation Course

- [Understanding Core Components of Ansible](#understanding-core-components-of-ansible)
    - [Understanding Core Components of Ansible Part 1](#understanding-core-components-of-ansible-part-1)
    - [Understanding Core Components of Ansible Part 2](#understanding-core-components-of-ansible-part-2)
    - [A Brief Tour of the Ansible Configuration File](#a-brief-tour-of-the-ansible-configuration-file)
    - [LAB: Getting Started with Ansible](#lab-getting-started-with-ansible)
- [Run Ad-Hoc Ansible Commands](#run-ad-hoc-ansible-commands)
    - [Run Ad-Hoc Ansible Commands](#run-ad-hoc-ansible-commands)
    - [Demonstration: Ansible Ad-Hoc Commands Part 1](#demonstration-ansible-ad-hoc-commands-part-1)
    - [Demonstration: Ansible Ad-Hoc Commands Part 2](#demonstration-ansible-ad-hoc-commands-part-2)
    - [LAB: Ad-Hoc Ansible Commands](#lab-ad-hoc-ansible-commands)
- [Inventory Management](#inventory-management)
    - [Inventory Essentials and Inventory Variables](#inventory-essentials-and-inventory-variables)
    - [Demo: Variables and Inventories](#demo-variables-and-inventories)
    - [Demo: Using YAML in Inventories](#demo-using-yaml-in-inventories)
    - [Dynamic Inventories](#dynamic-inventories)
    - [Demo: Dynamic Inventories](#demo-dynamic-inventories)
    - [LAB: Working with Ansible Inventories](#lab-working-with-ansible-inventories)
- [Create Ansible Plays and Playbooks](#create-ansible-plays-and-playbooks)
    - [Introduction to Playbooks and Common Modules](#introduction-to-playbooks-and-common-modules)
    - [Create Playbooks to Configure Systems to a Specified State](#create-playbooks-to-configure-systems-to-a-specified-state)
    - [Basic Playbook Syntax Demonstration](#basic-playbook-syntax-demonstration)
    - [Use Variables to Retrieve the Results of Running Commands](#use-variables-to-retrieve-the-results-of-running-commands)
    - [Use Conditionals to Control Play Execution Part 1](#use-conditionals-to-control-play-execution-part-1)
    - [Use Conditionals to Control Play Execution Part 2](#use-conditionals-to-control-play-execution-part-2)
    - [Configure Error Handling](#configure-error-handling)
    - [Demo: Error Handling – Ignore Errors](#demo-error-handling--ignore-errors)
    - [Demo: Error Handling – Block Groups](#demo-error-handling--block-groups)
    - [Selectively Run Specific Tasks In Playbooks Using Tags](#selectively-run-specific-tasks-in-playbooks-using-tags)
    - [LAB: Ansible Playbooks: The Basics](#lab-ansible-playbooks-the-basics)
    - [LAB: Ansible Playbooks - Error Handling](#lab-ansible-playbooks---error-handling)
- [Create and Use Templates to Create Customized Configuration Files](#create-and-use-templates-to-create-customized-configuration-files)
    - [Using Ansible Templates Lecture](#using-ansible-templates-lecture)
    - [Demo: Using Ansible Templates](#demo-using-ansible-templates)
- [Work with Ansible Variables and Facts](#work-with-ansible-variables-and-facts)
    - [Ansible Variables Lecture](#ansible-variables-lecture)
    - [Demo: Ansible Variables - Magic Variables and Jinja Filters](#demo-ansible-variables---magic-variables-and-jinja-filters)  
    - [Demo: Ansible Variables - Variable Files](#demo-ansible-variables---variable-files)
    - [Ansible Facts Lecture](#ansible-facts-lecture)
    - [Demo: Working with Ansible Facts](#demo-working-with-ansible-facts)
    - [LAB: Working with Ansible Templates, Variables, and Facts](#lab-working-with-ansible-templates-variables-and-facts)  
- [Create and Work with Roles](#create-and-work-with-roles)
    - [Working with Ansible Roles Lecture](#working-with-ansible-roles-lecture)
    - [Demo: Creating and Applying a Role in Ansible](#demo-creating-and-applying-a-role-in-ansible)
    - [Applying In-Line Roles and Role Dependencies](#applying-in-line-roles-and-role-dependencies)
    - [LAB: Working with Ansible Roles](#lab-working-with-ansible-roles)
- [Download roles from an Ansible Galaxy](#download-roles-from-an-ansible-galaxy)
    - [Download Roles from Ansible Galaxy](#download-roles-from-ansible-galaxy)  
- [Managing Parallelism](#managing-parallelism)
    - [Parallelism in Ansible](#parallelism-in-ansible)
- [Use Ansible Vault in Playbooks to Protect Sensitive Data](#use-ansible-vault-in-playbooks-to-protect-sensitive-data)
    - [The Ansible-Vault Command](#the-ansible-vault-command)
    - [Using Vaults in Playbooks](#using-vaults-in-playbooks)
    - [LAB: Working with Confidential Data in Ansible](#lab-working-with-confidential-data-in-ansible)  
- [Install Ansible Tower and Use it to Manage Systems](#install-ansible-tower-and-use-it-to-manage-systems)
    - [Introduction to Ansible Tower](#introduction-to-ansible-tower)
    - [Installing Ansible Tower](#installing-ansible-tower)
    - [Demo: Working with Ansible Tower](#demo-working-with-ansible-tower)
- [Use Documentation to Look Up Specific Information About Ansible Modules and Commands](#use-documentation-to-look-up-specific-information-about-ansible-modules-and-commands)
    - [Finding Documentation](#finding-documentation)
- [Ansible 2.7 Exam Update](#ansible-2.7-exam-update)
    - [Install and Configure Control Node and Ansible Nodes](#install-and-configure-control-node-and-ansible-nodes)
    - [Shell Scripts to Run Ad-Hoc Commands](#shell-scripts-to-run-ad-hoc-commands)
    - [Firewall Rules](#firewall-rules)
    - [Archiving](#archiving)
    - [Scheduled Tasks: Cron](#scheduled-tasks-cron)
    - [Scheduled Tasks: `at`](#scheduled-tasks-at)
    - [Security](#security)

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

### LAB: Getting Started with Ansible
The very first step to harnessing the power of Ansible is configuring your environment. This activity goes over installing Ansible on a control node and configuring two managed servers for use with Ansible. We will also create a simple inventory and run an Ansible command to verify our configuration is correct.
  
##### Additional Information and Resources
Your CIO has greenlit a proof of concept for Ansible in your environment. You are to set up an Ansible control node in a test environment and verify basic functionality. You have three demo hosts, one to be the control node (`control1`), and two to serve as managed nodes (`node1` and `node2`). You must complete the following steps:
  
- Install Ansible on the `control` node.
- Configure the `ansible` user on the control node for ssh shared key access to managed nodes.
  Note: do not use a passphrase for the key pair.
- Create a simple Ansible inventory on the control node in `/home/ansible/inventory` containing node1 and node2.
- Configure sudo access for Ansible on `node1` and `node2` so that Ansible may use `sudo` for any command with no password prompt.
- Verify each managed node can be accessed by Ansible from the control node using the `ping` module. Redirect the output of a successful command to `/home/ansible/output`.
  
Important Notes:
- The user `ansible` is already present on all servers for your convenience.
- The `ansible` user has the same password as the `cloud_user`.
- `/etc/hosts` entries are present on `control1` for the managed nodes.

##### Install Ansible on the control node.
- To install Ansible on the control node, run  ansible.
```
yum install ansible
```

- If package not found run
```
yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
```

##### Configure the `ansible` user on the control node for ssh shared key access to managed nodes. Do not use a passphrase for the key pair.
- To create a keypair for the ansible user on the control host, run the following:
  - `sudo su - ansible`
  - `ssh-keygen` (accept all defaults: press enter for each prompt)

- Copy the `public key` to both `node1` and `node2`.

- As the ansible user on the control host:
  - `ssh-copy-id node1` (accept the host key if prompted, authenticate as ansible user)
  - `ssh-copy-id node2` (accept the host key if prompted, authenticate as ansible user)

##### Create a simple Ansible inventory on the control node in `/home/ansible/inventory` containing `node1` and `node2`.
- On the control host:
  - `sudo su - ansible` (if not already ansible user)
  - `touch /home/ansible/inventory`
  - `echo "node1" >> /home/ansible/inventory`
  - `echo "node2" >> /home/ansible/inventory`

##### Configure sudo access for Ansible on `node1` and `node2` such that Ansible may use sudo for any command with no password prompt.
- Log in to node1 as cloud_user and edit the sudoers file to contain appropriate access for the ansible user:
  - `ssh cloud_user@node1`
  - `sudo visudo`
  - Add the following line to the file and save:
```
ansible    ALL=(ALL)       NOPASSWD: ALL
```

- Repeate these steps for `node2`.

##### Verify each managed node is able to be accessed by Ansible from the control node using the `ping` module. Redirect the output of a successful command to `/home/ansible/output`.
- To verify each node, run the following as the `ansible` user from the control host:
  - `ansible -i /home/ansible/inventory node1 -m ping`
  - `ansible -i /home/ansible/inventory node2 -m ping`
- To redirect output of a successful command to `/home/ansible/output`:
  - `ansible -i /home/ansible/inventory node1 -m ping > /home/ansible/output`


## Run Ad-Hoc Ansible Commands
### Run Ad-Hoc Ansible Commands
Learn how to use ad-hoc ansible commands for simple system managment. This lecture covers one of the key objectives for Red Hat exam 407.

- Overview:
    - What is an ad-hoc command in Ansible? 
    - Use cases for ad-hoc commands
    - Ad-hoc vs Playbook
    - Ansible command syntax
    - Common modules

- What is an ad-hoc command in Ansible
    - You can run ansible either ad-hoc or as a playbook
    - Both methods have the same capabilities
    - Ad-hoc commands are effectively one-liners

- Use cases for Ad-hoc
    - Operational commands
        - Checking log contents
        - Daemon control
        - Process management
    - Informational commands
        - Check installed software
        - Check system properties
        - Gather system performance information
    - Research
        - Work with unfamiliar modules on test systems
        - Practice for playbook engineering

##### Ad-hoc vs Playbook
  
![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img2.png)
  
##### Common Modules

![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img3.png)

![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img4.png)

![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img5.png)


### Demonstration: Ansible Ad-Hoc Commands Part 1
  
- Let's use `yum` as an example of ad-hoc command
    - `ansible myserver.example.com -i inv.ini -m yum -b -a "name=elinks state=latest"` - install **elinks** with **latest** version
        - `-i` - key for inventory host file
        - `-m yum` - use `yum` module 
        - `-b` - become (by default become **root**). Can be changed in `/etc/ansible/ansible.cfg` file
        - `-a "name=elinks state=latest"` - arguments. For `yum` module we're using **name** and **state**
    - `ansible myserver.example.com -i inv.ini -m yum -b -a "name=elinks state=absent"` - state **absent** will uninstall **elinks**

### Demonstration: Ansible Ad-Hoc Commands Part 2

- Let's work with a **file** module
    - `ansible myserver.example.com -i inv.ini -m file -a "name=/home/user/newfile state=touch"`
        - `-m file` - using **file** module
        - `-a "name=/home/user/newfile state=touch"` - arguments **name** - for declaring path of file and **state** what to do with it. 
    - `ansible myserver.example.com -i inv.ini -m file -a "name=/home/user/newfile"` - get **properties** of the file
    - `ansible myserver.example.com -i inv.ini -m file -a "name=/home/user/newfile mode=0400"` - set a **mode** of the file to **0400**
    - `ansible myserver.example.com -i inv.ini -m file -b -a "name=/home/user/newfile owner=root"` - we are changing file owner to **root** and using `-b`
    key for become. 
    - `ansible myserver.example.com -i inv.ini -m user -b -a "name=sam"` - create user **sam**
        - `-m user` - using **user** module
        - `-a "name=sam"` - as argument we indicate user name  
    - `ansible myserver.example.com -i inv.ini -m user -b -a "name=sam append=yes groups=wheel"` - add user to a **wheel** group.
        - `append=yes` - for appending group, otherwise it will wipe out previous groups
        - `groups=wheel` - define which group needs to be added

### LAB: Ad-Hoc Ansible Commands
One of the keys to success with Ansible is being able to run `ad-hoc` commands. The value of `ad-hoc` commands is underscored by the fact that it is an objective of the Red Hat Certified Ansible Specialist exam. This exercise guides students through crafting many `ad-hoc` commands which will not only build experience with the concept but also broaden the students' exposure to various Ansible command modules.

#### Additional Information and Resources
Some consultants have been employed to perform audits on a number of systems in your company's environment. You must create the user accounts noted in `/home/ansible/userlist.txt` and set up the provided public keys for their accounts. The security team has built a jump host for the consultants to access production systems and provided the full key-pair to you so you may set up and test the connection. All hosts in `dbsystems` will need the provided public key installed so the consultants may use key-pair authentication to access the systems. Also, you must ensure the `auditd` service is enabled and running on all systems.
  
To summarize, you must do the following:
- Create the user accounts noted in `/home/ansible/userlist.txt`.
- Copy the `authorized_keys` file for each user to the correct location so the new accounts can log in with ssh key authentication.
- Ensure `auditd` is enabled and running on all systems.
  
Important notes:
- For your convenience, Ansible is already on the control node. If you connect to the server by clicking on the Public IP address in your browser, make sure to change to the ansible user with the `su - ansible` command.

- The user `ansible` is present on all servers with appropriate shared keys for access to managed servers from the control node. Make sure to use this user to complete the commands.
- The `ansible` user has the same password as `cloud_user`.
- The default Ansible inventory has been configured for you with the appropriate hosts and groups.
- `/etc/hosts` entries are present on `control1` for the managed servers.
  
#### Learning Objectives
##### Create the User Accounts Noted in `/home/ansible/userlist.txt`
- `ansible dbsystems -b -m user -a "name=consultant"`
- `ansible dbsystems -b -m user -a "name=supervisor"`

##### Place Key Files in the Correct Location, `/home/$USER/.ssh/authorized_keys`, on Hosts in `dbsystems`
- `ansible dbsystems -b -m file -a "path=/home/consultant/.ssh state=directory owner=consultant group=consultant mode=0755"`
- `ansible dbsystems -b -m copy -a "src=/home/ansible/keys/consultant/authorized_keys dest=/home/consultant/.ssh/authorized_keys mode=0600 owner=consultant group=consultant"`
- `ansible dbsystems -b -m file -a "path=/home/supervisor/.ssh state=directory owner=supervisor group=supervisor mode=0755"`
- `ansible dbsystems -b -m copy -a "src=/home/ansible/keys/supervisor/authorized_keys dest=/home/supervisor/.ssh/authorized_keys mode=0600 owner=supervisor group=supervisor"`

##### Ensure `auditd` Is Enabled and Running on All Hosts
- `ansible all -b -m service -a "name=auditd state=started enabled=yes"`
  

## Inventory Management
### Inventory Essentials and Inventory Variables
In Ansible, inventories are crucially important as they serve as the foundation for ansible automation. This lecture extends on the basic inventory concpets already covered such as file format and location.  Students will be introduced to the concept of static and dynamic inventories and learn about how inventories and variables work together. 
  
##### Overview
- Use both static and dynamic inventories to define groups of hosts:
    - What is the inventory
    - File formats
    - Statis vs. Dynamic
    - Variables and inventories
- Utilize an existing dynamic inventory script:
    - On dynamic inventories
    - Some popular options
  
##### What is an Inventory
- An inventory is a list of hosts that Ansible manages
- Inventory location may be specified as follows:
    - Default: /etc/ansible/hosts
    - Specified by CLI: ansible -i <filename>
    - Can be set in ansible.cfg
- The inventory file may contain hosts, patterns, groups, and variables
- You may specofy the inventory as a directory containing a series of inventory files (both static and dynamic)
- The inventory may be specified in YAML or INI format
- Can be static or dynamic

##### File Formats 
  
![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img6.png)
  
##### Static vs. Dynamic
  
![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img7.png)
  
##### Variables and Inventories
  
![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img8.png)
  
### Demo: Variables and Inventories
Being able to work with inventories and variables is an essential skill for any user of Ansible. This command line demonstration will show students the best practices for using variables within inventories.
  
Inside of **inventory** directory we have following structure: 
```
[cloud_user@innaghiyev2c inventory]$ ls -l
total 4
drwxrwxr-x. 2 cloud_user cloud_user  23 Feb 28 05:18 group_vars
drwxrwxr-x. 2 cloud_user cloud_user  25 Feb 27 10:53 host_vars
-rw-rw-r--. 1 cloud_user cloud_user 127 Feb 27 10:41 inventory
```
  
Where:
- `inventory` - stores our hosts
```
[cloud_user@innaghiyev2c inventory]$ cat inventory
innaghiyev1c ansible_host=innaghiyev1c.mylabserver.com

[labservers]
innaghiyev3c.mylabserver.com
innaghiyev1c.mylabserver.com
```
  
- `group_vars` - contains group name of our hosts' group. `labservers` - name of group, which contains variables
```
[cloud_user@innaghiyev2c inventory]$ ls -l group_vars/
total 4
-rw-rw-r--. 1 cloud_user cloud_user 50 Feb 28 05:18 labservers
[cloud_user@innaghiyev2c inventory]$ cat group_vars/labservers
logs : /var/log/messages
secure : /var/log/secure
```
  
- `host_vars` - contains hostname with stored variable inside. `innaghiyev1c` - name of the host, which contains variables
```
[cloud_user@innaghiyev2c inventory]$ ls host_vars/
innaghiyev1c
[cloud_user@innaghiyev2c inventory]$ cat host_vars/innaghiyev1c
opt_dir : /opt
```
  
### Demo: Using YAML in Inventories
Inventories may be specified in INI or YAML format. This demonstration goes over how to use YAML to create an inventory. Students will benefit from a refresher on YAML syntax as well as review key details on Ansible inventories.
  
This is how YAML inventory file looks like:
```
all:
  hosts:
    innaghiyev1c.mylabserver.com:
  children:
    production:
      hosts:
        innaghiyev1c.mylabserver.com:
        innaghiyev3c.mylabserver.com:
    labservers:
      hosts:
        innaghiyev[1:3]c.mylabserver.com:
```

### Dynamic Inventories
Being able to use dynamic inventories in essential skill for any Ansible specialist. This lecture goes over the details of how dynamic inventories in Ansible work.

![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img9.png)
  
Some Popular Options:

![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img10.png)

### Demo: Dynamic Inventories
- `chmod +x script.py` - script for dynamic inventory must be executable. Output of your script must be in **JSON** format
- `ansible all -i script.py -m ping` - usage of dynamic inventory is the same as a static one


### LAB: Working with Ansible Inventories
#### Additional Information and Resources
Your company has decided the backup software license is frivolous and unnecessary. As a consequence, the license was not renewed. Your supervisor has created a simple script and an Ansible playbook to create an archive of select files, depending on pre-defined Ansible host groups, as a stop-gap measure. You will create the inventory file to complete the backup strategy.
  
You must do the following:
- Create the inventory file in **/home/ansible/inventory**.
- Configure the host group **media** to contain media1 and media2.
- Define the following variables for **media** with their accompanying values:
  - **media_content** should be set to `/var/media/content/`.
  - **media_index** should be set to `/opt/media/mediaIndex`.
- Configure the host group **webservers** to contain the hosts web1 and web2.
- Define the following variables for `webservers` with their accompanying values:
  - **httpd_webroot** should be set to `/var/www/`
  - **httpd_config** should be set to `/etc/httpd/`
- Define the variable **script_files** specifically for web1. The value of **script_files** should be set to `/usr/local/scripts`.
- You can run `/home/ansible/scripts/backup.sh` to test your inventory. If you have correctly configured the inventory, it should not error.
- Do not edit anything in **/home/ansible/scripts/**.
  
Important notes:
- For your convenience, Ansible has been installed on the control node.
- The user `ansible` has already been created on all servers with appropriate shared keys for access to managed servers from the control node.
- The `ansible` user has the same password as `cloud_user`.
- `/etc/hosts` entries have been made on control1 for the managed servers.
- Do not edit anything in `/home/ansible/scripts/`.

#### Learning Objectives
##### Create the `inventory` File in `/home/ansible/`
- `touch /home/ansible/inventory`
##### Configure the Host Group `media` to Contain `media1` and `media2`
- `echo "[media]" >> /home/ansible/inventory`
- `echo "media1" >> /home/ansible/inventory`
- `echo "media2" >> /home/ansible/inventory`
##### Define Variables for `media` with Their Accompanying Values
- `mkdir /home/ansible/group_vars`
- `touch /home/ansible/group_vars/media`
- `echo "media_content: /var/media/content/" >> /home/ansible/group_vars/media`
- `echo "media_index: /opt/media/mediaIndex" >> /home/ansible/group_vars/media`
##### Configure the Host Group `webservers` to Contain the Hosts `web1` and `web2`
- `echo "[webservers]" >> /home/ansible/inventory`
- `echo "web1" >> /home/ansible/inventory`
- `echo "web2" >> /home/ansible/inventory`
##### Define Variables for `webservers` with Their Accompanying Values
- `touch /home/ansible/group_vars/webservers`
- `echo "httpd_webroot: /var/www/" >> /home/ansible/group_vars/webservers`
- `echo "httpd_config: /etc/httpd/" >> /home/ansible/group_vars/webservers`
##### Define the Variable `script_files` Specifically for `web1`, Setting Its Value to `/usr/local/scripts`
- `mkdir /home/ansible/host_vars`
- `touch /home/ansible/host_vars/web1`
- `echo "script_files: /usr/local/scripts" >> /home/ansible/host_vars/web1`
  
  
## Create Ansible Plays and Playbooks
### Introduction to Playbooks and Common Modules
This less provides an overview of the section and reviews some of the common modules that will continue showing up as the playbook discussion occurs.
  
#### Overview:
- Know how to work with commonly used Ansible modules
- Create playbooks to configure systems to a specified state
- Use variables to retrieve the results of running commands
- Use conditionals to control play execution
- Configure error handling 
- Selectively run specified tasks in playbooks using tags

#### Know how to work with Commonly Used Ansible Modules
- Core modules to be familiar with:
  - Working with files: copy, archive, unarchive, get_url
  - user, group
  - ping
  - service
  - yum
- Lineinfile module
- htpasswd
- Shell and command modules
- Script module
- Debug module
- https://docs.ansible.com/ansible/latest/modules/modules_by_category.html

### Create Playbooks to Configure Systems to a Specified State
  
![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img11.png)

### Basic Playbook Syntax Demonstration
Let's write some simple playbook. 
```
--- #to mention that this is a playbook
- hosts: labservers #define hosts group
  become: yes #become means sudo, by default is root user 
  tasks: #what to do on defined hosts
    - name: install apache #task name, can be anything
      yum: #what module to call
        name: httpd #package name
        state: latest #state of that package, version, absent etc.
    - name: start and enable httpd #task name
      service: #module name
        name: httpd #service name
        state: started #what is desired state of that service 
        enabled: yes #enable service, equal to systemctl enable httpd
    - name: create index.html #name of task 
      file: #module name 
        path: /var/www/html/index.html #path of file to change
        state: touch #what to do with that file, in our case - touch
    - name: add a linex to index.html #task name
      lineinfile: #module name
        path: /var/www/html/index.html #path to the file
        line: "Hello World" #check line, if not exist add it
```
  
- `ansible-playbook playbook.yml` - instead of **ansible** - ad-hoc run, we're running **ansible-playbook** to execute playbook file.
- `ansible-playbook playbook.yml --limit innaghiyev1c.mylabserver.com` - set limits on playbook run and execute it only on limited host. 

### Use Variables to Retrieve the Results of Running Commands
  
![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img12.png)

- by `register` we can get a lot of information regarding module. What has been changed, where etc
- playbook with retriving output as a variable
```
---
- hosts: labservers
  tasks:
    - name: create file
      file:
        path: /tmp/newfile
        state: touch
      register: output
    - debug: msg="Register output is {{output}}"
    - name: edit file
      lineinfile:
        path: /tmp/newfile
        line: "{{output.uid}}"
```
- As an output we will have following result
```
    "msg": "Register output is {u'group': u'cloud_user', u'uid': 1004, u'dest': u'/tmp/newfile', u'changed': True, 'failed': False, u'state': u'file',  u'gid': 1005, u'secontext': u'unconfined_u:object_r:user_tmp_t:s0', u'mode': u'0664', u'owner': u'cloud_user', u'diff': {u'after': {u'path': u'/tmp/ newfile', u'state': u'touch', u'atime': 1583240962.247869, u'mtime': 1583240962.247869}, u'before': {u'path': u'/tmp/newfile', u'state': u'file',  u'atime': 1583240712.9548037, u'mtime': 1583240712.9548037}}, u'size': 5}"
}
``` 
- By `register` we're registering output in defined variable. In our case this is **output** variable. We can use this variable during playbook run. 
  
###  Use Conditionals to Control Play Execution Part 1
  
![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img13.png)
  
Playbook with handler:
  
```
---
- hosts: labservers
  become: yes
  handlers:
    - name: restart apache
      service: name="httpd" state="restarted"
      listen: "restart web"
  tasks:
    - name: change config
      replace:
        path: /etc/httpd/conf/httpd.conf
        regexp: '^DocumentRoot.*$'
        replace: 'DocumentRoot "/opt/www"'
        backup: yes
      notify: "restart web"
```
  
Explanation for playbook:
- handlers waiting for notify message from tasks 
- once notify message appeared it's going to trigger handler in the end of play
- handler is not going to run again if there is no change made. 
- doesn't matter if we run playbook several times, handler will not be triggered (what is useful, to avoid downtime of the service)

### Use Conditionals to Control Play Execution Part 2
  
![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img14.png)

- **When** - if condition is true, it will execute. More similar to **if-else** condition 
- **With_items** - will take each item in a list and loop through it
- **With_files** - really similar to **With_items**
  
Demonstration of how to use a **loop** in playbooks:
```
---
- hosts: labservers
  become: yes
  tasks:
    - name: create users
      user:
        name: "{{item}}"
      with_items:
        - sam
        - john
        - bob
```
- Following playbook is going to run through `items` and create users **sam** **john** and **bob** listed in `with_items` block
  
Demonstration of how to use **when** condition in playbooks:
```
---
- hosts: labservers
  become: yes
  tasks:
    - name: edit index
      lineinfile:
        path: /var/www/html/index.html
        line: "I'm back!!!"
      when:
        - ansible_hostname == "innaghiyev1c"
```
- Condition is going to wait for proper hostname and apply your changes only on that node.   

### Configure Error Handling
- **Ignoring acceptable errors** - you're familiar with error and you accept it, you can configure to ignore such errors
- **Defining failure conditions** - define what to do with errors. Stop run or proceed with execute
- **Defining "Changed"** - control what it means that something needs to be changed
- **Blocks** - if some of task inside of block fails it will to another block. That logic  pre-configured already and it's going to switch to another block.

### Demo: Error Handling – Ignore Errors
Demonstration of playbook:
```
---
- hosts: labservers
  tasks:
    - name: get files
      get_url:
        url: "http://{{item}}/index.html"
        dest: "/tmp/{{item}}"
      ignore_errors: yes
      with_items:
        - innaghiyev1c
        - innaghiyev3c
        - innaghiyev2c
```

- We're going to `ignore errors` and even if playbook failed it's going to execute
- Output will look like this:

![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img15.png)

### Demo: Error Handling – Block Groups
Block groups and rescues - like a try and catch.
```
---
- hosts: labservers
  tasks:
    - name: get file
      block:
        - get_url:
            url: "http://innaghiyev3c/index.html"
            dest: "/tmp/index_file"
      rescue:
        - debug: msg="The file doesn't exists!"
      always:
        - debug: msg="Play done!"
```
  
- `rescue` - that part of block will run if playbook run failed
- `always` - that part of block will run any time. No matter playbook run fails or not. 
  
Here how rescue block is working:
![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img16.png)

### Selectively Run Specific Tasks In Playbooks Using Tags
How Ansible uses tags
- You can have several deployments in your playbook. Like database and application deployment
- By using tags we can deploy only application stage or only database stage
  
```
---
- hosts: web
  become: yes
  tasks:
  - name: deploy app binary
    copy:
      src: /home/cloud_user/apps/hello
      dest: /var/www/html/hello
    tags:
      - webdeploy
- hosts: db
  become: yes
  tasks:
  - name: deploy db script
    copy:
      src: /home/cloud_user/apps/script.sql
      dest: /opt/deb/scripts/script.sql
    tags:
      - dbdeploy
```

- `ansible-playbook tags_playbook.yml` - running playbook without tags
- `ansible-playbook tags_playbook.yml --tags webdeploy` - running playbook only for `webdeploy` part
- `ansible-playbook tags_playbook.yml --tags dbdeploy` - running playbook only for `dbdeploy` part
- `ansible-playbook tahs_playbook.yml --skip-tags webdeploy` - skip tag `webdeploy` and run the rest of playbook

### LAB: Ansible Playbooks: The Basics
#### Additional Information and Resources
Your company has been increasing the deployment of small broacher-style websites for clients. The head of IT has decided that each client should have their own web servers for better client isolation and has tasked you with creating concept automation to quickly deploy web-nodes with simple static website content.
  
You have been provided an ansible control node and 2 test lab servers (node1 and node2) that have been preconfigured with the ansible user and key.
  
You must create an ansible inventory in **/home/ansible/inventory** containing a host group named **web**. The web group should contain node1 and node2.
  
Furthermore, you must design an Ansible playbook that will execute the following tasks on your configured inventory: install **httpd**, start and enable the **httpd** service, and install a simple website provided on a repo server. Create the playbook in **/home/ansible/web.yml**. The simple website may be accessed from http://repo.example.com/website.tgz.
  
Summary tasks list:
  
1. Create an inventory in /home/ansible/inventory containing a host group named web. The web group should contain node1 and node2.
2. Create a playbook in /home/ansible/web.yml.
3. Configure the playbook to install httpd on the web group.
4. Configure the playbook to start and enable the httpd service on the web group.
5. Configure the playbook to retrieve the website from http://repo.example.com/website.tgz on each server in the web group.
6. Configure the playbook to unarchive the website into /var/www/html on all servers in the web group.
7. Execute the playbook you created using the inventory you created to verify your work.
  
Important notes:
- For your convenience, Ansible has been installed on the control node.
- The user **ansible** is present on all servers with appropriate shared keys for access to managed servers from the control node.
- The **ansible** user has the same password as **cloud_user**.
- **/etc/hosts** entries have been made on control1 for the managed servers.

#### Learning Objectives
##### Create an Inventory in `/home/ansible/inventory`. That Contains a Host Group Named `web`. The `web` Group Should Contain `node1` and `node2`
- `echo "[web]" >> /home/ansible/inventory`
- `echo "node1" >> /home/ansible/inventory`
- `echo "node2" >> /home/ansible/inventory`

##### Create a Playbook in `/home/ansible/web.yml`
- `echo "---" >> /home/ansible/web.yml`

##### Configure the Playbook to Install `httpd` on the `web` Group
  
Using a text editor, such as vim, edit **/home/ansible/web.yml** to contain the following text block below the line containing "---":
  
```
- hosts: web
  become: yes
  tasks:
    - name: install httpd
      yum: name=httpd state=latest
```

##### Configure the Playbook to Start and Enable the `httpd` Service on the `web` Group
  
Using a text editor such as vim, edit **/home/ansible/web.yml** to contain the following task block after the "install httpd task":
```
    - name: start and enable httpd
      service: name=httpd state=started enabled=yes
```

##### Configure the Playbook to Retrieve the Website from *http://repo.example.com/website.tgz* on Each Server in the `web` Group
  
Using a text editor such as vim, edit **/home/ansible/web.yml** to contain the following task block after the "start and enable httpd" task:
```
    - name: retrieve website from repo
      get_url: url=http://repo.example.com/website.tgz dest=/tmp/website.tgz
```

##### Configure the Playbook to Unarchive the Website into `/var/www/html` on All Servers in the `web` Group
  
Using a text editor such as vim, edit **/home/ansible/web.yml** to contain the following task block after the "retrieve website from repo" task:
```
    - name: install website
      unarchive: remote_src=yes src=/tmp/website.tgz dest=/var/www/html/
```

##### Verify the Work by Executing the Playbook Using the Inventory**
- `ansible-playbook -i /home/ansible/inventory /home/ansible/web.yml`
  

### LAB: Ansible Playbooks - Error Handling
#### Additional Information and Resources
We have to set up automation to pull down a data file, from a notoriously unreliable third-party system, for integration purposes. Create a playbook that attempts to pull down http://apps.l33t.com/transaction_list to `localhost`. The playbook should gracefully handle the site being down by outputting the message "l33t.com appears to be down. Try again later." to `stdout`. If the task succeeds, the playbook should write "File downloaded." to `stdout`. No matter if the playbook errors or not, it should always output "Attempt completed." to `stdout`.
  
If the report is collected, the playbook should write and edit the file to replace all occurrences of `#BLANKLINE` with a line break `\n`.
  
Tasks list summary:
- Create a playbook, `/home/ansible/report.yml`.
- Configure the playbook to download http://apps.l33t.com/- transaction_list to `/home/ansible/transaction_list` on `localhost` - and output "File downloaded." to `stdout`.
- Configure the playbook to handle connection failure by outputting - "l33t.com appears to be down. Try again later." to `stdout`.
- Configure the playbook to output "Attempt Completed" to `stdout`, - whether it was successful or not.
- Configure the playbook to replace all instances of `#BLANKLINE` with - the line break character `\n`.
- Run the playbook using the default inventory to verify whether things work or not.
  
Important notes:
- For convenience, Ansible has been installed on the control node.
- The user `ansible` already exists on all servers, with appropriate shared keys for access to the necessary servers from the control node.
- The `ansible` user has the same password as `cloud_user`.
- All necessary Ansible inventories have already been created.
- **apps.l337.com** is unavailable by default.
- We may force a state change by running `/home/ansible/scripts/change_l33t.sh`.

#### Learning Objectives
##### Create a playbook: `/home/ansible/report.yml`
- `echo "---" >> /home/ansible/report.yml`
##### Configure the Playbook to Download *http://apps.l33t.com/transaction_list* to `/home/ansible/transaction_list` on `localhost` and Outputs the Message "File downloaded." to `stdout`
  
Using a text editor, such as vim, edit `/home/ansible/report.yml` to contain the following text block below the line containing "---":
```
- hosts: localhost
  tasks:
    - name: download tranaction_list
      get_url:
        url: http://apps.l33t.com/transaction_list 
        dest: /home/ansible/transaction_list
    - debug: msg="File downloaded"
```

##### Configure the Playbook to Handle Connection Failure by Outputting "l33t.com appears to be down. Try again later." to `stdout`
  
Using a text editor, such as vim, edit the tasks section in `/home/ansible/report.yml` to contain the new lines as shown below. Note that the `get_url` line was changed to include a leading hyphen:
```
---
- hosts: localhost
  tasks:
    - name: download transction_list
      block:
        - get_url:
            url: http://apps.l33t.com/transaction_list
            dest: /home/ansible/transaction_list
        - debug: msg="File downloaded"
      rescue:
        - debug: msg="l33t.com appears to be down.  Try again later."
```

##### Configure the Playbook to Output "Attempt Completed" to `stdout`, Whether It Was Successful or Not
Using a text editor, such as vim, edit `/home/ansible/report.yml` to contain the following text block below the line containing "---":
  
```
---
- hosts: localhost
  tasks:
    - name: download transction_list
      block:
        - get_url:
            url: http://apps.l33t.com/transaction_list
            dest: /home/ansible/transaction_list
        - debug: msg="File downloaded"
      rescue:
        - debug: msg="l33t.com appears to be down.  Try again later."
      always:
        - debug: msg="Attempt completed."
```

##### Configure the Playbook to Replace All Instances of `#BLANKLINE` with the Line Break Character `\n`
  
Using a text editor, such as vim, edit `/home/ansible/report.yml` to contain the following text block below the line containing "---":
```
---
- hosts: localhost
  tasks:
    - name: download transction_list
      block:
        - get_url:
            url: http://apps.l33t.com/transaction_list
            dest: /home/ansible/transaction_list
        - replace: 
            path: /home/ansible/transaction_list 
            regexp: "#BLANKLINE"
            replace: '\n'
        - debug: msg="File downloaded"
      rescue:
        - debug: msg="l33t.com appears to be down.  Try again later."
      always:
        - debug: msg="Attempt completed."
```

##### Verify Configuration by Running the Playbook
- `ansible-playbook /home/ansible/report.yml`
  
  
## Create and Use Templates to Create Customized Configuration Files
### Using Ansible Templates Lecture
This lecture covers how templates are used, why they are used, and how they are created. A successful Ansible Specialist must have an understanding of these concepts.
  
Overview:
- Template basics
- Template module 
- Template file 
  
Template basics
- Template give the ability to provide a skeletal file that can be dynamically completed using variables 
- The most common template use case is configuration file management
- Templates are generally used by providing a template file on the ansible control node, and then using the template module within your playbook to deploy the file to a target server or group
- Templates are processed using the Jinja2 template language
  
Template Module
  
![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img17.png)
  
Template File
  
![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img18.png)


  
### Demo: Using Ansible Templates
  
Our template `network.j2` file will look like this:
```
My IP address is {{ ansible_default_ipv4.address }}.

{{ ansible_distribution }} is my OS version.
```

- `ansible_default_ipv4.address` and `ansible_distribution` - are gathered facts during playbook run 
  
Playbook for calling our template will look like this:
```
---
- hosts: labservers
  tasks:
  - name: deploy local net file
    template:
      src: /home/cloud_user/template/network.j2
      dest: /home/cloud_user/template/network.txt
```
  
Created file `/home/cloud_user/template/network.txt` after playbook run will be:
```
My IP address is 142.21.46.232.

RedHat is my OS version.
```
  


## Work with Ansible Variables and Facts
### Ansible Variables Lecture
This lecture broadly covers how to work with Ansible variables. Variable conventions, dictionary variables, magic variables and jinja2 filters are all covered conceptually as well as syntactically.
    
Updated Link https://jinja.palletsprojects.com/en/2.10.x/templates/
  
Overview:
  - Ansible variables
  - Dictionary variables
  - Magic variables and filters
  - What are facts?
  - How to use facts? 
  - Facts.d - custom facts

- Ansible variables
  - Review on naming convention and quotes
  - Some more places to define variables:
    - vars, vars_files and vars_prompt
    - Command line: ansible-playbook play.yml -e '{"myVar":"myValue","anotherVar":"anotherValue"}'
    - Roles, blocks, and inventories
  - Essential variable use:
    - -debug: msg="Look! I'm using my variable {{myVar}}!"
  - A note on quotes:
    - name: "{{package}}"
  
- Dictionary variables

![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img19.png)
  
- Magic Variables and Filters
  
![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img20.png)
  
### Demo: Ansible Variables - Magic Variables and Jinja Filters
  
Cookbook with variables usage:
```
---
- hosts: labservers
  vars:
    inv_file: /home/cloud_user/vars/inv.txt
  tasks:
  - name: create file
    file:
      path: "{{inv_file}}"
      state: touch
  - name: generate inventory
    lineinfile:
      path: "{{inv_file}}"
      line: "{{ groups['labservers']|join(' ') }}"
```

- `inv_file` - defined variable before task started
- `groups['labservers']` - magic variable with `labservers` host group in default inventory
- `|join(' ')` - join our hostnames with space between them.
  
Content of the file after playbook run:
```
[cloud_user@innaghiyev2c playbook]$ cat ../vars/inv.txt 
innaghiyev1c.mylabserver.com innaghiyev2c.mylabserver.com innaghiyev3c.mylabserver.com
```

### Demo: Ansible Variables - Variable Files
  
Possible ways to define variable files:
- `var_files` - using it within the playbook to define variables file  
- `ansible-playbook var_files_playbook.yml -e "@../vars/users.lst"` - using `-e` key to provide variable file path.
  
Here how `users.lst` file looks like:
```
[cloud_user@innaghiyev2c playbook]$ cat ../vars/users.lst
staff:
  - joe
  - john
  - bob
  - sam
  - mark
faculty:
  - matt
  - alex
  - frank
other:
  - will
  - jack
```

Cookbook with variable file usage:
```
---
- hosts: labservers
  vars:
    userFile: /home/cloud_user/vars/list
  tasks:
  - name: create file #going to create file with defined path
    file:
      state: touch
      path: "{{ userFile }}"
  - name: list users #add inside of file users name looping through items
    lineinfile:
      path: "{{ userFile }}"
      line: "{{ item }}"
    with_items:
      - "{{ staff }}"
      - "{{ faculty }}"
      - "{{ other }}"
```

### Ansible Facts Lecture
What are facts? 
- Facts are information discovered by Ansible about a target system
- There are two ways facts are collected:
  - Using the setup module with an ad-hoc command: `ansible all -m setup`
  - Facts are gathered by default when a playbook is executed 
- Fact gathering in playbooks may be disabled using the **gather_facts** attribute
  
How to use facts
  
![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img21.png)
  

Facts.d - custome facts
  
![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img22.png)
    
  
### Demo: Working with Ansible Facts
- `ansible labservers -m setup | less` - gather facts for labservers host group
- `ansible labservers -m setup --limit innaghiyev2c.mylabserver.com -a "filter=*ip*"` - gathering facts with used **filter**
- `ansible labservers -m setup --limit innaghiyev2c.mylabserver.com -a "filter=*dist*"` 
```
innaghiyev2c.mylabserver.com | SUCCESS => {
    "ansible_facts": {
        "ansible_distribution": "RedHat", 
        "ansible_distribution_file_parsed": true, 
        "ansible_distribution_file_path": "/etc/redhat-release", 
        "ansible_distribution_file_search_string": "Red Hat", 
        "ansible_distribution_file_variety": "RedHat", 
        "ansible_distribution_major_version": "7", 
        "ansible_distribution_release": "Maipo", 
        "ansible_distribution_version": "7.7", 
        "discovered_interpreter_python": "/usr/bin/python"
    }, 
    "changed": false
}
```
  

Custom facts set up:
-  `sudo mkdir -p /etc/ansible/facts.d` - create `facts.d` directory
- `sudo vim /etc/ansible/facts.d/prefs.fact` - create custom fact with `.fact` extension
```
[cloud_user@innaghiyev2c playbook]$ sudo cat /etc/ansible/facts.d/prefs.fact
[location]
type=physical
datacenter=Alexandrea
```

- `ansible labservers --limit innaghiyev2c.mylabserver.com -m setup -a "filter=ansible_local"` - if we call **ansible_local** facts. Output gonna be like that
```
innaghiyev2c.mylabserver.com | SUCCESS => {
    "ansible_facts": {
        "ansible_local": {
            "prefs": {
                "location": {
                    "datacenter": "Alexandrea", 
                    "type": "physical"
                }
            }
        }, 
        "discovered_interpreter_python": "/usr/bin/python"
    }, 
    "changed": false
}
```
  

### LAB: Working with Ansible Templates, Variables, and Facts
#### Additional Information and Resources
A colleague of yours was the unfortunate victim of a scam email, and their network account was compromised. Shortly after you finished helping them pack up their desk, your boss gave you the assignment to promote system security through deploying a hardened **sudoers** file. You will need to create an Ansible template of the **sudoers** file that meets the following criteria:
- A file named **/etc/sudoers.d/hardened** to deploy on all ansible inventory servers. WARNING: Do NOT edit the default **sudoers** file, doing so may break your exercise environment. Additionally, always validate any file placed in **/etc/sudoers.d** with `/sbin/visudo -cf <filename>` prior to deployment!!
- Grant users in the **sysops** group the ability to run all commands as **root** for each local system by IP address. This would be what the entry in your result - file except with the target system's IP: `%sysops 34.124.22.55 = (ALL) ALL`.
- Define the **host_alias** group **WEBSERVERS** to contain all servers in the **ansible web inventory** group: `Host_Alias WEBSERVERS = <host name>`
- Define the **host_alias** group **DBSERVERS** to contain all servers in the ansible database inventory group: `Host_Alias DBSERVERS = <host name>`
- Grant users in the **httpd** group the ability to `sudo su - webuser` on the **WEBSERVERS** hosts: `%httpd WEBSERVERS = /bin/su - webuser`
- Grant users in the dba group sudo su - dbuser on the DBSERVERS hosts: `%dba DBSERVERS = /bin/su - dbuser`
- The file must be validated using `/sbin/visudo -cf` before deployment.
  
You will need to create an accompanying playbook in `/home/ansible/security.yml` that will deploy this template to all servers in the default inventory.
  
Summary tasks list:
- Create a template **sudoers** file in */home/ansible/hardened.j2 *that produces a file with appropriate output for each host.
- The deployed file should resemble the following, except with the **IP** and **hostnames** customized appropriately:
```
  %sysops 34.124.22.55 = (ALL) ALL
  Host_Alias WEBSERVERS = server1, server2
  Host_Alias DBSERVERS = serverA, serverB
  %httpd WEBSERVERS = /bin/su - webuser
  %dba DBSERVERS = /bin/su - dbuser
```
  
- Create a playbook in **/home/ansible/security.yml** that uses the template module to deploy the template on all servers in the default ansible inventory after validating the syntax of the generated file.
  - Note: You may find it easier to have the play output to **/home/ansible/test** and validate manually using `/sbin/visudo -cf <filename>` before using the template module's validate.
  - IMPORTANT: Do not deploy any file to `/etc/sudoers.d/ `without first validating with visudo! A syntax error in a `sudoers` file will break sudo on the system and require starting the exercise over again!
  - Note: The video shows the use of join(' ') which is a typo. To support multiple hosts in the sudoers file it should instead be join(', ')
- Run the playbook and ensure the files deployed correctly.

#### Learning Objectives
##### Create a Template *sudoers* File in `/home/ansible/hardened.j2` That Produces a File with Appropriate Output for Each Host
- `touch /home/ansible/hardened.j2`
  
##### The Deployed File Should Resemble the Example File Except with the *IP* and *hostnames* Customized Appropriately
- Edit **hardened.j2** to contain the following text:
```
    %sysops {{ ansible_default_ipv4.address }} = (ALL) ALL
    Host_Alias WEBSERVERS = {{ groups['web']|join(', ') }}
    Host_Alias DBSERVERS = {{ groups['database']|join(', ') }} 
    %httpd WEBSERVERS = /bin/su - webuser
    %dba DBSERVERS = /bin/su - dbuser
```
  
##### Create a Playbook in `/home/ansible/security.yml` That Uses the Template Module to Deploy the Template on All Servers in the Default Ansible Inventory After Validating the Syntax of the Generated File
- Edit **/home/ansible/security.yml** to contain the following:
```
---
- hosts: all
  become: yes
  tasks:
  - name: deploy sudo template
    template:
      src: /home/ansible/hardened.j2
      dest: /etc/sudoers.d/hardened
      validate: /sbin/visudo -cf %s
```
  
##### Run the Playbook and Ensure the Files Are Correctly Deployed
- `ansible-playbook /home/ansible/security.yml`
  
Check the local **/etc/sudoers.d/hardened** on the **ansible control** node for the correct contents.
  
  
## Create and Work with Roles
### Working with Ansible Roles Lecture
  
![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img23.png)
  

![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img24.png)

- **Tasks** - the tasks directory contains the main list of tasks to be executed by the role.
  - This directory must include a **main.yml** if that directroy is being used. You can think of main.yml as the entry point for the tasks section of the role. 

- **Vars** - the vars directory contains variables used within the role
  - The vars directory is entered via a main.yml
  - The vars directory is one of three primary ways to interact with variables within a role (aside from convetional variable use such as inventory). The other two ways are using the defautls directory and passing parameters to the role
  - The vars directory has the highest level of precedence. It will override inventory variables as well
  - The vars directory may only be overridded by variablers passed via CLI. 

- The **defaults** - directory that contains default variables for the role 
  - The defaults directory is entered via a main.yml
  - The default directory is one of three primary was to interact with vairables within a role (aside from conventional variables use such as inventory). The other two ways are using the directory ans passing parameters to the role.
  - The defaults directory has the lowest level of precedence. 
  - The defaults directory is only meant to provide a value to a variable if no other value is given.

Best practice dictates that you properly namespace your variables when working with a role to avoid conflicts. 

- The **handlers** directory contains handlers, which may be used by this role or even anywhere outside this role
  - The directory is entered via a main.yml within the directory

- More on **handlers**:
  - Handlers are essentially tasks that my be flagged to run using the **notify** keyword
  - The notify keyword will only flag the handler if a task block makes changes
  - A handler will only be triggered once even if they are notified by multiple tasks

- The **files** directory contains files which can be deployyed vis this role
  - Files within this directory may be referenced without path throughout the role.
  - Note this directory is for ordinary files (not var fies or templates)

- The **templates** directory contains templates which can be deployed via this role
  - Templates within this directory may be referenced without a path throughout the role. 
  

### Demo: Creating and Applying a Role in Ansible
In this terminal-side demonstration, a new role is created and then applied to a target host.
  
- `ansible-galaxy role init apache` - create an **apache** role with default structure by using *ansible-galaxy*
```
[cloud_user@innaghiyev2c ~]$ ll /etc/ansible/roles/apache/
total 4
drwxrwxr-x. 2 cloud_user cloud_user   21 Mar  9 08:27 defaults
drwxrwxr-x. 2 cloud_user cloud_user    6 Mar  9 08:27 files
drwxrwxr-x. 2 cloud_user cloud_user   21 Mar  9 08:27 handlers
drwxrwxr-x. 2 cloud_user cloud_user   21 Mar  9 08:27 meta
-rw-rw-r--. 1 cloud_user cloud_user 1328 Mar  9 08:27 README.md
drwxrwxr-x. 2 cloud_user cloud_user   21 Mar  9 08:27 tasks
drwxrwxr-x. 2 cloud_user cloud_user    6 Mar  9 08:27 templates
drwxrwxr-x. 2 cloud_user cloud_user   37 Mar  9 08:27 tests
drwxrwxr-x. 2 cloud_user cloud_user   21 Mar  9 08:27 vars
```
  
- `vim /etc/ansible/roles/tasks/main.yml` - we're going to start from `tasks`
```
---
# tasks file for apache
- name: install apache
  yum: name=httpd state=latest

- name: copy httpd.conf template
  template:
    src: httpd.conf.j2
    dest: /etc/httpd/conf/httpd.conf
  notify: restart httpd

- name: enable and start service
  service:
    name: httpd
    enabled: yes
    state: started
```
  
- `ls -l /etc/ansible/roles/apache/templates` - our templates for apache role stored in **templates** directory, no need to define full path for it
```
[cloud_user@innaghiyev2c templates]$ ls -l
total 12
-rw-r--r--. 1 root root 11765 Mar  9 08:47 httpd.conf.j2
```
  
- `vim /etc/ansible/roles/apache/defaults/main.yml` - we're going to setup default attributes.
```
---
# defaults file for apache
apache_server_admin: admin@example.com
```
  
- `/etc/ansible/roles/apache/handlers/main.yml` - configuring handler 
```
---
# handlers file for apache

- name: restart apache service
  service: name=httpd state=restarted
  listen: "restart httpd"
```
  
- `/etc/ansible/roles/install.yml` - configure playbook to use **apache** role
```
---
- hosts: labservers
  become: yes
  roles:
    - apache
```

- `ansible-playbook install.yml` - finally run your playbook and check for results.
```
PLAY RECAP **********************************************************************************************************************************************************
innaghiyev1c.mylabserver.com : ok=5    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
innaghiyev2c.mylabserver.com : ok=5    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
innaghiyev3c.mylabserver.com : ok=5    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

- `vim /etc/ansible/roles/install.yml` - let's change our default variable for **apache_server_admin**
```
---
- hosts: labservers
  become: yes
  roles:
    - apache
  vars:
    apache_server_admin: beson@example.com
```

- `vim -R /etc/httpd/conf/httpd.conf` - as we can see new **ServerAdmin** value has been updated
```
# ServerAdmin: Your address, where problems with the server should be
# e-mailed.  This address appears on some server-generated pages, such
# as error documents.  e.g. admin@your-domain.com
#
ServerAdmin beson@example.com
```
  

### Applying In-Line Roles and Role Dependencies
Working with roles is further covered in a discussion on static vs dynamic roles followed by a lecture on how to create and work with role dependencies in Ansible. This lesson concludes with a demonstration of creating a new role that is dependent on another role.
  
We can put some conditions and tags to involve a roles inside of playbook:
```
---
- hosts: webservers
  tasks:
  - include_role:
      name: apache
    tags:
    - RH_HTTPD
    when "ansible_os_family == 'RedHat'"
```
  
You can configure roles to use **dependencies**:
```
---
dependencies:
  - role: common
    vars:
      some_parameter: 3
  - role: apache
    vars:
      apache_port: 80    
```
  
- **Meta** directory:
  - The meta-directory defines certain meta data for the role.
  - Relevant meta data includes role dependecies and vairous role level configurations such as *allow_duplicates*.

   The meta-directroy is entered via a *main.yml*

- **Nesting**:
  - Roles my include other roles using the dependecies keyword.
  - Dependent roles are applied prior to the role dependent on them
  - A role using the same parameters will not be applied more than one time. This can cause complication with role dependencies
  - Having `allow_duplicates: true` defined in **meta/main.yml** within a role will allow the role to be applied more than once. 
  
  
- `ansible-galaxy init php-webserver` - let's generate **php-webserver** role. That roles is going to use **apache** role as a dependency role.
- `sudo vim /etc/ansible/roles/php-webserver/tasks/main.yml` - write tasks for a php-webserver role
```
---
# tasks file for php-webserver

- name: install php
  yum: name= {{ item }} state=latest
  with_items:
    - php
    - php-gd
    - php-pear
    - php-mysql
  notify: restart httpd
```

- `sudo vim /etc/ansible/roles/php-webserver/meta/main.yml` - configure dependency from **meta** directory. We only need **dependencies** block here
```
dependencies:
  # List your role dependencies here, one per line. Be sure to remove the '[]' above,
  # if you add dependencies to this list.
  - role: apache
```

- `sudo vim /etc/ansible/roles/install.yml` - our cookbook will look like this
```
---
- hosts: labservers
  become: yes
  roles:
    - php-webserver
```
  
From output it can be seen that dependency **apache** role run **first** and then our **php-webserver** role.  
```
PLAY [labservers] ********************************************************************************************************************************************
TASK [Gathering Facts] ********************************************************************************************************************************************
ok: [innaghiyev2c.mylabserver.com]

TASK [apache : install apache] ********************************************************************************************************************************************
ok: [innaghiyev2c.mylabserver.com]

TASK [apache : copy httpd.conf template] ***********************************************************************************************************************************
ok: [innaghiyev2c.mylabserver.com]

TASK [apache : enable and start service] ***********************************************************************************************************************************
ok: [innaghiyev2c.mylabserver.com]

TASK [php-webserver : install php] ***********************************************************************************************************************************
ok: [innaghiyev2c.mylabserver.com] => (item=php)
ok: [innaghiyev2c.mylabserver.com] => (item=php-gd)
ok: [innaghiyev2c.mylabserver.com] => (item=php-pear)
ok: [innaghiyev2c.mylabserver.com] => (item=php-mysql)

PLAY RECAP ************************************************************************************************************************
innaghiyev2c.mylabserver.com : ok=5    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```
  

### LAB: Working with Ansible Roles
#### Additional Information and Resources
You have just started a new job as the operations lead at a small company. There is currently no formal server baseline, and it makes for a mixed configuration environment that is consuming more support and maintenance than it should. You have decided to create a baseline process using Ansible by creating a baseline role. You have noted the following commonalities that should be included in the baseline role:
- Set **/etc/motd** based on a template.
- Install the latest Nagios client.
- Add the Nagios server to **/etc/hosts**.
- Create a **noc** user.
- Import the **noc** user's public key (copy authorized keys to **/home/noc/.ssh/authorized_keys**).
    
The role should be called *"baseline"* and should reside in **/etc/ansible/roles** on the **ansible control** node.
  
You will test your role on some newly requested webservers. A playbook called **web.yml** has been provided for you and deploys httpd to all servers in the web group (defined in your default inventory). You will need to edit the playbook to deploy the **baseline** role to the servers in the **web** group as well.
  
You will find the **motd** template, Nagios server IP information, the **noc** user's public key, and the **web.yml** playbook in **/home/ansible/resources** on the **ansible control** node.
  
Summary tasks list:
- Create the necessary directories and files for the **baseline** role.
- Configure the role to deploy the **/etc/motd** template.
- Configure the role to install the latest Nagios client.
- Configure the role to add an entry to **/etc/hosts** for the Nagios server.
- Configure the role to create the **noc** user and deploy the provided public key for the **noc** user on target systems (copy **authorized_keys** to **/home/noc/.ssh authorized_keys** with the **owner** and **group owner** set as **noc** and the mode as **0600**).
- Edit **web.yml** to deploy the **baseline** role in addition to what it already does.
- Verify that your role works by deploying **web.yml** with Ansible.
  
Important notes:
- For your convenience, Ansible is already installed on the control node.
- The user **ansible** is on all servers with the appropriate shared keys for access to necessary servers from the control node.
- The **ansible** user has sudo access with no password. It uses the same password as **cloud_user**.
- All the necessary Ansible inventories have been created for you.

#### Learning Objectives
##### Create a Role Called baseline in /etc/ansible/roles
Run the following commands to create the structure needed for the role:
- `sudo mkdir /etc/ansible/roles/baseline && sudo chown ansible.ansible /etc/ansible/roles/baseline`
- `mkdir /etc/ansible/roles/baseline/{templates,tasks,files}`
- `echo "---" > /etc/ansible/roles/baseline/tasks/main.yml`
  
##### Configure the Role to Deploy the /etc/motd Template
- `cp /home/ansible/resources/motd.j2 /etc/ansible/roles/baseline/templates`
- Create a file called `/etc/ansible/roles/baseline/tasks/deploy_motd.yml` with the following content:
```
---
- template:
    src: motd.j2
    dest: /etc/motd
```
  
- Edit `/etc/ansible/roles/baseline/tasks/main.yml` to include the following lines at the bottom of the file:
```
- name: configure motd
  import_tasks: deploy_motd.yml
```
  
##### Configure the Role to Install the Latest Nagios Client
- Create a file called `/etc/ansible/roles/baseline/tasks/deploy_nagios.yml` with the following content:
```
---
- yum: name=nrpe state=latest
```
  
- Edit `/etc/ansible/roles/baseline/tasks/main.yml` to include the following lines at the bottom of the file (take care with the formatting.):
```
- name: deploy nagios client
  import_tasks: deploy_nagios.yml
```

##### Configure the Role to Add an Entry to /etc/hosts for the Nagios Server
- Create a file called `/etc/ansible/roles/baseline/tasks/edit_hosts.yml` with the following content, substituting <PROVIDED> with the IP specified in `/home/ansible/resources/nagios_info.txt`:
```
---
- lineinfile:
    line: "<<PROVIDED>PROVIDED> nagios.example.com"
    path: /etc/hosts
```
  
- Edit `/etc/ansible/roles/baseline/tasks/main.yml` to include the following lines at the bottom of the file:
```
  - name: edit hosts file
    import_tasks: edit_hosts.yml
```

##### Configure the Role to Create the noc User and Deploy the Provided Public Key for the noc User on Target Systems
- Copy the file `/home/ansible/resources/authorized_keys*` to `*/etc/ansible/roles/baseline/files/`.

- Create a file called `/etc/ansible/roles/baseline/tasks/deploy_noc_user.yml` with the following content:
```
---
- user: name=noc
- file:
     state: directory
     path: /home/noc/.ssh
     mode: 0600
     owner: noc
     group: noc
- copy:
        src: authorized_keys
        dest: /home/noc/.ssh/authorized_keys
        mode: 0644
        owner: noc
        group: noc
```

- Edit `/etc/ansible/roles/baseline/tasks/main.yml` to include the following lines at the bottom of the file:
```
      - name: set up noc user and key
        import_tasks: deploy_noc_user.yml
```

##### Edit web.yml to Deploy the baseline Role
Edit `/home/ansible/resources/web.yml` to the following:
```
---
- hosts: webservers
  become: yes
  roles:
    - baseline
  tasks:
    - name: install httpd
      yum: name=httpd state=latest
    - name: start and enable httpd
      service: name=httpd state=started enabled=yes
```
  
##### Run Your Playbook Using the Default Inventory
Run ansible-playbook `/home/ansible/resources/web.yml`.
  
  
## Download roles from an Ansible Galaxy
### Download Roles from Ansible Galaxy
Ansible Galaxy - galaxy.ansible.com or github.com:
  - Essentially a large public repository of Ansible roles. 
  - Role ship with readmes detailining role use and available variables.
  - Galaxy contains a large number of roles that are constantly evolving and increasing.
  - Galaxy can use git allowing for other role sources such as GitHub
  
- Ansible ships with the ansible-galaxy command which may be used to install roles form Galaxy among other useful role management features.
- `ansible-galaxy` can also create new empty roles in your working directory like so:
  - `ansible-galaxy init <role_name>`
- Using `ansible-galaxy install <username.role>`, you can download roels from **galaxy.ansible.com**
- Roles installed in the roles_path may be listed using `ansible-galaxy list`
- Remove, search, and loging are other useful subcommands. 
- The **-p** flag allows specification of local role location (`ansible-galaxy` uses `/etc/ansible/roles` by default)
  
- `ansible-galaxy init mysql` - initiate mysql named role with required structure inside
```
[cloud_user@innaghiyev2c ~]$ ansible-galaxy init mysql
- Role mysql was created successfully
[cloud_user@innaghiyev2c ~]$ ll mysql/
total 4
drwxrwxr-x. 2 cloud_user cloud_user   21 Mar 10 09:29 defaults
drwxrwxr-x. 2 cloud_user cloud_user    6 Mar 10 09:29 files
drwxrwxr-x. 2 cloud_user cloud_user   21 Mar 10 09:29 handlers
drwxrwxr-x. 2 cloud_user cloud_user   21 Mar 10 09:29 meta
-rw-rw-r--. 1 cloud_user cloud_user 1328 Mar 10 09:29 README.md
drwxrwxr-x. 2 cloud_user cloud_user   21 Mar 10 09:29 tasks
drwxrwxr-x. 2 cloud_user cloud_user    6 Mar 10 09:29 templates
drwxrwxr-x. 2 cloud_user cloud_user   37 Mar 10 09:29 tests
drwxrwxr-x. 2 cloud_user cloud_user   21 Mar 10 09:29 vars
```

- `ansible-galaxy search elasticsearch` - search for an **elasticsearch** role on ansible-galaxy
```
Found 487 roles matching your search:

 Name                                                  Description
 ----                                                  -----------
 0x0i.elasticsearch                                    Elasticsearch, a real-time distributed search and analytics engine
 0x0i.grafana                                          Grafana - an analytics and monitoring observability platform
 0x0i.kibana                                           Kibana, an analytics and visualization platform designed to operate with Elasticsearch
 1it.sudo                                              Ansible role for managing sudoers
 aaronpederson.fluentd                                 Really simple management of data collection from logs or scripts. Installation from gem.
 abelboldu.elasticsearch                               Elasticsearch for Linux.
 abelboldu.logstash                                    Logstash for Linux.
 abraverm.kibana-management                            Kibana objects (dashboard, visualization) management
 adamaod.Single-Instance-ELK                           Single Instance Elk Stack
 AerisCloud.collectd                                   This role takes care of adding collectd to any given server
 AerisCloud.elasticsearch                              Installs ElasticSearch
 AerisCloud.librato                                    Install and configure the Librato Agent
 AerisCloud.logstash                                   This role is used to add log aggregation and forwarding capability to a given server
 AerisCloud.repos                                      Manage CentOS yum and Debian apt repositories
```

- `ansible-galaxy install elastic.elasticsearch` - install elasticsearch role from ansible-galaxy

- let's create simple playbook which will install role for us:
```
---
- hosts: localhost
  become: yes
  tasks:
    - name: install role
      command: ansible-galaxy install elastic.elasticsearch
```

- `sudo ansible-galaxy remove elastic.elasticsearch` - remove installed role
  

## Managing Parallelism
### Parallelism in Ansible
This lecture covers how to configure Ansible for higher performance using Ansible Forks. There is also a demonstration on how to use the serial keyword to batch host operations.
  
- It's posssible to control the number of hosts acted upon at once time by Ansible
- The Ansible process will create forks to execute actions in parallel.
- By default, the process will only for 5 times
- The number of forks can be set for a single command using **-f** flag with either the ansible or ansible-playbook commands.
- The default may be changed in **ansible.cfg**
- The serial keyword may also confine the number of simultaneous updates within a playbook
  
For number: 
  - best practice recommends do not increase it more than 50
  - 5 is pretty small number 
  - you can increase your fork number up to 10 or 15 without risk

- `serial` - used to speficy on how many hosts playbook will be executed simultaneously
```
---
- hosts: labservers
  become: yes
  serial:
    - 1   #run on one hosts
    - 2   #run on two hosts
    - 50% #run on 50% of hosts
  tasks:
  - name: add host entry
    lineinfile:
      path: /etc/hosts
      line: "webserver mywebserver.labs.com"
```
  
- From run it can be seen that playbook first run on **one** host, then **two** and finally the rest
```
[cloud_user@innaghiyev2c ~]$ ansible-playbook serial.yml 

PLAY [labservers] **********************************************************************************************************************************************************

TASK [Gathering Facts] *****************************************************************************************************************************************************
ok: [innaghiyev1c.mylabserver.com]

TASK [add host entry] ******************************************************************************************************************************************************
changed: [innaghiyev1c.mylabserver.com]

PLAY [labservers] **********************************************************************************************************************************************************

TASK [Gathering Facts] *****************************************************************************************************************************************************
ok: [innaghiyev2c.mylabserver.com]
ok: [innaghiyev3c.mylabserver.com]

TASK [add host entry] ******************************************************************************************************************************************************
changed: [innaghiyev2c.mylabserver.com]
changed: [innaghiyev3c.mylabserver.com]

PLAY RECAP *****************************************************************************************************************************************************************
innaghiyev1c.mylabserver.com : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
innaghiyev2c.mylabserver.com : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
innaghiyev3c.mylabserver.com : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

- `max_fail_percentage: 30` - we can use this key to provide percentage of failure during cookbook run. If 1/3 of our cookbook run will fail, then whole playbook gonna stop and concidered as **failed**
  
  
## Use Ansible Vault in Playbooks to Protect Sensitive Data
### The Ansible-Vault Command
- The `ansible-vault` command allows file encryption, and requires a password to unencrypt
- Command: `ansible-vault encrypt <file>`
- The ansible-vault rekey command will allow you to re-encrypt a file and reset the password.
- To supply the vault password during play execution, you must use either of the `--ask-vault-password` or `--ask-vault-file` flags.
- Ansible 2.4 introduces the `--vault-id` feature.
- It is also possible to set `no_log` within a module to censor sensitive log output

- `vault-id` feature
  - going to replace `--ask-vault-password` or `--ask-vault-file` flags
  - before you can only specify one password for whole vault
  - `vault-id` provides a possibility to set several passwords for a single play. 
  - `vault-id` will go through each password stored in `vault` for encypted file to find proper one.
  - it's possible to set up `label` for `vault-id`
  
As a demonstration let's create simple text file:
- `echo "Super secret word stored here" > secret.txt`
- `ansible-vault encrypt secret.txt` - simply encrypt our file
```
[cloud_user@innaghiyev2c ~]$ ansible-vault encrypt secret.txt
New Vault password: <your vault password here>
Confirm New Vault password: <confirm your vault password here> 
Encryption successful 
```
  
- `[cloud_user@innaghiyev2c ~]$ cat secret.txt` - as an output we have this now
```
$ANSIBLE_VAULT;1.1;AES256
38643439333433636239326461326234386361306331366666636534623065343237393662363538
3635633736663639663162326166636561666639653930650a303762393030663230386438393361
64336461643063383564306230313037363166623735386164363964323265366332626138663266
3638643239626366660a613162316565303936396437393133336631346166636538336533653637
31396364666430653163306164336535333562343464376438663361663436643765
```

- `ansible-vault edit secret.txt` - if you want to edit encrypted file
- `ansible-vault decrypt secret.txt` - decrypt your file
- `ansible-vault encrypt_string 'The answer is 42' -n meaning` - you can encrypt pieces of your playbook, rather all files
- `ansible-vault encrypt_string 'The answer is 42' -n meaning --vault-id dev@prompt` - provide vault-id with a label `dev`
```
[cloud_user@innaghiyev2c ~]$ ansible-vault encrypt_string 'The answer is 42' -n meaning --vault-id dev@prompt
New vault password (dev): 
Confirm new vault password (dev): 
meaning: !vault |
          $ANSIBLE_VAULT;1.2;AES256;dev
          36333866373732363065613065643062383936656461626235326238643162303863343465373166
          6431633033383432396638383463636636666364386165370a326337653336613564623363633362
          31666264646662633365333237366631343130316136353939386131396432393233383732356261
          6133353264626234630a353233366234343564653737383637633565623364633466343565623435
          37393137383861373631636135616265613166323361356266353836626265356135
Encryption successful
```

### Using Vaults in Playbooks
- We have following a playbook for testing:
```
---
- hosts: localhost
  vars_files:
    - /home/cloud_user/secure
  tasks:
  - name: Output message
    shell: echo {{ message }} > /home/cloud_user/deployed.txt
```
  
- let's create simple file with `password` word inside:
```
[cloud_user@innaghiyev2c ~]$ cat vault
password
```

- `ansible-vault encrypt --vault-id prod@vault secure` - encrypt `secure` file by labeling it as a `prod` and using file `vault` we recently created
```
[cloud_user@innaghiyev2c ~]$ ansible-vault encrypt --vault-id prod@vault secure
Encryption successful
```

- `secure` file looks like that now:
```
[cloud_user@innaghiyev2c ~]$ cat secure 
$ANSIBLE_VAULT;1.2;AES256;prod
64366564623135316434353863666465646330626435613865363839626565353738363861336134
6234353734313535623764393439666463613831356434310a336365663839393465333535313061
64303464336666343739373736653162333866663733393930646366643031326239616538316665
3963616365336631610a623566666265306432316435303032383435336165613432343761353165
66336333366632353166643638663865366231356430333034663135343266633636
```

- Let's try to run our `vault.yml` playbook
```
[cloud_user@innaghiyev2c ~]$ ansible-playbook vault.yml 
ERROR! Attempting to decrypt but no vault secrets found
```

- Same command, but with `vault-id` providing.
```
[cloud_user@innaghiyev2c ~]$ ansible-playbook vault.yml --vault-id prod@vault
```

- If we run playbook with `-v` - verbose key. We will see content of the encrypted file
```
changed: [localhost] => {"changed": true, "cmd": "echo I am a walrus"
```

- That can be prevented by using simple `no_log: True` string. 
```
---
- hosts: localhost
  vars_files:
    - /home/cloud_user/secure
  tasks:
  - name: Output message
    shell: echo {{ message }} > /home/cloud_user/deployed.txt
    no_log: true
```

- Now output of the playbook will look like that:
```
TASK [Output message] **********************************************************************************
changed: [localhost] => {"censored": "the output has been hidden due to the fact that 'no_log: true' was specified for this result", "changed": true}
```
  

### LAB: Working with Confidential Data in Ansible
#### Additional Information and Resources
In an effort to improve security, you have been tasked with securing an Ansible variable file. The variable file is to be used in an ansible job that creates a secure website. To do this, complete the following:
  
1. Encrypt the file **/home/ansible/secret using ansible-vault**.
2. Then configure a vault password file named **/home/ansible/vault** to be used to run the Ansible playbook **/home/ansible/secPage.yml** successfully with the encrypted secrets file.
3. Verify your work by running the **secPage.yml** playbook using **ansible-playbook** and specifying your vault password file.
4. Test that the site deployed correctly by trying to access http://node1/secure/classified.html using the user **bond** with the password **james**.
  
Summary tasks list:
- Encrypt **/home/ansible/secret** using the `ansible-vault` command.
- Create **/home/ansible/vault** as a vault password file that may be used to access the encrypted secret file without prompt.
- Run the playbook **/home/ansible/secPage.yml** using your vault password file to validate your work.
- Verify that the secure page deployed correctly by attempting to access http://node1/secure/classified.html as the user **bond** with the password **james**.

#### Learning Objectives
##### Encrypt `/home/ansible/secret` using the `ansible-vault` command.
- Run `ansible-vault encrypt /home/ansible/secret` and provide a simple password of your choosing.
- Be sure to remember the password!
##### Create */home/ansible/vault* as a vault password file that may be used to access the encrypted secret file without prompt.
- Run the command `echo "<Your_Vault_Password>" > /home/ansible/vault`.
- Substitute <<Your_Vault_Password>Your_Vault_Password> with the password you chose in the previous task.
##### Run the playbook */home/ansible/secPage.yml* using your *vault* password file to validate your work.
- Run the command `ansible-playbook --vault-password-file /home/ansible/vault /home/ansible/secPage.yml`.
- If your encryption was configured correctly, you should get no errors.
##### Verify that the secure page deployed correctly by attempting to access http://node1/secure/classified.html as the user *bond* with the password *james*.
- Run `curl -u bond http://node1/secure/classified.html` and supply the password **james** when prompted.
- The command should return the contents of **classified.html** regarding the weather in a certain city.
  
  
## Install Ansible Tower and Use it to Manage Systems
### Introduction to Ansible Tower
- Ansible Tower provides a web server interface to ansible.
- System requirements are somewhat heavy.
- Tower is only free for minimal use. Working with more than a few systems requires a paid license
- The two key benefitty of Ansible Tower are user permissioning and the audit trail (only provided with license)
  
### Installing Ansible Tower
Steps to install ansible Tower:
- Go to the following link https://docs.ansible.com/ansible-tower/latest/html/quickinstall/download_tower.html
- Download an un-tar your archive
- Get a free license (maximum 10 hosts)
- Read manual in **README.md** in your main directory that you just unarchived
```
Ansible Tower Deployment
========================

This collection of files provides a complete set of playbooks for deploying
the Ansible Tower software to a single-server installation. It is also to
install Tower to the local machine, or to a remote machine reachable by SSH.

For quickly getting started with installation and setup instructions, refer to:

- Ansible Tower Quick Installation Guide -- http://docs.ansible.com/ansible-tower/latest/html/quickinstall/index.html
- Ansible Tower Quick Setup Guide -- http://docs.ansible.com/ansible-tower/latest/html/quickstart/index.html

For more indepth documentation, refer to:

- Ansible Tower Installation and Reference Guide -- http://docs.ansible.com/ansible-tower/latest/html/installandreference/index.html
- Ansible Tower User Guide -- http://docs.ansible.com/ansible-tower/latest/html/userguide/index.html 
- Ansible Tower Administration Guide -- http://docs.ansible.com/ansible-tower/latest/html/administration/index.html
- Ansible Tower API Guide -- http://docs.ansible.com/ansible-tower/latest/html/towerapi/index.html

To install or upgrade, start by editing the inventory file in this directory. 
Uncomment and change the password from 'password' for the 3 variables below.
* admin_password
* pg_password
* rabbitmq_password

Tower can be installed in 3 different modes:
1. On a single machine. This is the default, and will install in this mode with
   no modifications to the inventory file.
2. On a single machine with a remote PostgreSQL database. Supplying the pg_host
   and pg_port variables will trigger this mode of installation.
3. Cluster/High Availability, multiple machines with a remote PostgreSQL database.
   Adding multiple hosts to the [tower] inventory group will trigger this mode of
   installation. Note that pg_host and pg_port are also required.

```
  
- Next one is ansible tower **inventory** file:
```
[tower]
localhost ansible_connection=local

[database]

[all:vars]
admin_password=''

pg_host=''
pg_port=''

pg_database='awx'
pg_username='awx'
pg_password=''
pg_sslmode='prefer'  # set to 'verify-full' for client-side enforced SSL

rabbitmq_username=tower
rabbitmq_password=''
rabbitmq_cookie=cookiemonster

# Isolated Tower nodes automatically generate an RSA key for authentication;
# To disable this behavior, set this value to false
# isolated_key_generation=true


# SSL-related variables

# If set, this will install a custom CA certificate to the system trust store.
# custom_ca_cert=/path/to/ca.crt

# Certificate and key to install in nginx for the web UI and API
# web_server_ssl_cert=/path/to/tower.cert
# web_server_ssl_key=/path/to/tower.key

# Use SSL for RabbitMQ inter-node communication.  Because RabbitMQ never
# communicates outside the cluster, a private CA and certificates will be
# created, and do not need to be supplied.
# rabbitmq_use_ssl=False

# Server-side SSL settings for PostgreSQL (when we are installing it).
# postgres_use_ssl=False
# postgres_ssl_cert=/path/to/pgsql.crt
# postgres_ssl_key=/path/to/pgsql.key

```

- some of the basic configuration stored in `/etc/tower/settings.py`
  
![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img25.png)
     

### Demo: Working with Ansible Tower
- You can create a new project and select SCM type (Manual, Git, Mercirial etc)
- **Inventories** - in this tab we can manage our invetory files, editing and adding new hosts inside of inventory files. 
  - groups can be added inside of inventories tab
  - ad-hoc commands can be executed from hosts tab
- **Credential** - from this tab you can manage your users, access type, import your private key, prompt for password/passphrase and so on
- **Execute ad-hoc command** 
![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img26.png)
  
- **Templates** - the same as in ansible playbook 
- **Jobs** - you can see the status of your jobs from this tab

![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img27.png)


## Use Documentation to Look Up Specific Information About Ansible Modules and Commands
### Finding Documentation
Two main ways to find documentation:
- built-in ansible commands
- http://docs.ansible.com/

- `ansible-doc` - by using this command we can search for any ansible module documentation
  - `ansible-doc lineinfile` - get help about `lineinfile` module
```
> LINEINFILE    (/usr/lib/python2.7/site-packages/ansible/modules/files/lineinfile.py)

        This module ensures a particular line is in a file, or replace an existing line using a back-referenced regular expression. This is primarily useful when you
        want to change a single line in a file only. See the [replace] module if you want to change multiple, similar lines or check [blockinfile] if you want to
        insert/update/remove a block of lines in a file. For other cases, see the [copy] or [template] modules.

  * This module is maintained by The Ansible Core Team
OPTIONS (= is mandatory):

- attributes
        The attributes the resulting file or directory should have.
        To get supported flags look at the man page for `chattr' on the target system.
        This string should contain the attributes in the same order as the one displayed by `lsattr'.
        The `=' operator is assumed as default, otherwise `+' or `-' operators need to be included in the string.
        (Aliases: attr)[Default: (null)]
        type: str
        version_added: 2.3

- backrefs
        Used with `state=present'.
        If set, `line' can contain backreferences (both positional and named) that will get populated if the `regexp' matches.
        This parameter changes the operation of the module slightly; `insertbefore' and `insertafter' will be ignored, and if the `regexp' does not match anywhere in
        the file, the file will be left unchanged.
        If the `regexp' does match, the last matching line will be replaced by the expanded line parameter.
        [Default: False]
        type: bool
        version_added: 1.1

- backup
        Create a backup file including the timestamp information so you can get the original file back if you somehow clobbered it incorrectly.
        [Default: False]
        type: bool

- create
        Used with `state=present'.
        If specified, the file will be created if it does not already exist.
        By default it will fail if the file is missing.
        [Default: False]
        type: bool

- firstmatch
        Used with `insertafter' or `insertbefore'.
        If set, `insertafter' and `insertbefore' will work with the first line that matches the given regular expression.
        [Default: False]
        type: bool
        version_added: 2.5

- group
        Name of the group that should own the file/directory, as would be fed to `chown'.
:
```
  
- `ansible-doc replace` - another example with `replace` module
```
# Prior to Ansible 2.7.10, using before and after in combination did the opposite of what was intended.
# see https://github.com/ansible/ansible/issues/31354 for details.
- name: Replace between the expressions (requires Ansible >= 2.4)
  replace:
    path: /etc/hosts
    after: '<VirtualHost [*]>'
    before: '</VirtualHost>'
    regexp: '^(.+)$'
    replace: '# \1'

- name: Supports common file attributes
  replace:
    path: /home/jdoe/.ssh/known_hosts
    regexp: '^old\.host\.name[^\n]*\n'
    owner: jdoe
    group: jdoe
    mode: '0644'

- name: Supports a validate command
  replace:
    path: /etc/apache/ports
    regexp: '^(NameVirtualHost|Listen)\s+80\s*$'
    replace: '\1 127.0.0.1:8080'
    validate: '/usr/sbin/apache2ctl -f %s -t'

- name: Short form task (in ansible 2+) necessitates backslash-escaped sequences
  replace: path=/etc/hosts regexp='\\b(localhost)(\\d*)\\b' replace='\\1\\2.localdomain\\2 \\1\\2'

- name: Long form task does not
  replace:
    path: /etc/hosts
    regexp: '\b(localhost)(\d*)\b'
    replace: '\1\2.localdomain\2 \1\2'

- name: Explicitly specifying positional matched groups in replacement
  replace:
    path: /etc/ssh/sshd_config
    regexp: '^(ListenAddress[ ]+)[^\n]+$'
    replace: '\g<1>0.0.0.0'

- name: Explicitly specifying named matched groups
  replace:
    path: /etc/ssh/sshd_config
    regexp: '^(?P<dctv>ListenAddress[ ]+)(?P<host>[^\n]+)$'
    replace: '#\g<dctv>\g<host>\n\g<dctv>0.0.0.0'
```

- `ansible-doc -s htpasswd` - with **-s** key we will get more consolidated view. 
```
- name: manage user files for basic authentication
  htpasswd:
      attributes:            # The attributes the resulting file or directory should have. To get supported flags look at the man page for `chattr' on the target system. This string should contain the
                               attributes in the same order as the one displayed by `lsattr'. The `=' operator is assumed as default, otherwise `+' or `-' operators need to be
                               included in the string.
      create:                # Used with `state=present'. If specified, the file will be created if it does not already exist. If set to "no", will fail if the file does not exist
      crypt_scheme:          # Encryption scheme to be used.  As well as the four choices listed here, you can also use any other hash supported by passlib, such as md5_crypt and sha256_crypt, which are linux
                               passwd hashes.  If you do so the password file will not be compatible with Apache or Nginx
      group:                 # Name of the group that should own the file/directory, as would be fed to `chown'.
      mode:                  # The permissions the resulting file or directory should have. For those used to `/usr/bin/chmod' remember that modes are actually octal numbers. You must either add a leading zero
                               so that Ansible's YAML parser knows it is an octal number (like `0644' or `01777') or quote it (like `'644'' or `'1777'') so Ansible receives a
                               string and can do its own conversion from string into number. Giving Ansible a number without following one of these rules will end up with a
                               decimal number which will have unexpected results. As of Ansible 1.8, the mode may be specified as a symbolic mode (for example, `u+rwx' or
                               `u=rw,g=r,o=r'). As of Ansible 2.6, the mode may also be the special string `preserve'. When set to `preserve' the file will be given the same
                               permissions as the source file.
      name:                  # (required) User name to add or remove
      owner:                 # Name of the user that should own the file/directory, as would be fed to `chown'.
      password:              # Password associated with user. Must be specified if user does not exist yet.
      path:                  # (required) Path to the file that contains the usernames and passwords
      selevel:               # The level part of the SELinux file context. This is the MLS/MCS attribute, sometimes known as the `range'. When set to `_default', it will use the `level' portion of the policy if
                               available.
      serole:                # The role part of the SELinux file context. When set to `_default', it will use the `role' portion of the policy if available.
      setype:                # The type part of the SELinux file context. When set to `_default', it will use the `type' portion of the policy if available.
      seuser:                # The user part of the SELinux file context. By default it uses the `system' policy, where applicable. When set to `_default', it will use the `user' portion of the policy if
                               available.
      state:                 # Whether the user entry should be present or not
      unsafe_writes:         # Influence when to use atomic operation to prevent data corruption or inconsistent reads from the target file. By default this module uses atomic operations to prevent data
                               corruption or inconsistent reads from the target files, but sometimes systems are configured or just broken in ways that prevent this. One example
                               is docker mounted files, which cannot be updated atomically from inside the container and can only be written in an unsafe manner. This option
                               allows Ansible to fall back to unsafe methods of updating files when atomic operations fail (however, it doesn't force Ansible to perform unsafe
                               writes). IMPORTANT! Unsafe writes are subject to race conditions and can lead to data corruption.
```

- Do not hesitate to use http://docs.ansible.com. Very similar to `ansible-doc` but nicer with all information about modules. In http view
  
  
## Ansible 2.7 Exam Update
### Install and Configure Control Node and Ansible Nodes
The new exam now mentions, as an objective, needing to know how to install and configure an Ansible control node:
  
This lesson will help you to learn how to:
- Install required packages
- Create a static host inventory file
- Configure Ansible managed nodes
- Configure privilege escalation on managed nodes
- Validate a working configuration using ad-hoc Ansible commands

Following commands have been used during this process:
- `sudo yum install ansible` - install ansible
- `sudo useradd ansible` and `sudo passwd ansible` - setup **ansible** user
- `sudo visudo` - configure ansible user to run without password prompt 
  - `ansible ALL=(ALL)       NOPASSWD: ALL` - add this line to **visudo**
- `vim /etc/hosts` - add worker hosts to master node as a `client1` and `client2`
- `vim /etc/ansible/hosts` - add `client1` and `client2` in your default inventory file
- `ssh-keygen` - generate ssh key on your **master** node, with **ansible** user. 
- `ssh-copy-id client1` - distribute ssh key to the worker nodes
- `ansible all -m ping` - run ad-hoc command using `ping` module through all hosts
- `ansible all -m ping -b` - run ad-hoc command in escalated mode (-b) using `ping` module through all hosts


### Shell Scripts to Run Ad-Hoc Commands
Why shell scripts? 
- Shell scripts can be used to hide complexity
- You can use shell scripts easily with Ansible ad-hoc commands
- People not experienced in Ansible can leverage them
- People not skilled in Ansible can create and use them
- There is no need to know yam and .yml formatiing

![img](https://github.com/Bes0n/EX407-Ansible-Automation/blob/master/images/img28.png)
  

### Firewall Rules
Ansible and Firewall Rules
- There are Ansible modules that can be used with firewalls
- The **firewalld** module like othersm, can be used to add or remove rules. 
- **firewalld** module - https://docs.ansible.com/ansible/latest/modules/firewalld_module.html
- **iptables** module - https://docs.ansible.com/ansible/latest/modules/iptables_module.html
  
- Playbook for installation and enabling firewalld:
```
---
- hosts: labservers
  user: ansible
  become: yes
  gather_facts: no
  tasks:
    - name: install firewalld
      action: yum name=firewalld state=installed
    - name: enable firewalld on system boot
      service: name=firewalld enabled=yes
    - name: start service firewalld, if not started
      service:
        name: firewalld
        state: started
```

- Second playbook will install **elinks** and **httpd** on your nodes
```
---
- hosts: labservers
  user: ansible
  become: yes
  gather_facts: no
  tasks:
    - name: install elinks
      action: yum name=elinks state=installed
    - name: install httpd
      action: yum name=httpd state=installed
    - name: enable and start apache on system reboot
      service: name=httpd enabled=yes state=started
```

- `elinks http://localhost `- our apache server accessible from internal network 
- `elinks http://client` - but it's not accessible from outside

- Let's create playbook to change this firewall rule:
```
---
- hosts: labservers 
  user: ansible
  become: yes
  gather_facts: no
  tasks:
    - firewalld:
        service: http
        permanent: yes
        state: enabled
    - name: restart service firewalld
      service:
        name: firewalld
        state: restarted
```
  
### Archiving
The Archive Module
- There are Ansible modules that can be used for archive purposes. 
- It is mentioned as a part of exam's objectives
- Archive module documentation page: https://docs.ansible.com/ansible/latest/modules/archive_module.html
- Assumes the compression source exists on the target
- Does **not** copy source files from the local system to the target before archiving
- You can delete source files after archiving by using the **remove=true** option. 
  
The Unarchive module
- The opposite module is **unarchive**
- unarchive module documentation page: https://docs.ansible.com/ansible/latest/modules/unarchive_module.html
- if a **checksum** is required, the use **get_url** or **uri** instead
- By default it will copy from the source file to the target before unpacking
  
- Let's create some backup-logs playbook. Which will archive directory for us and fetch it by hostnames. 
```
---
- hosts: all
  user: ansible
  become: yes
  gather_facts: no
  tasks:
  - name: Compress directory /var/log/ into /home/ansible/logs.zip
    archive:
      path: /var/log
      dest: /home/ansible/logs.tar.gz
      owner: ansible
      group: ansible
      format: gz
  - name: Fetch the log files to the local filesystem
    fetch:
      src: /home/ansible/logs.tar.gz
      dest: logbackup-{{ inventory_hostname }}.tar.gz
      flat: yes
```
  
  
### Scheduled Tasks: Cron
The Cron Module
- The **cron** module is used to manage **crontab** on your nodes. 
- You can create environmnet variables as well as named **crontab** entries
- You should add a **name** with the **crontrab** entry so it can be removed easily with a playbook
    - `e.g. name: "Job 0001"`
- When managing environment variables, no comment line gets added; however, the module uses the **name** parameter to find the correct definition line. 
  
The Cron Module - Extra Parameters
- You remove the **crontab** entry by using `state: absent` in a playbook. 
- The `name:`  gets matched for a removal
- You can use the boolean **disabled** to comment out an entry (only works if `state=present`)
- Jobs can be set to run at reboot if required. Use the `special_time: reboot` if that is required. 
- You can add a specific user if you need to set a **crontab** entry for a user (need to become **root**)
- Use `insertafter` or `insertbefore` to add env entry before or after another **env** entry
  
- Let's create some cron playbook, which will run command to check space at 5am and 5pm
```
---
- hosts: all
  user: ansible
  become: yes
  gather_facts: no
  tasks:
  - name: Ensure a job that runs at 5am and 5pm exists.
    cron:
      name: "Job 0001"
      minute: "0"
      hour: "5,17"
      job: "df -h >> /tmp/diskspace"
  
  - name: Creates an entry like "PATH=/opt/bin/" on top of crontab
    cron:
      name: PATH
      env: yes
      job: /opt/bin
  
  - name: Create an entry like "APP_HOME=/srv/app" and insert it after PATH declaration
    cron: 
      name: APP_HOME
      env: yes
      job: /srv/app
      insertbefore: PATH
```
  
- `state: absent` - to remove all created crontab entries. 
  

### Scheduled Tasks: `at`
**at** software
- The **at** command is used to schedule jobs that will be running once in the future.
- It is used for single ad-hoc jobs and is not meant as a replacement for **cron**
- It is part of a group of commands that get installed with the **at** software
- The other commands are:
  - `at` - executes commands at a specific time. 
  - `atq` - lists the users pending jobs
  - `atrm` - deletes a job by its job number
  - `batch` - executes the command depending depending on specific system load levels. A value must be specified. 
  - only `at` and `atrm` are controlled via the `at` module
  
**at** software - Service Details
- It may not be on all systems, so verify its installation 
- On Red Hat or CentOS systems it is installed with a `yum install at` command
- The service is controlled via the `atd` daemon

- Cookbook for installing and enabling `at`
```
---
- hosts: all
  user: ansible
  become: yes
  gather_facts: no
  tasks:
    - name: install the at command for job scheduling
      action: yum name=at state=installed
      
    - name: enable and start service at if not started
      service:
        name: atd
        state: started
        enabled: yes
```
  
- Scheduling a task with `at` module
```
---
- hosts: all
  user: ansible
  become: yes
  gather_facts: no
  tasks:
    - name: schedule a command to execute in 20 minutes as the ansible user
      at:
        command: df -h >> tmp/diskspace
        count: 20
        units: minutes
```

- `state: absent` - to remove scheduled task 
 

### Security
Ansible Security Tasks
- Ansible is very useful as a security tool
- You can make security changes to many nodes at once
- You can apply changes to help with easily securing nodes
- You can check lots of nodes for vulnerabilities quickly 
- It can work well with other tools that you may have in place
- Check for Ansible modules that can be used for security tasks
- Not just for Linux - can be used for OS X, Solaris, Windows, and others
- Can be used for devices such as NetApp or EMC storagfe, F5 and others
  
Some Ansible Modules for Security
- **selinux** - Configures the SELinux mode and policy
- **firewalld** and **iptables**- Both manage firewall policies
- **pamd** - Manages PAM modules
  
- Capable of working with **Datadog**, **Nagios** and other monitoring tools.
- Manage users and groups (bulk add and delete users if you don't have SSO ability)
- Can manage certificates such as OpenSSL or SSH
  
Let's us consider some examples. 
- `ansible all -a /usr/bin/uptime` - check uptime of our nodes
- We're going to create a playbook to check SELinux status
```
---
- hosts: all
  user: ansible
  become: yes
  gather_facts: no
  tasks:
    - name: Enable SELinux
      selinux:
        policy: targeted
        state: enforcing
```
  
- Let's add some user that expires and is a member of a group
```
---
- hosts: all
  user: ansible
  become: yes
  gather_facts: no
  tasks:
    - name: Ensure group "developers" exists
      group:
        name: developers
        state: present
```

- `sudo useradd tempuser` - create a user
- `sudo passwd tempuser` - set a password for a user
- `sudo grep tempuser /etc/shadow` - get password hash
```
tempuser:$6$U/WVBoCW$UX62EjlZLVucylus7N8NZ4/WV2o6kDFIMwaPAjNukwnVxYrF3tZhOCnJwnIXwxseRVrxybneDrYJuTXQ0hpAS0:18349:0:99999:7:::
```
- go to https://www.epochconverter.com/ to get epoch timestamp. Set your expire date there
- our cookbook will look like that
```
---
- hosts: all
  user: ansible
  become: yes
  gather_facts: no
  tasks:
    - name: Add a consultant whose account you want to expire
      user:
        name: james20
        shell: /bin/bash
        groups: developers
        append: yes
        expires: 1585402826 #epoch time here
        password: $6$U/WVBoCW$UX62EjlZLVucylus7N8NZ4/WV2o6kDFIMwaPAjNukwnVxYrF3tZhOCnJwnIXwxseRVrxybneDrYJuTXQ0hpAS0
        # we added password hash above
```
- `tail /etc/passwd` - we can see that **james20** user has been created
- `chage -l james20` - to see when account expires
```
Last password change                                    : Mar 28, 2020
Password expires                                        : never
Password inactive                                       : never
Account expires                                         : Apr 28, 2020
Minimum number of days between password change          : 0
Maximum number of days between password change          : 99999
Number of days of warning before password expires       : 7
```