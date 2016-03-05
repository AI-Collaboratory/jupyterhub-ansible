# jupyterhub

set up a jupyterhub on a remote server

## Setup and Configure

First get this repository if you haven't already:

    git clone https://github.com/umd-dcic/jupyterhub-ansible.git
    cd jupyterhub

Next edit `hosts` to point at your server, and edit `hub_ip` in 
`group_vars/all/config.yml` to match the server you added to `hosts`.
Note: this is the IP address that JupyterHub will bind to, so be sure
it is the ip address on the interface you want to bind to, which may not 
be the public IP you see when you resolve the host name.

It's best to run JupyterHub under SSL. If you have a certificate (ssl.crt)
and private key already (ssl.key) you can place them in this directory. 
Otherwise you can generate a self signed certificate by:

    openssl req -x509 -newkey rsa:2048 -keyout ssl.key -out ssl.crt -days XXX

Since this setup uses GitHub for authentication you will need to add those
to `group_vars/all/secret.yml`. A template is included for you in 
`group_vars/all/secret.template`.

    cp group_vars/all/secret.template group_vars/all/secret.yml

and then add the missing variables into `group_vars/all/secret.yml`. See [Jupyterhub Getting Started](https://jupyterhub.readthedocs.org/en/latest/getting-started.html) for more details.

## Run

    ansible-playbook -v jupyterhub.yml

## Data

You don't need the `sync.yml` playbook or the exercises role to run a 
jupyterhub server. These are for copying sample data and notebooks to 
user directories.
