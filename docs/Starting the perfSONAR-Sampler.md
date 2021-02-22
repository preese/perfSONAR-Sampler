# Starting the perfSONAR MaDDash sampler project

This project doesn't do any network monitoring! It does show how you can set up the perfSONAR RPMS to install testpoint nodes and then a central management Maddash web site, incorporating the monitoring results from the testpoint nodes.



This is essentially a virtual machine implementation of Andy Lake's [MaDDash Quick Install Guide v4](https://docs.google.com/document/d/1k7FT66MKPy3JjpD5k0OFAFlTpSdFmZ6huhTUDQ2rGGY/edit?usp=sharing} document.


The project has been intentionally tested this on a small system, an Intel Nuc (NUC8i3BEK). It has a dual core Intel Core i3-8109U, 8G of RAM, and a 230g M.2 SATA drive. The project works on this level of hardware. If you have a larger box for this demo system, it will make the install and operation smoother.


The project uses libvirt KVM virtual machines and Centos 7, (the perfSONAR/MaDDash VMs also use Centos 7). Related to using libvirt VMs, the project uses Macvtap networking. This has a number of advantages not discussed here. It does require one extra bit of hardware however. The base system needs a second ethernet port! Many systems come native with that, use that if your system has it. The Nuc doesn't have the second port so a 'USB3 to Ethernet' dongle was used instead and it worked fine.


Build the base system with its own hard coded MAC and IP, **with the user 'vagrant' (sudo enabled) and any pword you'll remember**. Use Centos7, do a minimal install and add the EPEL repository, do a final 'update'.

The base host needs two ethernet interfaces, but only one needs to be active.  The easiest way to get this setup is to only plug in one ethernet cable to the base system during the initial install.  Once Centos is installed, plug in the second ethernet cable into the second port or plug in the USB-enet adapter with the ethernet cable connected.  Then use the following commands:
```
ip a
   (use this to identify the second interface, on the Nuc, with USB-enet dongle, it is
   enp0s20f0u2 typically if the network has DHCP enabled, this will be assigned an IP
   address when the cable is plugged in)
sudo nmcli dev disconnect enp0s20f0u2
ip a
   (the second interface should still be listed, and up, but not have any IP addresses)
```


Once that is done you'll need to load Git, Ansible and Vagrant. Git and Ansible are straight forward yum installs. Vagrant has a yum component and the libvirt provisioner needs to be added.

Tool install on Centos 7:
```
sudo yum install -y git ansible
sudo yum install -y yum-utils
sudo yum-config-manager --add-rep https://rpm.releases.hashicorp.com/RHEL/hashicorp.repo
sudo yum -y install libvirt-daemon-kvm libvirt-client vagrant gcc-c++ make libstdc++-devel libvirt-devel
sudo systemctl enable --now libvirtd
  
sudo usermod -a -G libvirt $( id -un ) 
newgrp libvirt

vagrant plugin install vagrant-libvirt

See this URL for more info: https://www.onyxpoint.com/blog/vagrant-libvirt-on-centos-7/
```

Make a SSH key for the Vagrant user:
```
ssh-keygen -o -a 256 -t ed25519
```


With all of this accomplished, there are just a few more things to establish.  To start you'll need to have management access to a DHCP. For networking IPs, you could be bold and use a public network or more likely use a non-routable private segment. The project git files use the 192.168.1.0/24 net, but that can be adjusted if needed (see maddash.yml).


Next let's plan the name, IP, and MAC addr needed for the project.

|Name |IP# |Mac Addr |
| ---| ---| ---|
|ps1|192.168.1.210|52:54:00:73:6f:41|
|ps2|192.168.1.211|52:54:00:73:6f:42|
|ps3|192.168.1.212|52:54:00:73:6f:43|
|md|192.168.1.213|52:54:00:73:6f:44|
|  |  |  |  |
|dj1|192.168.1.214|52:54:00:73:6f:45|
|dj2|192.168.1.215|52:54:00:73:6f:46|
|dj3|192.168.1.216|52:54:00:73:6f:47|

If you make changes to the above table, plan to make similar edits to: Vagrantfile, review all the .yml files and possibly mesh.json & disjoint.json.


To set the context, VMs create their own MAC addresses, thus the set suggested will be fine, as the suggested MAC addrs will be seeded to the VMs. From the MAC address, the DCHP server should provide a fixed IP number indicated.  Lastly, depending on your setup, you may be able to assign a private or public FQDN for each planned VM.


Now that the base system is done and a plan the VM names, IP, MAC addr has been created, return to the project README.md page for more steps.
