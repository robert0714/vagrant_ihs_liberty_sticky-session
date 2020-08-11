# -*- mode: ruby -*-
# vi: set ft=ruby :

require "fileutils"


VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  if (/cygwin|mswin|mingw|bccwin|wince|emx/ =~ RUBY_PLATFORM) != nil
    config.vm.synced_folder ".", "/vagrant", mount_options: ["dmode=700,fmode=600"]
  else
    config.vm.synced_folder ".", "/vagrant"
  end
  (1..2).each do |i|
    config.vm.define "his-n#{i}" do |d|
      d.vm.box = "tas50/windows_2016"
	  #d.vm.box = "StefanScherer/windows_2019"
	  d.vm.guest = :windows
	  d.vm.box_check_update = true
      d.vm.hostname = "his-n#{i}" 
      d.vm.network "private_network", ip: "10.0.30.11#{i}" 
      d.windows.set_work_network = true
	  #d.winrm.username = "Administrator"
      #d.winrm.password = "vagrant"
	  
	  # Port forward WinRM and RDP
      #d.vm.network :forwarded_port, guest: 3389, host: 3389
      #d.vm.network :forwarded_port, guest: 5985, host: 5985, id: "winrm", auto_correct: true
      d.vm.provider "virtualbox" do |vb|
        # Don't boot with headless mode
		vb.gui = false
		# Use VBoxManage to customize the VM. For example to change memory:
		#vb.customize ["modifyvm", :id, "--memory", "4096"]
		vb.customize ["modifyvm", :id, "--memory", "1700"]
		vb.customize ["modifyvm", :id, "--cpus",   "2"]
      end
    end
  end
  (1..2).each do |i|
    config.vm.define "liberty-n#{i}" do |d|
	  d.vm.box = "StefanScherer/windows_2019"
	  d.vm.guest = :windows
	  d.vm.box_check_update = true
      d.vm.hostname = "liberty-n#{i}" 
      d.vm.network "private_network", ip: "10.0.30.10#{i}" 
      d.windows.set_work_network = true
	  #d.winrm.username = "Administrator"
      #d.winrm.password = "vagrant"
	  
	  # Port forward WinRM and RDP
      #d.vm.network :forwarded_port, guest: 3389, host: 3389
      #d.vm.network :forwarded_port, guest: 5985, host: 5985, id: "winrm", auto_correct: true
      d.vm.provider "virtualbox" do |vb|
        # Don't boot with headless mode
		vb.gui = false
		# Use VBoxManage to customize the VM. For example to change memory:
		vb.customize ["modifyvm", :id, "--memory", "1748"]
		vb.customize ["modifyvm", :id, "--cpus",   "2"]
      end
    end
  end
  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end
  if Vagrant.has_plugin?("vagrant-vbguest")
    config.vbguest.auto_update = false
    config.vbguest.no_install = true
    config.vbguest.no_remote = true
  end
end
