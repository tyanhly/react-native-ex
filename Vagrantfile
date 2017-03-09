# -*- mode: ruby -*-
# vi: set ft=ruby :

# required vagrant plugins
# - vagrant-rsync-back
# - vagrant-gatling-rsync

Vagrant.configure(2) do |config|
  config.vm.box = "react_native_cli"
  config.vm.box_url = "https://atlas.hashicorp.com/centos/boxes/7/versions/1611.01/providers/virtualbox.box"

  config.ssh.insert_key = false

  if Vagrant.has_plugin?("vagrant-vbguest") then
    config.vbguest.auto_update = true
  end

  config.vm.network "private_network", ip: "10.10.10.112"
  # config.vm.network "public_network"

  config.vm.synced_folder ".", "/vagrant", mount_options: ["dmode=776,fmode=777"], type: "virtualbox"

  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = false

    # Customize the amount of memory on the VM:
    vb.cpus = 2
    vb.memory = "2048"
    vb.customize ["modifyvm", :id, "--ioapic", "on"]
    vb.customize ["modifyvm", :id, "--memory", 2048]
  end

  config.vm.provision "shell", inline: <<-EOC

yum install -y deltarpm

yum install -y epel-release

yum groupinstall "Development tools"

yum -y update

yum -y install git

curl --silent --location https://rpm.nodesource.com/setup_7.x | bash

yum -y install nodejs

npm install -g react-native-cli

echo "cd /vagrant" >> /home/vagrant/.bashrc

  EOC

end
