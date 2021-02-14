# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.ps.define "ps1" do |config|
	  config.ps.box = "centos/7"
	  config.ps.network :public_network, :dev => "enp0s20f0u2", :mode => "bridge", :mac => "52:54:00:73:6f:41"
      config.ps.provision "file", source: "/home/vagrant/.ssh/id_ed25519.pub", destination: "/home/vagrant/.ssh/authorized_keys"
	  config.ps.provision "shell", inline: "hostnamectl set-hostname --static 'ps1.ufixu.com'"
	  config.ps.provider :libvirt do |domain|
		  domain.memory = 2048
		  domain.cpus = 1
		  domain.storage_pool_name = "default"
	  end
	end

    config.ps.define "ps2" do |config|
	  config.ps.box = "centos/7"
	  config.ps.network :public_network, :dev => "enp0s20f0u2", :mode => "bridge", :mac => "52:54:00:73:6f:42"
      config.ps.provision "file", source: "/home/vagrant/.ssh/id_ed25519.pub", destination: "/home/vagrant/.ssh/authorized_keys"
	  config.ps.provision "shell", inline: "hostnamectl set-hostname --static 'ps2.ufixu.com'"
	  config.ps.provider :libvirt do |domain|
		  domain.memory = 2048
		  domain.cpus = 1
		  domain.storage_pool_name = "default"
	  end
	end

    config.ps.define "ps3" do |config|
	  config.ps.box = "centos/7"
	  config.ps.network :public_network, :dev => "enp0s20f0u2", :mode => "bridge", :mac => "52:54:00:73:6f:43"
      config.ps.provision "file", source: "/home/vagrant/.ssh/id_ed25519.pub", destination: "/home/vagrant/.ssh/authorized_keys"
	  config.ps.provision "shell", inline: "hostnamectl set-hostname --static 'ps3.ufixu.com'"
	  config.ps.provider :libvirt do |domain|
		  domain.memory = 2048
		  domain.cpus = 1
		  domain.storage_pool_name = "default"
	  end
	end

    config.ps.define "md" do |config|
	  config.ps.box = "centos/7"
	  config.ps.network :public_network, :dev => "enp0s20f0u2", :mode => "bridge", :mac => "52:54:00:73:6f:44"
      config.ps.provision "file", source: "/home/vagrant/.ssh/id_ed25519.pub", destination: "/home/vagrant/.ssh/authorized_keys"
	  config.ps.provision "shell", inline: "hostnamectl set-hostname --static 'md.ufixu.com'"
	  config.ps.provider :libvirt do |domain|
		  domain.memory = 2048
		  domain.cpus = 1
		  domain.storage_pool_name = "default"
	  end
	end

    config.ps.define "dj1" do |config|
	  config.ps.box = "centos/7"
	  config.ps.network :public_network, :dev => "enp0s20f0u2", :mode => "bridge", :mac => "52:54:00:73:6f:45"
      config.ps.provision "file", source: "/home/vagrant/.ssh/id_ed25519.pub", destination: "/home/vagrant/.ssh/authorized_keys"
	  config.ps.provision "shell", inline: "hostnamectl set-hostname --static 'dj1.ufixu.com'"
	  config.ps.provider :libvirt do |domain|
		  domain.memory = 2048
		  domain.cpus = 1
		  domain.storage_pool_name = "default"
	  end
	end

    config.ps.define "dj2" do |config|
	  config.ps.box = "centos/7"
	  config.ps.network :public_network, :dev => "enp0s20f0u2", :mode => "bridge", :mac => "52:54:00:73:6f:46"
      config.ps.provision "file", source: "/home/vagrant/.ssh/id_ed25519.pub", destination: "/home/vagrant/.ssh/authorized_keys"
	  config.ps.provision "shell", inline: "hostnamectl set-hostname --static 'dj2.ufixu.com'"
	  config.ps.provider :libvirt do |domain|
		  domain.memory = 2048
		  domain.cpus = 1
		  domain.storage_pool_name = "default"
	  end
	end

    config.ps.define "dj3" do |config|
	  config.ps.box = "centos/7"
	  config.ps.network :public_network, :dev => "enp0s20f0u2", :mode => "bridge", :mac => "52:54:00:73:6f:47"
      config.ps.provision "file", source: "/home/vagrant/.ssh/id_ed25519.pub", destination: "/home/vagrant/.ssh/authorized_keys"
	  config.ps.provision "shell", inline: "hostnamectl set-hostname --static 'dj3.ufixu.com'"
	  config.ps.provider :libvirt do |domain|
		  domain.memory = 2048
		  domain.cpus = 1
		  domain.storage_pool_name = "default"
	  end
	end
end
