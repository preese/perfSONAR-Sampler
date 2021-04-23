# perfSONAR-Sampler
This project illustrates, using VMs, what the document [MaDDash Quick Install Guide v4](https://docs.google.com/document/d/1k7FT66MKPy3JjpD5k0OFAFlTpSdFmZ6huhTUDQ2rGGY/edit?usp=sharing) covers bit by bit.

Andy Lake put together the first version of this document several years ago.  That prompted an AHA! moment for me.  This project is an attempt to share that AHA! with others looking to better understand the perfSONAR and MaDDash projects.
<p align="left">
<img src="https://github.com/preese/perfSONAR-Sampler/blob/main/docs/Maingrid.png">
</p>

The project pulls together .json, vagrant and ansible files to move from a number of bare VMs to a working perfSONAR and MaDDash grid.  It doesn't show real network tests but just traffic between the different VMs on the single host.  The project files can later be reviewed and edited for use on real hardware for perfSONAR node configs and MaDDash server web setups.

The project also shows how to setup a second dashboard showing a disjoint grid in addition to the more traditional mesh grid.
<p align="left">
<img src="https://github.com/preese/perfSONAR-Sampler/blob/main/docs/Disjointgrid.png">
</p>

The [Wiki page](../../wiki) for the project details how to setup the base environment using a single NUC computer.  Once that environment is setup, return here for the next steps.

## Building and Configure the VMs
The first step is to bring up all the needed VMs.  This is composed of 3 mesh network perfSONAR nodes, a fourth node for the Central Managment and MaDDash servers.  To minimize steps, we'll also bring up the 3 nodes used for the disjoint grid discussed later.
```
curl -L https://github.com/preese/perfSONAR-Sampler/archive/main.tar.gz | tar xzf -
cd perfSONAR-Sampler-main

vi Vagrantfile
   (Using your chart, edit this file, and all the others mentioned, if you changed the
   IP numbers I was using.)
```

Start the VMs:
```
vagrant up --provider libvirt
```
Use Ansible to configure the nodes for persSONAR and MaDDash use.
```
cd ansible-yml-files
ansible-playbook Testpoint-MaDDashbuild.yml -i hosts
   (This is a SLOW process, the command typically takes about 13 min to 
   complete!  Many things are packed into this playbook.  The testpoints 
   and MD servers are built, provisioned and enabled.  The web page should 
   have grids on it when visited.)
```

You should be able to vist the MaDDash server URL at this point.  In the stock case it would be **http://192.168.1.213/maddash-webui**, (change to your IP from the Chart).

Let the project run for a couple of hours.  If all went well, you should see the grid start to populate

When you are happy with the results, add in the disjoint grid.

## Add second dashboard page and integrate the disjoint nodes
```
ansible-playbook Maddash-dj.yml -i hosts
   (this configures the MaDDash host to accept traffic from additional 
   nodes and show sesults on a second dashboard.  It also configures the testpoint nodes
   for the additionsl disjoint dashboard)
   (NOTE: ALL the hosts are sent both .json file links, though only those
   involved will do the tests)
