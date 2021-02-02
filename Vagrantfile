# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.vm.define "vm1" do |config|
	  config.vm.box = "centos/7"
	  config.vm.network :public_network, :dev => "enp2s0", :mode => "bridge", :mac => "52:54:00:73:6f:41"
      config.vm.provision "file", source: "/home/vagrant/.ssh/id_ed25519.pub", destination: "/home/vagrant/.ssh/authorized_keys"
	  config.vm.provision "shell", inline: "hostnamectl set-hostname --static 'vm1.ufixu.com'"
	  config.vm.provider :libvirt do |domain|
		  domain.memory = 2048
		  domain.cpus = 1
		  domain.storage_pool_name = "default"
	  end
	end

    config.vm.define "vm2" do |config|
	  config.vm.box = "centos/7"
	  config.vm.network :public_network, :dev => "enp2s0", :mode => "bridge", :mac => "52:54:00:73:6f:42"
      config.vm.provision "file", source: "/home/vagrant/.ssh/id_ed25519.pub", destination: "/home/vagrant/.ssh/authorized_keys"
	  config.vm.provision "shell", inline: "hostnamectl set-hostname --static 'vm2.ufixu.com'"
	  config.vm.provider :libvirt do |domain|
		  domain.memory = 2048
		  domain.cpus = 1
		  domain.storage_pool_name = "default"
	  end
	end

    config.vm.define "vm3" do |config|
	  config.vm.box = "centos/7"
	  config.vm.network :public_network, :dev => "enp2s0", :mode => "bridge", :mac => "52:54:00:73:6f:43"
      config.vm.provision "file", source: "/home/vagrant/.ssh/id_ed25519.pub", destination: "/home/vagrant/.ssh/authorized_keys"
	  config.vm.provision "shell", inline: "hostnamectl set-hostname --static 'vm3.ufixu.com'"
	  config.vm.provider :libvirt do |domain|
		  domain.memory = 2048
		  domain.cpus = 1
		  domain.storage_pool_name = "default"
	  end
	end

    config.vm.define "md" do |config|
	  config.vm.box = "centos/7"
	  config.vm.network :public_network, :dev => "enp2s0", :mode => "bridge", :mac => "52:54:00:73:6f:44"
      config.vm.provision "file", source: "/home/vagrant/.ssh/id_ed25519.pub", destination: "/home/vagrant/.ssh/authorized_keys"
	  config.vm.provision "shell", inline: "hostnamectl set-hostname --static 'md.ufixu.com'"
	  config.vm.provider :libvirt do |domain|
		  domain.memory = 2048
		  domain.cpus = 1
		  domain.storage_pool_name = "default"
	  end
	end

    config.vm.define "dj1" do |config|
	  config.vm.box = "centos/7"
	  config.vm.network :public_network, :dev => "enp2s0", :mode => "bridge", :mac => "52:54:00:73:6f:45"
      config.vm.provision "file", source: "/home/vagrant/.ssh/id_ed25519.pub", destination: "/home/vagrant/.ssh/authorized_keys"
	  config.vm.provision "shell", inline: "hostnamectl set-hostname --static 'dj1.ufixu.com'"
	  config.vm.provider :libvirt do |domain|
		  domain.memory = 2048
		  domain.cpus = 1
		  domain.storage_pool_name = "default"
	  end
	end

    config.vm.define "dj2" do |config|
	  config.vm.box = "centos/7"
	  config.vm.network :public_network, :dev => "enp2s0", :mode => "bridge", :mac => "52:54:00:73:6f:46"
      config.vm.provision "file", source: "/home/vagrant/.ssh/id_ed25519.pub", destination: "/home/vagrant/.ssh/authorized_keys"
	  config.vm.provision "shell", inline: "hostnamectl set-hostname --static 'dj2.ufixu.com'"
	  config.vm.provider :libvirt do |domain|
		  domain.memory = 2048
		  domain.cpus = 1
		  domain.storage_pool_name = "default"
	  end
	end

    config.vm.define "dj3" do |config|
	  config.vm.box = "centos/7"
	  config.vm.network :public_network, :dev => "enp2s0", :mode => "bridge", :mac => "52:54:00:73:6f:47"
      config.vm.provision "file", source: "/home/vagrant/.ssh/id_ed25519.pub", destination: "/home/vagrant/.ssh/authorized_keys"
	  config.vm.provision "shell", inline: "hostnamectl set-hostname --static 'dj3.ufixu.com'"
	  config.vm.provider :libvirt do |domain|
		  domain.memory = 2048
		  domain.cpus = 1
		  domain.storage_pool_name = "default"
	  end
	end
end
