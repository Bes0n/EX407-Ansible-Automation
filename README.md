# EX407-Ansible-Automation
Red Hat Certified Specialist in Ansible Automation (EX407) Preparation Course

- [Understanding Core Components of Ansible](#understanding-core-components-of-ansible)
    - [Understanding Core Components of Ansible Part 1](#understanding-core-components-of-ansible-part-1)
    - [Understanding Core Components of Ansible Part 2](#understanding-core-components-of-ansible-part-2)
    - [A Brief Tour of the Ansible Configuration File](#a-brief-tour-of-the-ansible-configuration-file)
    - [LAB Getting Started with Ansible](#lab-getting-started-with-ansible)
- [Run Ad-Hoc Ansible Commands](#run-ad-hoc-ansible-commands)
    - [Run Ad-Hoc Ansible Commands](#run-ad-hoc-ansible-commands)
    - [Demonstration: Ansible Ad-Hoc Commands Part 1](#demonstration-ansible-ad-hoc-commands-part-1)
    - [Demonstration: Ansible Ad-Hoc Commands Part 2](#demonstration-ansible-ad-hoc-commands-part-2)
    - [LAB Ad-Hoc Ansible Commands](#lab-ad-hoc-ansible-commands)

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

### LAB Getting Started with Ansible
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

### LAB Ad-Hoc Ansible Commands
One of the keys to success with Ansible is being able to run `ad-hoc` commands. The value of `ad-hoc` commands is underscored by the fact that it is an objective of the Red Hat Certified Ansible Specialist exam. This exercise guides students through crafting many `ad-hoc` commands which will not only build experience with the concept but also broaden the students' exposure to various Ansible command modules.

##### Additional Information and Resources
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