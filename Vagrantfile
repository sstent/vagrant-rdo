# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure('2') do |config|

  #
  # Boxes to use.
  # 

  # Puppet Labs CentOS 6.4 for VirtualBox
  config.vm.provider :virtualbox do |virtualbox, override|
    override.vm.box     = 'puppetlabs-centos-65-x64-vbox'
    override.vm.box_url = 'http://puppet-vagrant-boxes.puppetlabs.com/centos-65-x64-virtualbox-puppet.box'
  end

  #
  # Define the Foreman server
  # 
  config.vm.define "foreman", primary: true do |foreman|

    # Forward standard ports (local only, does not run under AWS)    
    foreman.vm.network :forwarded_port, guest: 80,  host: 8080, auto_correct: true
    foreman.vm.network :forwarded_port, guest: 443, host: 8443, auto_correct: true

    # provide a 2nd network
    foreman.vm.network "private_network", ip: "192.168.1.2", virtualbox__intnet: "private"

    # Run shell provisioner
    foreman.vm.provision :shell, :path => 'bootstrap/foreman.sh'
  end


  #
  # Define the Controller server
  # 

  config.vm.define "controller1", primary: true do |controller|

    controller.vm.network :forwarded_port, guest: 80,  host: 9080, auto_correct: true
    controller.vm.network :forwarded_port, guest: 443, host: 9443, auto_correct: true
    controller.vm.network :forwarded_port, guest: 5000,  host: 5000, auto_correct: true
    controller.vm.network :forwarded_port, guest: 35357,  host: 35357, auto_correct: true 
    controller.vm.network :forwarded_port, guest: 9292,  host: 9292, auto_correct: true
    controller.vm.network :forwarded_port, guest: 8773,  host: 8773, auto_correct: true  
    controller.vm.network :forwarded_port, guest: 8774,  host: 8774, auto_correct: true  
    controller.vm.network :forwarded_port, guest: 8775,  host: 8775, auto_correct: true  
    controller.vm.network :forwarded_port, guest: 8776,  host: 8776, auto_correct: true 
    controller.vm.network :forwarded_port, guest: 8777,  host: 8777, auto_correct: true 
    controller.vm.network :forwarded_port, guest: 6080,  host: 6080, auto_correct: true 
    controller.vm.network :forwarded_port, guest: 9696,  host: 9696, auto_correct: true    
    controller.vm.network :forwarded_port, guest: 8000,  host: 8000, auto_correct: true
    controller.vm.network :forwarded_port, guest: 8004,  host: 8004, auto_correct: true

    # provide a 2nd network
    controller.vm.network "private_network", ip: "192.168.1.3", virtualbox__intnet: "private"

    # Run shell provisioner
    controller.vm.provision :shell, :path => 'bootstrap/node.sh', :args => 'controller'
  end

  config.vm.define "controller2", primary: true do |controller|
    controller.vm.network "private_network", ip: "192.168.1.4", virtualbox__intnet: "private"
    controller.vm.provision :shell, :path => 'bootstrap/node.sh', :args => 'controller'
  end


  config.vm.define "controller3", primary: true do |controller|
    controller.vm.network "private_network", ip: "192.168.1.5", virtualbox__intnet: "private"
    controller.vm.provision :shell, :path => 'bootstrap/node.sh', :args => 'controller'
  end



  #
  # Define the Compute server
  # 

  config.vm.define "compute", primary: true do |compute|
    compute.vm.network "private_network", ip: "192.168.1.6", virtualbox__intnet: "private"
    compute.vm.provision :shell, :path => 'bootstrap/node.sh', :args => 'compute'
  end

  #
  # Define a 2nd Compute server
  # 

  # config.vm.define "compute2", primary: true do |compute|

  #   compute2.vm.network "private_network", ip: "192.168.1.7", virtualbox__intnet: "private"
  #   compute2.vm.provision :shell, :path => 'bootstrap/node.sh', :args => 'compute2'
  # end


end
