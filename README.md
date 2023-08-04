# perfSONAR-Sampler VERSION 5
This project illustrates, using VMs, what the document [MaDDash Quick Install Guide v4](https://docs.google.com/document/d/1k7FT66MKPy3JjpD5k0OFAFlTpSdFmZ6huhTUDQ2rGGY/edit?usp=sharing) covers bit by bit.

The project pulls together files to move from bare VMs to working perfSONAR Testpoint nodes and a MaDDash grid.  It doesn't show real network tests but just traffic between the different VMs on the single host.  The project files can later be reviewed and edited for use on real hardware for perfSONAR node configs and MaDDash server web setups.

The project has been intentionally tested on a small system, an Intel Nuc (NUC8i3BEK). It has a dual core Intel Core i3-8109U, 8G of RAM, and a 230g M.2 SATA drive. The project works on this level of hardware.

The project uses VirtualBox VMs and Centos 7 (though other RPM based OS's may work, but use an OS approved for PerfSonar systems).  To make networking work smoothly, the project  does require one extra bit of hardware. The base system needs a second ethernet port.  Many systems come native with that, use that if your system has it. The Nuc doesn't have the second port so a 'USB3 to Ethernet' dongle was used instead and it worked fine.

Build the base system with a 'vagrant' user (sudo enabled) and any pword you'll remember.  Do a minimal install and add the EPEL repository and a final 'update'.  **Log into the system as user 'vagrant'**.

The base host needs two ethernet interfaces, but only the first one should to be active during the install. The easiest way to get this setup is to only plug in one ethernet cable to the base system during the initial install. Once Centos is installed, plug in the second ethernet cable into the second port or plug in the USB-enet adapter with the ethernet cable connected. Then use the following commands:
```
ip a
   (use this to identify the second interface.
    On the Nuc, with my USB-enet dongle, it is enp0s20f0u2.)
   
sudo nmcli dev disconnect enp0s20f0u2
   (this disconnects the port but leaves it in an 'up' state)
   
ip a
   (confirm the second interface is listed, and up, but doesn't have an IP addresses)
```

Once that is done you'll need to load Ansible, Vagrant and VirtualBox. Ansible and Vagrant install with basic yum commands.  VirtualBox install is a bit more involved but there are many sites with detailed directions.

Make a SSH key for the Vagrant user:
```
ssh-keygen -o -a 256 -t ed25519
```
You will need to have 4 IPs available on the same network segment. Review the chart below and create a similar chart for your deployment.

Here is the chart for my systems. You'll need to make one of these using your available IPs. VM MAC addresses are ephemeral in nature, so using the ones suggested would be easiest, though not required.

## Chart for perfSONAR-Sampler
**Second host interface name:** enp0s20f0u2

**My Address** segment for the IPs in use: 192.168.0.0/23 (yours if probably a /24!)

|Name |IP# |Mac Addr |
| ---| ---| ---|
|ps1|192.168.1.211|52:54:00:73:6f:41|
|ps2|192.168.1.212|52:54:00:73:6f:42|
|ps3|192.168.1.213|52:54:00:73:6f:43|
|md|192.168.1.2134|52:54:00:73:6f:44|

If you make changes to the above chart, plan to make similar edits to:

Top section of **Vagrantfile** and top section of **mesh.json**.

Then the IP for the MaDDash server is used in several files.


## Building and Configure the VMs
Bring up all the needed VMs.  This is composed of 3 mesh network perfSONAR nodes, a fourth node for the Archiver and  MaDDash systems.
```
curl -L https://github.com/preese/perfSONAR-Sampler/archive/main.tar.gz | tar xzf -
cd perfSONAR-Sampler-main

vi Vagrantfile
   (Using your chart, edit this file, and all the others mentioned, if you changed the
   IP numbers I was using.)
```

Start the VMs:
```
vagrant up
```
**Some 30+ minutes later** you should be able to vist the MaDDash server URL to see the grids.  In the stock case it would be **http://192.168.1.214/maddash-webui**, (change to your IP from the Chart).

Let the project run for a couple of hours.  If all went well, you should see the grid start to populate
