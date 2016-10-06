# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.

  config.vm.define "local" do |local|
    local.vm.box = "ubuntu/xenial64"

    
    local.vm.network "private_network", ip: "192.168.55.5"

    local.vm.provider "virtualbox" do |vb|
      # Display the VirtualBox GUI when booting the machine
      vb.gui = false

      # Customize the amount of memory on the VM:
      vb.memory = "1024"
      vb.cpus = 2
    end

    local.vm.provision "ansible" do |ansible|
      ansible.playbook = "tests/test.yml"
      ansible.verbose = "v"
    end


  end

  config.vm.define "ec2" do |ec2|
    ec2.vm.box = "dummy"

    ec2.vm.provider :aws do |aws, override|
      aws.access_key_id = ENV["ACCESS_KEY_ID"]
      aws.secret_access_key = ENV["SECRET_ACCESS_KEY"]

      aws.instance_type = 'p2.xlarge'
      aws.security_groups = ['cordial_consumer']
      aws.terminate_on_shutdown = true

      aws.ami = "ami-2ef48339"

      override.ssh.username = "ubuntu"
      override.ssh.private_key_path = ENV["SSH_KEY_PATH"]
    end

    ec2.vm.provision "ansible" do |ansible|
      ansible.playbook = "tests/test.yml"
      ansible.verbose = "v"
    end


  end

 
end
