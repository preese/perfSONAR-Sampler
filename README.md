# perfSONAR-Sampler
This project illustrates, using VMs, what the document 'MaDDash and perfSONAR install' covers bit by bit.  

Andy Lake put together the first version of this document several years ago.  That prompted an AHA! moment for me.  This project is an attempt to share that AHA! with others looking to better understand the perfSONAR and MaDDash projects.

The project pulls together .json files and vagrant and ansible files to move from a number of bare VMs to a working perfSONAR and MaDDash grid.  It doesn't show real network tests but rather shows how the project's files could be used on real hardware to develop a grid of perfSONAR nodes reporting to a MaDDash server's web page.

It also shows how to setup a second grid page and shows a disjoint grid rather than the more traditional mesh grid.

The Wiki page for the project details how setup the base environment using a single NUC computer.  Once that environment is setup, return here for the next steps.

##Building the VMs
The first step is to bring up all the needed VMs.  This is composed for 3 perfSONAR nodes for a mesh network using a fourth node for the Central Managment and MaDDash servers.  To minimize steps, we'll just bring up all the needed VMs for the first mesh grid and the second disjoint grid.
```
git clone https://github.com/preese/perfSONAR-Sampler.git
cd perfSONAR-Sampler
vi Vagrantfile
   (edit the file to replace any MAC addr, IP and specifically the name of the second ethernet port)
```

Start the VMs:
```
vagrant up --provider libvirt
```

Go get your favorite beverage!

Fix up any issues that may present themselves.

```
cd ansible-yml-files
edit the 'hosts' file if needed to reflect any name changes you may have made
ansible-playbook nodes.yml -i hosts -l vm
  (this loads up the edge nodes with needed rpms)
ansible-playbook mesh.yml -i hosts -l vm
```

The three edge nodes are ready to go now.  

Configure the MaDDash host now.

```
ansible-playbook maddash.yml -i hosts -l md,dj
   (this is where most of Andy's document is implemented)
   (take a good look a this file, at the end, the time frames for two tests, 
   RTT and Throughput are made shorter)
```

You should be able to visi the MaDDash server URL at this point.  In the stock case it would be **http://md.ufixu.com/maddash-webui**

Let the project run for a couple of hours.   If all went well, you should see the grid start to populate.

When you are happy with the results, add in the disjoint grid.

```
ansible-playbook maddash-dj.yml -i  hosts -l md
   (this configures the MaDDash host to accept traffic from a second grid and how to show it on the web page)
ansible-playbook disjoing.yml -i hosts -l dj,vm
   (configure all the edge nodes with a second set of tasks to perform)
   (note that ALL the hosts are sent both task .json URLs)
```
   
