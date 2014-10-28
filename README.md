# ansible-centos-django-stack

An Ansible Playbook for quickly getting a Django Web App up and running on CentOS.

This playbook installs and configures the following applications:

    * Python (latest version from source)
    * Nginx
    * Gunicorn
    * PostgreSQL
    * Memcached (latest version from source)
    * RabbitMQ
    * Virtualenv
    * Supervisor
    * Celery
    * Flower
    * Django

Tested on CentOS 6.5 x64 with Cloud Providers: Digital Ocean, <a href="https://flutue.com">Flutue</a>

## Requirements

### Ansible

#### Installation

##### Ubuntu
    
    apt-get install software-properties-common
    apt-add-repository ppa:ansible/ansible
    apt-get update
    apt-get install ansible

##### Mac
    
    brew update
    brew install ansible

### SSHPass

#### Installation

##### Ubuntu

    apt-get install sshpass

##### Mac

    cd ~/Downloads
    curl -O -L http://downloads.sourceforge.net/project/sshpass/sshpass/1.05/sshpass-1.05.tar.gz
    tar xvzf sshpass-1.05.tar.gz
    cd sshpass-1.05

    ./configure
    make
    sudo make install

## Getting Started

This project comes with a sample Vagrantfile. This means you can use Vagrant and VirtualBox to
quickly test this playbook on your local machine.

Just run the following command:

    vagrant up

Wait a few minutes and go to http://192.168.33.10 and you will see a simple blog app up and running!

You should also be able to access the following URLs:

* http://192.168.33.10:9001 (Supervisor)
* http://192.168.33.10:5555 (Flower)
* http://192.168.33.10:15672 (RabbitMQ)

Really impressive, uh?

## Playing on a real cloud server

Just edit the hosts/{{ environment }} file with your hosts information and edit the group_vars/all
file with your app settings.

Then, all you have to do is run the following command:

    ansible-playbook -i hosts/{{ environment }} site.yml

## Playing with your own web app

If you want to test your own web app, just edit the groups_vars/all file with your app settings.

Pay attention to the repo_deploy_key setting. The one on group_vars/all is for demonstration
purposes only. When deploying your app, you will have to create your own deployment key on Github, 
Bitbucket, Stash.

More info:
https://developer.github.com/guides/managing-deploy-keys/#deploy-keys
https://confluence.atlassian.com/display/BITBUCKET/Use+deployment+keys