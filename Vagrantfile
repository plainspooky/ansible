# -*- mode: ruby -*-
# vim: set ft=ruby expandtab tabstop=4 shiftwidth=4 softtabstop=4:

Vagrant.configure("2") do |config|
    config.vm.define :ubuntu do |ubuntu|
        ubuntu.vm.box = "ubuntu/xenial64"
        ubuntu.vm.network :private_network, ip: "172.20.20.10"
        ubuntu.vm.network "forwarded_port", guest: 80, host: 8000
        ubuntu.vm.provision :shell, path: "scripts/software_update_debian"
        ubuntu.vm.provision "shell", path:"./scripts/virtualenv_install_debian"
        ubuntu.vm.provision "shell", path:"./scripts/ansible_setup", privileged:false
        ubuntu.vm.provision "shell", path:"./scripts/ansible_install", privileged:false
        ubuntu.vm.provision "shell", path:"./scripts/genereate_ssh_key", privileged:false
        ubuntu.vm.provision "shell", path:"./scripts/import_ssh_key", privileged:false
        ubuntu.vm.provider "virtualbox" do |vb|
            vb.customize ["modifyvm", :id, "--memory", "512"]
            vb.customize ["modifyvm", :id, "--cpus", "1"]
        end
    end

    config.vm.define :centos do |centos|
        centos.vm.box = "centos/7"
        centos.vm.network :private_network, ip: "172.20.20.11"
        centos.vm.network "forwarded_port", guest: 80, host: 8001
        centos.vm.provision :shell, path: "scripts/software_update_centos"
        centos.vm.provision "shell", path:"./scripts/import_ssh_key", privileged:false
        centos.vm.provider "virtualbox" do |vb|
            vb.customize ["modifyvm", :id, "--memory", "512"]
            vb.customize ["modifyvm", :id, "--cpus", "1"] 
        end
    end
end
