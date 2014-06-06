# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.define :openstack do |config|
    config.vm.hostname = "openstack"
    config.vm.box = "https://github.com/2creatives/vagrant-centos/releases/download/v6.5.3/centos65-x86_64-20140116.box"
    config.vm.network :private_network, ip: "192.168.33.11"
    config.vm.synced_folder ".", "/vagrant"
    config.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--memory", 4096, "--cpus", 4]
      v.gui = false
    end
    config.vm.provision "ansible" do |ansible|
        ansible.sudo = true
        ansible.verbose = 'vv'
        ansible.playbook = "provisioning/site.yml"
        ansible.inventory_path = "provisioning/ansible_hosts"
        ansible.limit = "all"
    end
  end
end
