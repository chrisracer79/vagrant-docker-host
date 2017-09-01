# -*- mode: ruby -*-
# vi: set ft=ruby :

# Author : Christopher Parent
# Email  : chris@learnweblogiconline.com
# Date   : 08-30-2017

# This Vagrantfile will create a CentOS 7 virtual machine running Docker.
# It installs all the necessary repos and packages required by docker,
# including git.  The Vagrantfile also configures several port forwards that
# can be used for the admin server and some number of managed servers.

Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.provider "virtualbox" do |v|
    v.memory = 1024
    v.cpus = 2
  end

  config.vm.box = "centos/7"
  #config.vm.synced_folder "share/", "/home/vagrant"

  # Setting up some port forwards for admin server and 3 managed servers
  config.vm.network "forwarded_port", guest: 7001, host: 7001
  config.vm.network "forwarded_port", guest: 7002, host: 7002
  config.vm.network "forwarded_port", guest: 7003, host: 7003
  config.vm.network "forwarded_port", guest: 7004, host: 7004

  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 2
  end
  # Configure the guest machine
  config.vm.provision "shell", inline: <<-SHELL
  echo "Configuring VM for LWOL Course...."
  echo "Setting SELinux to Permissive mode"
  sudo setenforce 0


  echo "Setting up required packages"
  sudo yum -y update
  sudo yum -y install git yum-utils device-mapper-persistent-data lvm2
  sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
  echo "Installing Docker"
  sudo yum makecache fast
  sudo yum install -y docker-ce
  sudo systemctl start docker
  sudo systemctl enable docker
  sudo usermod -a -G docker vagrant
  docker run hello-world
  mkdir -p /home/vagrant/oracle_docker
  sudo chown -R vagrant:vagrant /home/vagrant/oracle_docker
  SHELL

end
