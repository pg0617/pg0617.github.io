---
title: "Ansible"
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

### How to install
#### Intall from Latest Release
TODO
#### Install from Tarballs of Tagged Releases
TODO
#### Install by running the source code
Clone the code from the github with $ git clone https://github.com/ansible/ansible.git --recursive, then apply $ cd ./ansible
After get the source code, setting up the environment with Bash/Fish

## How To Use

TODO

## Where To Go From Here

TODO
