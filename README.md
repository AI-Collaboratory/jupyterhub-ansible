# jupyterhub-ansible

This ansible playbook is used to setup, configure and manage DCIC's JupyterHub.
UMD's LDAP is used for authentication and every logged in user gets their own
environment managed as a Docker container.

Jupyter's [datascience-notebook] is used which includes Python, R and Julia
notebook environments with tons of useful third party libraries. But if other
languages we can pick additional containers from [docker-stacks] or build our
own. Leave an issue ticket if you'd like more things to be included.

## Setup

First get this repository if you haven't already:

    git clone https://github.com/umd-dcic/jupyterhub-ansible.git
    cd jupyterhub-ansible

Edit `hosts` to point at the IP address of your server you want to target with
the playbook. Make sure the section name for your IP address matches the `hosts`
property in your `jupyterhub.yml` file. Edit the `hub_ip` property in your
`group_vars/all/config.yml` to point at the public IP address for your
JupyterHub instance.

We run JupyterHub under SSL. If you have a certificate (ssl.crt) and private key
already (ssl.key) you can place them in this directory.  Otherwise you can
generate a self signed certificate by:

    openssl req -x509 -newkey rsa:2048 -keyout ssl.key -out ssl.crt -days XXX

If there is a passphrase associated with your certificate you will want to:

    cp group_vars/all/secret.template group_vars/all/secret.yml

and then add it the passphrase to group_vars/secret.yml.

## Run

Obviously you'll need to [install Ansible](http://docs.ansible.com/ansible/intro_installation.html#installation) in order to run the playbook. But once you've got Ansible you can install and start up JupyterHub by:

    ansible-playbook jupyterhub.yml

## Develop

If you want to work on this playbook you can use the supplied [Vagrant] setup
which will bring up a virtual Ubuntu instance and configure that:

    vagrant up

[docker-stacks]: https://github.com/jupyter/docker-stacks
[datascience-notebook]: https://github.com/jupyter/docker-stacks/tree/master/datascience-notebook
[Vagrant]: https://www.vagrantup.com/
