# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  #config.vm.box = "centos65-openstack-deploy-node"
  #config.vm.box_url = "http://www.lyricalsoftware.com/downloads/centos65.box"
  #config.vm.box = "ubuntu1404-openstack-deploy-node"
  #config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"
  config.vm.box = "ubuntu1404i386-openstack-deploy-node"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-i386-vagrant-disk1.box"
  config.vm.provider :virtualbox do |vb|
    vb.gui = false
  end
  #config.vm.provision :shell, :inline => "sudo yum install -y python-dev python-pip"
  #config.vm.provision :shell, :inline => "sudo pip install --upgrade pip"
  #config.vm.provision :shell, :inline => "sudo yum install -y python-devel python-pip"
  #config.vm.provision :shell, :inline => "sudo pip install python-openstackclient"
  
  config.vm.provision :shell, :inline => "apt-get update"
  config.vm.provision :shell, :inline => "apt-get install -y python-dev python-pip"
  config.vm.provision :shell, :inline => "aptitude install -y python-pip"
  config.vm.provision :shell, :inline => "sudo pip install python-novaclient"
  
  
  #config.vm.provision :shell, :inline => "sudo pip install python-quantumclient"
  #config.vm.provision :shell, :inline => "sudo pip install python-keystoneclient"
  #config.vm.provision :shell, :inline => "sudo pip install python-glanceclient"
  #config.vm.provision :shell, :inline => "sudo pip install python-swiftclient"
  #config.vm.provision :shell, :inline => "sudo pip install python-cinderclient"
  #config.vm.provision :shell, :inline => "export JAVA_HOME=/usr/bin"

end
