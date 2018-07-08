# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false


  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL

Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.


  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.define "control" do |control|

  control.vm.box = "ubuntu/xenial64"
 # acs.vm.provision "file", source: "/home/galal/.vagrant.d/insecure_private_key", destination: "~/.ssh/authorized_keys"
 config.vm.provision "file", source: "id_rsa", destination: "/home/vagrant/.ssh/id_rsa"
 public_key = File.read("id_rsa.pub")
 config.vm.provision :shell, :inline =>"
    echo 'Copying ansible-vm public SSH Keys to the VM'
    mkdir -p /home/vagrant/.ssh
    chmod 700 /home/vagrant/.ssh
    echo '#{public_key}' >> /home/vagrant/.ssh/authorized_keys
    chmod -R 600 /home/vagrant/.ssh/authorized_keys
    echo 'Host 192.168.*.*' >> /home/vagrant/.ssh/config
    echo 'StrictHostKeyChecking no' >> /home/vagrant/.ssh/config
    echo 'UserKnownHostsFile /dev/null' >> /home/vagrant/.ssh/config
    chmod -R 600 /home/vagrant/.ssh/config
    ", privileged: false

	control.vm.hostname = "control"
  control.vm.network "private_network", ip: "192.168.56.25" , virtualbox__intnet: true
  control.vm.provision "shell", inline: <<-SHELL
  sudo apt-get update
  sudo apt install ansible -y
 
  
  SHELL

  

	end
 config.vm.define "app1" do |app1|
  app1.vm.box = "ubuntu/xenial64"
  config.vm.provision "file", source: "id_rsa", destination: "/home/vagrant/.ssh/id_rsa"
  public_key = File.read("id_rsa.pub")
  config.vm.provision :shell, :inline =>"
     echo 'Copying ansible-vm public SSH Keys to the VM'
     mkdir -p /home/vagrant/.ssh
     chmod 700 /home/vagrant/.ssh
     echo '#{public_key}' >> /home/vagrant/.ssh/authorized_keys
     chmod -R 600 /home/vagrant/.ssh/authorized_keys
     echo 'Host 192.168.*.*' >> /home/vagrant/.ssh/config
     echo 'StrictHostKeyChecking no' >> /home/vagrant/.ssh/config
     echo 'UserKnownHostsFile /dev/null' >> /home/vagrant/.ssh/config
     chmod -R 600 /home/vagrant/.ssh/config
     ", privileged: false
  
	app1.vm.hostname = "app1"
  app1.vm.network "private_network", ip: "192.168.56.21" ,  virtualbox__intnet: true
  app1.vm.network "forwarded_port", guest: 80, host: 8081

	end
  


  config.vm.define "app2" do |app2|
    app2.vm.box = "ubuntu/xenial64"
    config.vm.provision "file", source: "id_rsa", destination: "/home/vagrant/.ssh/id_rsa"
    public_key = File.read("id_rsa.pub")
    config.vm.provision :shell, :inline =>"
       echo 'Copying ansible-vm public SSH Keys to the VM'
       mkdir -p /home/vagrant/.ssh
       chmod 700 /home/vagrant/.ssh
       echo '#{public_key}' >> /home/vagrant/.ssh/authorized_keys
       chmod -R 600 /home/vagrant/.ssh/authorized_keys
       echo 'Host 192.168.*.*' >> /home/vagrant/.ssh/config
       echo 'StrictHostKeyChecking no' >> /home/vagrant/.ssh/config
       echo 'UserKnownHostsFile /dev/null' >> /home/vagrant/.ssh/config
       chmod -R 600 /home/vagrant/.ssh/config
       ", privileged: false
    
    app2.vm.hostname = "app2"
    app2.vm.network "private_network", ip: "192.168.56.22" ,  virtualbox__intnet: true
    app2.vm.network "forwarded_port", guest: 80, host: 8082
  
    end

    
  config.vm.define "lb1" do |lb1|
    lb1.vm.box = "ubuntu/xenial64"
    config.vm.provision "file", source: "id_rsa", destination: "/home/vagrant/.ssh/id_rsa"
    public_key = File.read("id_rsa.pub")
    config.vm.provision :shell, :inline =>"
       echo 'Copying ansible-vm public SSH Keys to the VM'
       mkdir -p /home/vagrant/.ssh
       chmod 700 /home/vagrant/.ssh
       echo '#{public_key}' >> /home/vagrant/.ssh/authorized_keys
       chmod -R 600 /home/vagrant/.ssh/authorized_keys
       echo 'Host 192.168.*.*' >> /home/vagrant/.ssh/config
       echo 'StrictHostKeyChecking no' >> /home/vagrant/.ssh/config
       echo 'UserKnownHostsFile /dev/null' >> /home/vagrant/.ssh/config
       chmod -R 600 /home/vagrant/.ssh/config
       ", privileged: false
    
    lb1.vm.hostname = "lb1"
    lb1.vm.network "private_network", ip: "192.168.56.20" ,  virtualbox__intnet: true
    lb1.vm.network "forwarded_port", guest: 80, host: 8080
  
    end

  config.vm.define "db" do |db|
  db.vm.box = "ubuntu/xenial64"
  config.vm.provision "file", source: "id_rsa", destination: "/home/vagrant/.ssh/id_rsa"
  public_key = File.read("id_rsa.pub")
  config.vm.provision :shell, :inline =>"
     echo 'Copying ansible-vm public SSH Keys to the VM'
     mkdir -p /home/vagrant/.ssh
     chmod 700 /home/vagrant/.ssh
     echo '#{public_key}' >> /home/vagrant/.ssh/authorized_keys
     chmod -R 600 /home/vagrant/.ssh/authorized_keys
     echo 'Host 192.168.*.*' >> /home/vagrant/.ssh/config
     echo 'StrictHostKeyChecking no' >> /home/vagrant/.ssh/config
     echo 'UserKnownHostsFile /dev/null' >> /home/vagrant/.ssh/config
     chmod -R 600 /home/vagrant/.ssh/config
     ", privileged: false

 	db.vm.hostname = "db"
  db.vm.network "private_network", ip: "192.168.56.23" ,  virtualbox__intnet: true
 
  end
end
 

