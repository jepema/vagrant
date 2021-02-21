![GitHub last commit](https://img.shields.io/github/last-commit/jepema/vagrant)
![Build Status](https://img.shields.io/badge/build-passing-brightgreen)
![VirtualBox Version](https://img.shields.io/badge/VirtualBox-v6.1.18-blue)
![Vagrant Version](https://img.shields.io/badge/Vagrant-v2.2.9-blue)

# Vagrant for Network Programmability

This Vagrantfile can be used to setup two Cisco Nexus 9000/3000 Virtual Switches.

## Known Issue

When using any Vagrant version higher than v2.2.9 you will (probably) receive the error below after starting the box for the second time.

```diff
The following SSH command responded with a non-zero exit status.
Vagrant assumes that this means the command failed!

sed -i '/#VAGRANT-BEGIN/,/#VAGRANT-END/d' /etc/fstab

Stdout from the command:



Stderr from the command:
```

That being said, you still can use/access the boxes you have created.