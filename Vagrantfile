# -*- mode: ruby -*-
# vi: set ft=ruby :

nodes = [
  { :hostname => "ps1", :mac => "525400836f51", :ram => 2048 },
  { :hostname => "ps2", :mac => "525400836f52", :ram => 2048 },
  { :hostname => "ps3", :mac => "525400836f53", :ram => 2048 },
  { :hostname => "md", :mac => "525400836f54", :ram => 4096 }
]

Vagrant.configure("2") do |config|
  nodes.each do |node|
    config.vm.define node[:hostname] do |node_config|
      node_config.vm.box = "centos/7"
      node_config.vm.network :public_network, :mac => node[:mac], bridge: "enp0s20f0u2"
      node_config.vm.provision "file", source: "/home/vagrant/.ssh/id_ed25519.pub", destination: "/home/vagrant/.ssh/authorized_keys"

      node_config.vm.hostname = node[:hostname]
      node_config.vm.provider :virtualbox do |domain|
        domain.memory = node[:ram]
        domain.cpus = 1
      end
    end
  end

  config.vm.provision "ansible" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "Testpoint-MaDDashbuild.yml"
    ansible.groups = {
      "testpoint" => ["ps1", "ps2", "ps3"],
      "md-arch"   => ["md"]
    }
  end
end
