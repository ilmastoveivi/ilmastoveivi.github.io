# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"
APP_BOXNAME = "ilmastoveivi"
APP_HOSTNAME = "ilmastoveivi.test"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "hashicorp/precise64"

  config.vm.define APP_BOXNAME
  config.vm.hostname = APP_HOSTNAME
  config.vm.network :private_network, ip: '192.168.42.42'
  config.vm.network "forwarded_port", guest: 80, host: 8080

  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true


  config.vm.provider 'virtualbox' do |vb|
    vb.customize ['modifyvm', :id, '--cableconnected1', 'on']

    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    vb.customize ["modifyvm", :id, "--natsettings1", "16000,64,64,1024,1024"]
    vb.customize ["modifyvm", :id, "--nictype1", "virtio"]
    vb.customize ["modifyvm", :id, "--nataliasmode1", "sameports"]
  end

  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "_ansible/provision.yml"
    ansible.install_mode = "pip"
  end

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
end