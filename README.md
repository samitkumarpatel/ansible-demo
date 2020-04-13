### Ansible Demo

Use Of ansible in Azure cloud - 
[Official Documentation](https://docs.ansible.com/ansible/latest/scenario_guides/guide_azure.html)

PreReq Command to be execuated before run the paybooks are :

```
sudo apt-get update
sudo apt-get install python3-venv
sudo apt install python3-pip
pip3 install virtualenv
virtualenv -p python3 .venv
source .venv/bin/activate
pip3 install ansible
git clone https://github.com/samitkumarpatel/ansible-demo.git
cd ansible-demo/
---make the necessary change for ansible inventory---
sudo apt-get install sshpass
ansible-playbook -i inventories/cloud/host.yml install-docker.yml -e ansible_python_interpreter=python3

```

### Tips and Tricks

**Overview**

Ansible is an IT automation tool. It can configure systems, deploy software, and orchestrate more advanced IT tasks such as continuous deployments or zero downtime rolling updates.

It’s developed in python

Easy to use & learn - because of yml syntex.

Latest Version  : 2.9

Docs : https://docs.ansible.com/

Why it’s easy and popular: Ansible communicates with remote machines over the SSH protocol. By default, Ansible uses native OpenSSH and connects to remote machines using your current user name, just as SSH does.

Typically you’ll work with your favorite terminal program, a text editor, and probably a version control system to keep track of changes to your content.

Installation: 
	apt-get install ansible
	yum install ansible
	dnf install ansible
	brew install ansible
        pip install ansible


**Ansible Component **
- command line Tools:
   ```
     ansible, ansible-connection, ansible-doc, ansible-inventory, 
     ansible-pull, ansible-vault, ansible-config, ansible-console,
     ansible-galaxy, ansible-playbook, ansible-test
   ```
- module
- Plugins
- filter
- Inventory (static,dynamic)
- playbook
- roles

**Commandline Tool (ansible)**
AD-HOC command

Usage Example: 
  ```
    ansible -i ”loaclhost,” localhost –m ping
    ansible -i host.yml all –m module –a ”arg1=val1 arg2=val2”
    ansible -i inventories/dev/host.yml vm02 -m setup -a "filter=ansible_default_ipv4" 
 ```

**Commandline Tools (ansible connections)**

Connection plugins allow Ansible to connect to the target hosts so it can execute tasks on them. Ansible ships with many connection plugins, but only one can be used per host at a time.
By default, Ansible ships with several plugins. The most commonly used are the paramiko SSH, native ssh (just called ssh), and local connection types. All of these can be used in playbooks and with /usr/bin/ansible to decide how you want to talk to remote machines

```
ansible-doc -t connection -l
ansible-doc -t connection <plugin name>
```

**Commandline Tool (ansible-doc)**

displays information on modules installed in Ansible libraries

[official docs](https://docs.ansible.com/ansible/2.4/ansible-doc.html)

``` 
  ansible-doc dnf -l
  ansible-doc dnf -l | grep moduleName
  ansible-doc dnf
  ansible-doc dnf -s moduleName 
```

**Commandline Tool (ansible-inventory)**

Used to display or dump the configured inventory as Ansible sees it

[official docs](https://docs.ansible.com/ansible/latest/cli/ansible-inventory.html)

```	
 ansible-inventory --list -i inventory.yml/ini
 ansible-inventory --graph -i inventory.yml/ini
 ansible-inventory --host localhost -i inventory.ini/yml
```

**Commandline Tool (ansible-pull)**

pulls playbooks from a VCS repo and executes them for the localhost

[official docs](https://docs.ansible.com/ansible/latest/cli/ansible-pull.html)

is used to up a remote copy of ansible on each managed node, each set to run via cron and update playbook source via a source repository. This inverts the default push architecture of ansible into a pull architecture, which has near-limit less scaling potential.


**Commandline Tool (ansible-vault)**

Encryption/Decryption utility for Ansible data files

[official docs](https://docs.ansible.com/ansible/latest/cli/ansible-vault.html)

```
  ansible-vault {create,decrypt,edit,view,encrypt,encrypt_string,rekey} /path/to/vault.yml
	
  ansible-playbook –i host.yml –l "web" webdeploy.yml –ask-vault-pass
```

**Commandline Tool (ansible-config)**

view ansible configuration (read the details from default ansible.cfg).

[official docs](https://docs.ansible.com/ansible/latest/cli/ansible-config.html)

```
  ansible-config [-h] [--version] [-v] {list,dump,view}  [-c,--config] /pathto/configfile.yml

```

**Commandline Tool (ansible-console)**

Reason : Managing multiple machines sucks. No matter how much you automate there are always going to be edge cases where you'd like to perform the same command on multiple machines simultaneously.
It’s connect host to ansible-console to do some module based operation

[official docs](https://docs.ansible.com/ansible/2.4/ansible-console.html)

```
  ansible-console -i inventories/dev/host.yml -l vm02
  ansible-console -i inventories/dev/host.yml 
  ansible-console -i inventories/dev/host.yml –l vagrant
```
After connect, you can see a prompt like below

```
samitkumarpatel@vagrant (2)[f:5]$ 
```
on the above prompt you can just write the module name and pass related parameter 

Example:

```
samitkumarpatel@vagrant (2)[f:5]$ ping
```

**Commandline Tool (ansible-galaxy)**

Ansible Galaxy refers to the Galaxy website, a free site for finding, downloading, and sharing community developed roles.

It’s not limit to Galaxy, we can manage galaxy role in any SCM tool, like github, bitbucket, etc..

Use for create or install ansible role


[official docs](https://docs.ansible.com/ansible/latest/galaxy/user_guide.html)

```
ansible-galaxy init folderName
ansible-galaxy  install –r requirenment.yml –role-path=/path/to/folder
```

and a requirenment.yml can be look like

```
- name: role-name
  src: git+http://url:port/path/repo.git
  version: branchName
```

**Commandline tool (ansible-playbook)**

An Ansible playbook is an organized unit of scripts that defines work for a server configuration managed by the automation tool AnsibleCan do a lot withit

[official doc](https://docs.ansible.com/ansible/latest/user_guide/playbooks_intro.html)

```
ansible-playbook -i inventories/dev/host.yml playbook.yml
```

**Commandline tool (ansible-test)**

[official docs](https://docs.ansible.com/ansible/latest/dev_guide/testing_integration.html)

[molecule](https://molecule.readthedocs.io/en/latest/)

Drive- VM, docker, 

Install – `pip install molecule docker-py`

```
molecule init role -r <<role_name>> -d <<driver>>
molecule test
```



**module**

A module is a reusable, standalone script that Ansible runs on your behalf, either locally or remotely 
Modules (also referred to as “task plugins” or “library plugins”) are discrete units of code that can be used from the command line or in a playbook task. Ansible executes each module, usually on the remote target node, and collects return value
We can write our own module based on our needs. You may write specialized modules in any language that can return JSON (Ruby, Python, bash, etc).

[official docs](https://docs.ansible.com/ansible/latest/modules/modules_by_category.html)

**plugins**

Plugins are pieces of code that augment Ansible's core functionality. 
Ansible uses a plugin architecture to enable a rich, flexible and expandable feature set. 
Ansible ships with a number of handy plugins

[official docs](https://docs.ansible.com/ansible/latest/plugins/plugins.html)

**filter**

Filters in Ansible are from Jinja2, and are used for transforming data inside a template expression. ... Take into account that templating happens on the Ansible controller, not on the task's target host, so filters also execute on the controller as they manipulate local data.

[official docs](https://docs.ansible.com/ansible/latest/user_guide/playbooks_filters.html)

```
{{variable | to_yaml}}
{{variable | to_json}}

```

**inventory**

The Ansible inventory file defines the hosts and groups of hosts upon which commands, modules, and tasks in a playbook operate. 
The file can be in one of many formats depending on your Ansible environment and plugins

There are 2 types of inventory you can deal with – static and dynamic

[official docs](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html)

Inventory file contain (in yaml). also to define this with ini format

```
localhost:
  hosts:
    localhost:
      ansible_connection: local
  vars:
    ansible_python_interpreter: python
azure:
  hosts:
    0.0.0.0:
      ansible_connection: ssh
      ansible_user: lab_admin
      ansible_password: xxxxxxx
    0.0.0.1:
      ansible_connection: ssh
      ansible_user: testadmin
      ansible_password: xxxx
```

ans inventory structure can look like per env wise are :

```
inventories
├── cloud
│   ├── group_vars
│   │   └── vars.yml
│   └── host.yml
├── pp
│   ├── group_vars
│   │   └── all
│   ├── host.yml
│   └── host_vars
├── test
│   ├── group_vars
│   │   └── all
│   ├── host.yml
│   └── host_vars
└── vagrant
    ├── group_vars
    │   ├── all
    │   │   ├── vars.yml
    │   │   └── vault.yml
    │   └── vm01
    ├── host_vars
    └── hosts.yml
```

**playbook**

An Ansible playbook is an organized unit of scripts that defines work for a server configuration managed by the automation tool Ansible. 

Ansible is a configuration management tool that automates the configuration of multiple servers by the use of Ansible playbooks

[official docs](https://docs.ansible.com/ansible/latest/user_guide/playbooks.html)

In playbook , you can use 
Variable
Template (jinja2)
Condition
Loops
Block


**role**

Roles provide a framework for fully independent, or interdependent collections of variables, tasks, files, templates, and modules.
In Ansible, the role is the primary mechanism for breaking a playbook into multiple files. 

Note- Roles are not playbooks


```
.
├── Jenkinsfile / azure-pipeline.yml
├── README.md
├── defaults
│   └── main.yml
├── handlers
│   └── main.yml
├── meta
│   └── main.yml
├── molecule
│   ├── azure
│   │   ├── create.yml
│   │   ├── destroy.yml
│   │   └── molecule.yml
│   ├── default
│   │   ├── Dockerfile.j2
│   │   └── molecule.yml
│   └── resources
│       ├── playbooks
│       │   └── playbook.yml
│       └── tests
│           └── test_default.py
├── requirements.txt
├── tasks
│   ├── main.yml
│ 
└── templates
    ├── file.yml.j2
```

