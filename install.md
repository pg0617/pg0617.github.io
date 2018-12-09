---
title: Ansible Tutorial
---

# Ansible

## What is Ansible

Suppose you have a web application and you would like to deploy it. You might think Heroku. Which in some cases
would work fine assuming your application is rather simple. But what happens when you have alot of traffic
or need a database along with a reverse proxy server and load balancer? This is where Ansible comes in. Using Ansible, orchestrating
complex deployments becomes easy along with much more. Ansible is a radically simple IT automation engine that automates cloud provisioning, configuration management, application deployment, intra-service orchestration, and many other IT needs.

## Installation

Ansible can be installed on one machine then the this center machine can control the remote machines without install any software on the remote machines. You can use OS package manager to run the latest released version Red Hat Enterprise Linux (TM), CentOS, Fedora, Debian, or Ubuntu. The Python package manager "pip" can also be applied to get the lastest released version of the ansible.
As long as your can run Python2 or Python3 on your machine, you can run Ansible. The Ansible can be run on Red Hat, Debian, CentOS, macOS, any of the BSDs but not the Windows. 
Using sftp to control the nodes (remote machines), if sftp is not applicable, you can use scp.

## How to install
#### Intall from Latest Release

###### Install Ansible with DNF/Yum
On Fedora:

    $ sudo dnf install ansible
    
On RHEL and CentOS:

    $ sudo yum install ansible
    
##### Install Ansible with Apt
On Ubunto:

    $ sudo apt-get update
    $ sudo apt-get install software-properties-common
    $ sudo apt-add-repository --yes --update ppa:ansible/ansible
    $ sudo apt-get install ansible
    
On Debian：
First, add

    deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main
    
to /etc/apt/sources.list

Then, run the following code:
    
    $ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
    $ sudo apt-get update
    $ sudo apt-get install ansible
    
##### Install with Portage

    $ emerge -av app-admin/ansible
    $ echo 'app-admin/ansible' >> /etc/portage/package.accept_keywords

##### Install with pkg
   
    $ sudo pkg install py27-ansible

or

    $ sudo pkg install py36-ansible
    
or install from port

    $ sudo make -C /usr/ports/sysutils/ansible install

##### Install with OpenCSW for Sloaris

    # pkgadd -d http://get.opencsw.org/now
    # /opt/csw/bin/pkgutil -i ansible

##### Install with Pacman for Arch Linux

    $ pacman -S ansible
    
##### Install with pip
A preferred way for MacOS to install Ansible

    $ sudo easy_install pip
    $ sudo pip install ansible
    $ pip install git+https://github.com/ansible/ansible.git@devel
    
Using     

    $ sudo CFLAGS=-Qunused-arguments CPPFLAGS=-Qunused-arguments pip install ansible
    
to decrease the noise of compiler when installing ansible on macOS Mavericks

#### Install from Tarballs of Tagged Releases

Download Tarball release from https://releases.ansible.com/ansible/?extIdCarryOver=true&sc_cid=701f2000001OH7YAAW to avoid git checkout.

#### Install by running the source code
Clone the code from the github with 

    $ git clone https://github.com/ansible/ansible.git --recursive, 

then apply 

    $ cd ./ansible
    
After get the source code, setting up the environment with 

Bash:

    $ source ./hacking/env-setup
    
or Fish:

    $ source ./hacking/env-setup.fish
    
Ansible can also be installed vis 

    $ sudo pip install -r ./requirements.txt

Using 

    $ git pull --rebase
    
to update the ansible checkout
    
Finally, test the installation via

    $ ansible all -m ping --ask-pass


## How To Use
#### Inventory Management
Ansible's inventory contains all the systems that Ansible can work against. By default, Ansible's inventory is saved at /etc/ansible/hosts. This file can be in several formats, but INI is supported by default.

An INI inventory file looks like the following:

    one.example.com
    
    [group_one]
    two.example.com
    three.example.com
    [group_two]
    three.example.com
    four.example.com:5080
    five.example.com

All of the lines with example.com are host names. A host name can be extended with the port number if a non-standard port is being used. The names inside square brackets are group names. Groups can be used to send commands to only a subset of hosts. It is possible to have a host in more than one group, in the above example, 'three.example.com' is in both 'group_one' and 'group_two'.
    
#### Ad-hoc Commands
An ad-hoc command is a command that you type in to run once, without saving it for later. For example, the following command will copy a file to all of the hosts in your inventory file:

    ansible all -m copy -a "src=/srcfile dest=/destloc"

In the above command, 'all' indicates that this command should be run against all servers in the invetory. It is also possible to use just one host or one group of hosts.

    ansible one.example.com -m copy -a "src=/srcfile dest=/destloc"
    ansible group_one -m copy -a "src=/srcfile dest=/destloc"
    
The -m option specifies a module, in this case the copy module. The default module is 'command'. A index of modules can be found at https://docs.ansible.com/ansible/2.5/modules/modules_by_category.html .

The -a option specifies that what follows are the arguments to pass to the module, in this case the source file location and the destination file location.

#### Playbooks
Ad-hoc commands are useful when you want to do something simple quickly, but don't offer much advantage with more complex tasks that need to be done repeatedly. Instead, Ansible uses playbooks to achieve this. A playbook allows the user to setup multiple 'plays', which assign groups of hosts to tasks. At the simplest level, tasks are simply calls to ansible modules, as in an ad-hoc command.

Playbooks are written in YAML format. An example playbook looks like the following:

    - hosts: all
      remote_user: root
    
      tasks:
      - name: copy file to all hosts
        copy: src=/srcfile dest=/destloc
    
    - hosts: group_one
      remote_user: root
      
      tasks:
      - name: copy file to group_one
        copy: src=/group_one_file dest=/group_one_dest

This playbook contains two plays, each containing one task. Each play lists the hosts that it will be run against, and the user that the command will be run as on the host. Each play also contains a list of tasks. Each task has a name, which describes what the task does, and then a module name, followed by a list of arguments, in the form 'arg_name'='arg_value'.

To execute a playbook, use the following syntax:

    ansible-playbook playbookFileName.yml

## Where To Go From Here

#### Try Ansible with your first command
Editing /etc/ansible/hosts to put your remote systems on it and find your authorized_keys.

Setting up SSH agent to avoid retyping passwords with 

    $ ssh-agent bash
    $ ssh-add ~/.ssh/id_rsa
    
Ping all your nodes 
    
    $ ansible all -m ping

Now, you are ready to try to run the following command on all your nodes

    $ ansible all -a "/bin/echo hello"

## To view more about variables, loops and conditionals of Ansible
#### [Click here](https://pg0617.github.io/variables)

