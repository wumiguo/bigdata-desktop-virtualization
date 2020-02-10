# -*- mode: ruby -*-
# vi: set ft=ruby :

#config with version "2"
Vagrant.configure("2") do |config|
  #config.vm.box = "centos/7"
  config.vm.box = "hashicorp/precise64"
  config.vm.box_check_update = false
  config.vm.provider :virtualbox do |vb|
    vb.name = "bigdata-desktop-virtual-node"
  end
  
  #disable the box auto update checking
  #config.vm.box_check_update = false

  config.vm.provider :virtualbox do |vb| 
    vb.memory = "8096"
    vb.customize ['modifyvm', :id, '--cableconnected1', 'on']
    file_to_disk = File.join(File.dirname(__FILE__), '.vagrant', 'reside.vdi')
    unless File.exists? file_to_disk
      vb.customize ['createhd', '--filename', file_to_disk, '--size', 100 * 1024]
    end

    vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 1,'--device', 0, '--type', 'hdd', '--medium', file_to_disk]
  end

  config.vm.provision "shell", path: "src/provisionOs.sh"
end
