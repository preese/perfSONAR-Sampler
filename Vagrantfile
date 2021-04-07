# -*- mode: ruby -*-
# vi: set ft=ruby :

nodes = [
  {:hostname => 'ps1', :ip => "192.168.1.210", :mac => "52:54:00:83:6f:41", :dev => "enp0s20f0u2" },
  {:hostname => 'ps2', :ip => "192.168.1.211", :mac => "52:54:00:83:6f:42", :dev => "enp0s20f0u2" },
  {:hostname => 'ps3', :ip => "192.168.1.212", :mac => "52:54:00:83:6f:43", :dev => "enp0s20f0u2" },
  {:hostname => 'md', :ip => "192.168.1.213", :mac => "52:54:00:83:6f:44", :dev => "enp0s20f0u2" },
  {:hostname => 'dj1', :ip => "192.168.1.214", :mac => "52:54:00:83:6f:45", :dev => "enp0s20f0u2" },
  {:hostname => 'dj2', :ip => "192.168.1.215", :mac => "52:54:00:83:6f:46", :dev => "enp0s20f0u2" },
  {:hostname => 'dj3', :ip => "192.168.1.216", :mac => "52:54:00:83:6f:47", :dev => "enp0s20f0u2" }
]

Vagrant.configure("2") do |config|
   nodes.each do |node|
    config.vm.define node[:hostname] do |config|
	  config.vm.box = "centos/7"
	  config.vm.network :public_network, :dev => node[:dev], :mode => "bridge", :mac => node[:mac], :ip => node[:ip]
      config.vm.provision "file", source: "/home/vagrant/.ssh/id_ed25519.pub", destination: "/home/vagrant/.ssh/authorized_keys"
      config.vm.hostname = node[:hostname]
	  config.vm.provider :libvirt do |domain|
		  domain.memory = 2048
		  domain.cpus = 1
		  domain.storage_pool_name = "default"
      end
	 end
    end
end
