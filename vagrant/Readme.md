# vagrant
- Download VirtualBox - I am using VB as VM provider for vagrant
  https://www.virtualbox.org/wiki/Downloads
- Download Vagrant - Download for any OS
  https://www.vagrantup.com/downloads.html
- vagrant box search
  https://app.vagrantup.com/boxes/search

## vagrant commands
    [user]$ mkdir VM1
    [user]$ cd VM1
    [user]$ vagrant box add centos/7 => Add image to the system
    [user]$ vagrant box list => List all images added in the system
    [user]$ vagrant init centos/7
    [user]$ vagrant up
    [user]$ vagrant status
    [user]$ Once UP - you will find VM in Virutal Box application
    [user]$ vagrant up <VM name> to bring up the VMs
    [user]$ vagrant ssh <VM name> to SSH to VMs
    [user]$ vagrant halt <VM> to halt the VMs
    [user]$ vagrant suspend <VM> to suspend
    [user]$ vagrant resume <VM> to resume
    [user]$ vagrant destroy <VM> to remove the image and destroy the VM
    [user]$ vagrant status to list all VMs
    [user]$ vagrant reload to reload VMs after a config.

## Sample Config: Simple VM
    Vagrant.configure(2) do |configure| 
    	config.vm.box = "centos/7"
    	config.hostname = "linuxsrv1"
    	config.vm.network "private network", ip: "191.168.1.10"
    	#config.provision "shell", path: "setup.sh"
    	#config.vm.provider "virtualbox" do |vb|
    		#vb.gui = true
    		#vb.memory = "1024"
    	#end
    end

## Multi VM with one image
    Vagrant.configure(2) do |configure| 
    	config.vm.box = "centos/7"
    	config.vm.define "server1" do |server1|
    		server1.vm.hostname = "server1"
    		server1.vm.network "private network", ip: "190.168.1.10"
    	end
    	config.vm.define "server1" do |server2|
    		server1.vm.hostname = "server2"
    		server1.vm.network "private network", ip: "190.168.1.12"
    	end
    end

## Cable connection
    config.vm.provider "virtualbox" do |vb|
    	vb.customize ['modifyvm', :id, '--cableconnected1', 'on']
    end

## Enable GUI desktop - Ubuntu
    sudo apt update
    sudo apt-get install xfce4
    sudo startxfce4&
    
## Run Shell command during first startup
    config.vm.provision "shell", inline: "sudo apt-get update"
