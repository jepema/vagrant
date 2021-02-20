# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # Deploy 2 Nodes with two links between them

  config.vm.define "n9kv-1" do |node|
    node.vm.box = "cisco/n9kv703I79"

    node.vm.network "forwarded_port", guest: 22, host: 2122, auto_correct: true, id: "ssh"
    node.vm.network "forwarded_port", guest: 443, host: 4431, auto_correct: true, id: "https"

    # eth1/1 connected to vboxnet1, auto-config not supported.
    node.vm.network :private_network, virtualbox__intnet: "nxeth1", auto_config: false

    node.vm.provider "virtualbox" do |v|
      v.linked_clone =  true
      v.name = "n9kv-1"
      v.memory = 4096
      v.customize ["modifyvm", :id, "--nicpromisc2", "allow-all"]
      v.customize ["modifyvm", :id, "--uartmode1", "tcpserver", "21023"]
      v.customize ["modifyvm", :id, "--usb", "off"]
      v.customize ["modifyvm", :id, "--usbehci", "off"]
      v.customize ["modifyvm", :id, "--vram", "2"]
      v.check_guest_additions = false
    end

  config.vm.synced_folder ".", "/vagrant", disabled: true
  end

  config.vm.define "n9kv-2" do |node|
    node.vm.box = "cisco/n9kv703I79"

    node.vm.network "forwarded_port", guest: 22, host: 2222, auto_correct: true, id: "ssh"
    node.vm.network "forwarded_port", guest: 443, host: 4432, auto_correct: true, id: "https"

    # eth1/1 connected to vboxnet1, auto-config not supported.
    node.vm.network :private_network, virtualbox__intnet: "nxeth1", auto_config: false

    node.vm.provider "virtualbox" do |v|
      v.linked_clone =  true
      v.name = "n9kv-2"
      v.memory = 4096
      v.customize ["modifyvm", :id, "--nicpromisc2", "allow-all"]
      v.customize ["modifyvm", :id, "--uartmode1", "tcpserver", "22023"]
      v.customize ["modifyvm", :id, "--usb", "off"]
      v.customize ["modifyvm", :id, "--usbehci", "off"]
      v.customize ["modifyvm", :id, "--vram", "2"]
      v.check_guest_additions = false
    end

  config.vm.synced_folder ".", "/vagrant", disabled: true
  end

  config.ssh.insert_key = false
  config.ssh.shell = "run bash"
  config.vm.box_check_update = false
end
