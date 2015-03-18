# Ansible Bootstrap

This repository contains a basic Ansible role used for bootstrapping an Ubuntu server.

The included tasks are:

* Copy configuration files
* Configure locale
* Install and update Ubuntu packages
* Create users, assigning groups and public keys
* Basic security configuration:
    - Disable SSH root access
    - Disable password authentication
    - Install [Fail2ban](http://www.fail2ban.org/wiki/index.php/Main_Page)
    - Configure [UFW Firewall](https://help.ubuntu.com/community/UFW)
* Install and configure [Nullmailer](http://untroubled.org/nullmailer/) with [Mandrill](https://mandrill.com)
* Install and configure [NewRelic server monitoring](https://docs.newrelic.com/docs/server/installation-ubuntu-and-debian)

Only tested against Vagrant Trusty64 box, it should also work in Precise

_ansible.cfg_ and _hosts_ are configured to connect to a Vagrant server running with a default configuration  (localhost in port 2222). If you are using Vagrant 1.7 or greater, update _private_file_key_ path in _ansible.cfg_ as explained in [Ansible documentation](http://docs.ansible.com/guide_vagrant.html#running-ansible-manually)

   
   
## Usage

First of all, install Ansible, in Ubuntu:

    sudo add-apt-repository ppa:rquillo/ansible
    sudo apt-get update
    sudo apt-get install ansible

[Install Vagrant](https://www.vagrantup.com/downloads) and create a server  

    vagrant init ubuntu/trusty64
    vagrant up

Now, check the connection from Ansible to the server. From the project root you can ping to the server

    ansible dev -m ping
  
And check the setup
  
    ansible dev -m setup


Once checked, update the file _development.yml_ with your own configuration, if not configured properly, the installation will not work.

 
Finally, the role can be executed using

    ansible-playbook bootstrap.yml

If you don't need any of the tasks, just comment them in the _main.yml_ file of the role.  


## License

Released under the MIT License, Copyright (c) 2014-15 - Diego Rodríguez
