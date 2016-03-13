# jupyterhub-ansible

These ansible plays are used to setup, configure and manage DCIC's JupyterHub.
They are a work in progress.

## Setup

First get this repository if you haven't already:

    git clone https://github.com/umd-dcic/jupyterhub-ansible.git
    cd jupyterhub

Edit `hosts` to point at your server.  We run JupyterHub under SSL. If you 
have a certificate (ssl.crt) and private key already (ssl.key) you can 
place them in this directory.  Otherwise you can generate a self 
signed certificate by:

    openssl req -x509 -newkey rsa:2048 -keyout ssl.key -out ssl.crt -days XXX

Since this setup uses GitHub for authentication you will need to add those
to `group_vars/all/secret.yml`. A template is included for you in 
`group_vars/all/secret.template`.

    cp group_vars/all/secret.template group_vars/all/secret.yml

Fill in the missing variables in `group_vars/all/secret.yml`. See [Jupyterhub Getting Started](https://jupyterhub.readthedocs.org/en/latest/getting-started.html) and the [oauthenicator documentation](https://github.com/jupyter/oauthenticator) for more details.

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

