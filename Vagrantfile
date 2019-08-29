# coding: utf-8
# -*- mode: ruby -*-
# vi: set ft=ruby :

BOX_CENTOS7  = 'centos/7'
RAM          = 1024       # Default memory size in MB

# Network configuration
NETWORK           = "192.168.79."
NETMASK           = "255.255.255.0"

# IP, RAM, GUI, BOX, HDD_SDB, Default start
HOSTS = {
  "test01-centos7" => [NETWORK + "250", RAM, BOX_CENTOS7]
}

# unless Vagrant.has_plugin?("vagrant-vbguest")
#   raise 'vagrant-vbguest plugin is not installed!'
# end

Vagrant.configure("2") do |config|
  # Allow auto-build VBox Guest - this will allow adjust Screen Resolution
  # config.vbguest.auto_update = false
  # config.vbguest.no_remote = true

  config.ssh.insert_key = true

  HOSTS.each do | (name, cfg) |
    ipaddr, ram, box = cfg

    config.vm.define name do |machine|
      machine.vm.box = box
      machine.vm.synced_folder ".", "/vagrant", disabled: true
      machine.vm.provider "virtualbox" do |vbox|
        vbox.memory = ram
        vbox.name   = name
      end

      machine.vm.hostname = name
      machine.vm.network 'private_network', ip: ipaddr, netmask: NETMASK
    end # HOSTS-each
  end
end
