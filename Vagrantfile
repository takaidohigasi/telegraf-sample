# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "centos65-x86_64"
  config.vm.box_url = "https://github.com/2creatives/vagrant-centos/releases/download/v6.5.3/centos65-x86_64-20140116.box"

  DEPLOY_NODES = {
    'client-node' => '192.168.33.2',
    'log-server'  => '192.168.33.3'
  }

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024", "--cpus", "1", "--ioapic", "on"]
    vb.customize ["setextradata", :id, "VBoxInternal/Devices/VMMDev/0/Config/GetHostTimeDisabled", 0]
  end

  DEPLOY_NODES.each do |name, address|
    config.vm.define name do |node|
      node.vm.hostname = name
      node.vm.network :private_network, ip: address
    end
  end
end

