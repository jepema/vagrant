# -*- mode: ruby -*-
# vi: set ft=ruby :

# Goal - Deploy two nodes with one active link between them
Vagrant.configure("2") do |config|

  # Base image (Cisco Nexus 9000/3000 Virtual Switch)
  config.vm.box = "cisco/n9kv703I79"

  # Port forwarding
  config.vm.network "forwarded_port", guest: 22, host: 2222, auto_correct: true, id: "ssh"
  config.vm.network "forwarded_port", guest: 443, host: 4433, auto_correct: true, id: "https"

  # Port eth1/1 connected to vboxnet1 (auto-config not supported)
  config.vm.network :private_network, virtualbox__intnet: "vboxnet1", auto_config: false

  # Generic Vagrant settings
  config.ssh.insert_key = false
  config.ssh.shell = "run bash"
  config.vm.box_check_update = false
  config.vm.synced_folder ".", "/vagrant", disabled: true

  # Generic VM settings
  config.vm.provider "virtualbox" do |v|
    v.linked_clone = true
    v.cpus = 2
    v.memory = 4096
    v.customize ["modifyvm", :id, "--nicpromisc2", "allow-all"]
    v.customize ["modifyvm", :id, "--usb", "off"]
    v.customize ["modifyvm", :id, "--usbehci", "off"]
    v.customize ["modifyvm", :id, "--vram", "2"]
    v.check_guest_additions = false
  end

  # Loop over each VM to apply node specific settings 
  (1..2).each do |i|
    config.vm.define "n9kv-#{i}" do |node|
      node.vm.provider "virtualbox" do |v|
        v.name = "n9kv-#{i}"
        v.customize ["modifyvm", :id, "--uartmode1", "tcpserver", "2#{i}023"]
      end
    end
  end

end