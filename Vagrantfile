
# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "puppetlabs/centos-6.6-64-nocm"
  config.vm.synced_folder '.', '/vagrant'
#  config.vm.network "private_network", ip: "172.16.0.5"
  config.vm.provision "ansible" do |ansible|
  	ansible.playbook = "ans_nginx/site.yml"
	ansible.extra_vars = "vars.yml"
  end
end
