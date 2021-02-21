# -*- mode: ruby -*-
# vi: set ft=ruby :

# Minimum Vagrant and Vagrant API version
Vagrant.require_version "= 2.2.6"
VAGRANTFILE_API_VERSION = "2"

# Required modules if any
require 'yaml'

# Read YAML file
nodes = YAML.load_file('nodes.yaml')

# Goal - Deploy two nodes with one active link between them
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

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

  # Iterate through entries in YAML file
  nodes.each do |nodes|
    config.vm.define nodes["name"] do |node|
      node.vm.box = nodes["box"]
      # node.vm.network "private_network", ip: servers["ip"]

    # Port forwarding
    config.vm.network "forwarded_port", guest: 22, host: nodes["ssh_port"], auto_correct: true, id: "ssh"
    config.vm.network "forwarded_port", guest: 443, host: nodes["https_port"], auto_correct: true, id: "https"

      # Generic VM settings
      node.vm.provider :virtualbox do |vb|
        vb.name = nodes["name"]
        # vb.cpus = nodes["cpu"]
        # vb.memory = servers["memory"]
        vb.customize ["modifyvm", :id, "--uartmode1", "tcpserver", nodes["console_port"]]
      end

    end

  end

end