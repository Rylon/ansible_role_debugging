# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.define "ubuntu_trusty" do |ubuntu_trusty|
    ubuntu_trusty.vm.box = "ubuntu/trusty64"
    ubuntu_trusty.vm.hostname = "vagrant-ubuntu"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = 'dummy.yml'
    ansible.verbose  = true
  end

end
