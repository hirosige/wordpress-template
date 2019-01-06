# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/centos-7.3"
  # config.vm.network "public_network"
  config.vm.network "private_network", ip: "192.168.33.33"

  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/site.yml"
  end

  if Vagrant.has_plugin?("vagrant-vbguest")
    dev.vbguest.auto_update = false
  end

  config.vm.provider "virtualbox" do |vm|
    vm.customize ["modifyvm", :id, "--memory", "1024"]
    vm.customize ["modifyvm", :id, "--cpuexecutioncap", "65"]
  end

  config.vm.synced_folder ".",
    "/var/www/html",
    :mount_options => ["dmode=775", "fmode=775"]

  config.vm.synced_folder ".",
    "/vagrant",
    :mount_options => ["dmode=775", "fmode=775"]
end
