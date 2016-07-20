# jupyterhub-ansible

This ansible playbook ius used to setup, configure and manage DCIC's JupyterHub.
UMD's LDAP is used for authentication and every logged in user gets their own
environment managed as a Docker container.

By default we're using the stock SciPy Docker container. But if other languages
environments are useful to you let us know and we can pick additional 
containers from [docker-stacks] or build our own.

## Setup

First get this repository if you haven't already:

    git clone https://github.com/umd-dcic/jupyterhub-ansible.git
    cd jupyterhub-ansible

Edit `hosts` to point at your server.  We run JupyterHub under SSL. If you 
have a certificate (ssl.crt) and private key already (ssl.key) you can 
place them in this directory.  Otherwise you can generate a self 
signed certificate by:

    openssl req -x509 -newkey rsa:2048 -keyout ssl.key -out ssl.crt -days XXX

## Run

Obviously you'll need to [install Ansible](http://docs.ansible.com/ansible/intro_installation.html#installation) in order to run the playbook. But once you've got Ansible you can install and start up JupyterHub by:

    ansible-playbook -v jupyterhub.yml

## Data

You don't need the `sync.yml` playbook or the exercises role to run a 
jupyterhub server. These are for copying sample data and notebooks to 
user directories.

## Develop

If you want to workon this playbook you can use the supplied Vagrant setup.

    vagrant up

[docker-stacks]: https://github.com/jupyter/docker-stacks
