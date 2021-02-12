# perfSONAR-Sampler
This project illustrates, using VMs, what the document 'MaDDash and perfSONAR install' covers bit by bit. (see https://docs.google.com/document/d/1k7FT66MKPy3JjpD5k0OFAFlTpSdFmZ6huhTUDQ2rGGY/edit?usp=sharing)

Andy Lake put together the first version of this document several years ago.  That prompted an AHA! moment for me.  This project is an attempt to share that AHA! with others looking to better understand the perfSONAR and MaDDash projects.

The project pulls together .json, vagrant and ansible files to move from a number of bare VMs to a working perfSONAR and MaDDash grid.  It doesn't show real network tests but just traffic between the different VMs on the single host.  The project files can be used on real hardware to develop a grid of perfSONAR nodes reporting to a MaDDash server's web page.

It also shows how to setup a second grid page showing a disjoint grid rather than the more traditional mesh grid.

The Wiki page for the project details how setup the base environment using a single NUC computer.  Once that environment is setup, return here for the next steps.

## Building the VMs
The first step is to bring up all the needed VMs.  This is composed for 3 mesh network perfSONAR nodes, a fourth node for the Central Managment and MaDDash servers.  To minimize steps, we'll just bring up 3 nodes used for the disjoint grid.
```
git clone https://github.com/preese/perfSONAR-Sampler.git
cd perfSONAR-Sampler
vi Vagrantfile
   (edit the file to replace any MAC addr, IP and specifically the name of the second
   ethernet port)
```

Start the VMs:
```
vagrant up --provider libvirt
```

Go get your favorite beverage!

Fix up any issues that may present themselves.

## Use Ansible to configure the VMs
```
cd ansible-yml-files
   (edit the 'hosts' file if needed to reflect any name changes you may have made)
ansible-playbook nodes.yml -i hosts -l ps,dj
   (this loads up the edge nodes with needed rpms)
ansible-playbook mesh.yml -i hosts -l ps,dj
   (sets up 'work' that the nodes will do and report to the MaDDash VM)
```

The three edge nodes (and the 3 disjoint nodes) are ready to go now.  

Configure the MaDDash host now.
```
ansible-playbook maddash.yml -i hosts -l mad
   (this is where most of Andy's document is implemented)
   (at the end of this file, the time frames for two tests, 
   RTT and Throughput are shortened)
```

You should be able to vist the MaDDash server URL at this point.  In the stock case it would be **http://md.ufixu.com/maddash-webui**

Let the project run for a couple of hours.   If all went well, you should see the grid start to populate.

When you are happy with the results, add in the disjoint grid.

## Add second grid page and integrate the disjoint mesh
```
ansible-playbook maddash-dj.yml -i hosts -l mad
   (this configures the MaDDash host to accept traffic from a second grid 
   and how to show it on the web page)
ansible-playbook disjoint.yml -i hosts -l dj,ps
   (configure all the edge nodes with a second set of tasks to perform)
   (note that ALL the hosts are sent both task .json URLs)
```


