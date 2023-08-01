# -*- mode: ruby -*-
# vi: set ft=ruby :

nodes = [
  {:hostname => 'ps1',  :mac => "525400836f51" },
  {:hostname => 'ps2',  :mac => "525400836f52" },
  {:hostname => 'ps3',  :mac => "525400836f53" },
  {:hostname => 'md',   :mac => "525400836f54" }
]

Vagrant.configure("2") do |config|
   nodes.each do |node|
    config.vm.define node[:hostname] do |config|
	  config.vm.box = "centos/7"
	  config.vm.network :public_network, :mac => node[:mac], bridge: "enp0s20f0u2"
    config.vm.provision "file", source: "/home/vagrant/.ssh/id_ed25519.pub", destination: "/home/vagrant/.ssh/authorized_keys"
   config.vm.hostname = node[:hostname]
	  config.vm.provider :virtualbox do |domain|
		  domain.memory = 2048
		  domain.cpus = 1
         end
       end
    end
        config.vm.provision "ansible" do |ansible|
          ansible.compatibility_mode = "2.0"
          ansible.groups = {
            "testpoint" => ["ps1", "ps2", "ps3"],
            "md"        => ["md"],
            }
          ansible.playbook = "Testpoint-MaDDashbuild.yml"
    end
end
