# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network "private_network", ip: "192.168.33.15"
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "jupyterhub.yml"
    ansible.inventory_path = "hosts"
    ansible.limit = "develop"
    ansible.extra_vars = {
      ansible_ssh_user: "vagrant"
    }
  end
end
