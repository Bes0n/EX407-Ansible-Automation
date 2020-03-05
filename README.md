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
