# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
#Vagrant.actions[:start].delete(Vagrant::Action::VM::ShareFolders)
Vagrant.configure("2") do |config|
#  config.vm.box = "centos/7"
  config.vm.box = "avinashkolluru/centos7-1508.01-bzip2"
  config.vm.synced_folder '.', '/vagrant', disabled: true
  config.ssh.insert_key = false
#  config.vm.network "public_network", ip: "192.168.1.203", bridge: "enp3s0", auto_config: false
  config.vm.network "forwarded_port", guest: 8080, host: 8080
# add swap
#  config.vm.provision :shell, inline: "fallocate -l 2G /swapfile && chmod 0600 /swapfile && mkswap /swapfile && swapon /swapfile && echo '/swapfile none swap sw 0 0' >> /etc/fstab"
  config.vm.provision :shell, inline: "echo vm.swappiness = 10 >> /etc/sysctl.conf && echo vm.vfs_cache_pressure = 50 >> /etc/sysctl.conf && sysctl -p"
# vagrant name
  config.vm.provider "virtualbox" do |v|
    v.name = "dbvmine"
    v.memory = 2048
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end
  config.vm.hostname = 'dbvmine'
# add vagrant name to status
  config.vm.define :dbvmine do |t|
  end
# Ansible
  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "v"
    ansible.playbook = "ora.yml"
  end
end

