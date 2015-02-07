# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
 config.vm.box = "humaton/fedora-21-cloud"
 config.vm.host_name = "vagrant-presentation"
 config.vm.synced_folder ".", "/vagrant", type: :rsync
 
 
 config.vm.provision "shell", inline: "yum install fedora-release-server"
 config.vm.provision "shell", inline: "yum update -y"
 config.vm.provision "shell", inline: "yum install -y vagrant vagrant-libvirt vagrant-lxc --enablerepo=updates-testing"
 config.vm.provision "shell", inline: "yum install -y docker ruby-devel nodejs npm"
 
 config.vm.provision "shell", inline: "systemctl enable cockpit"
 config.vm.provision "shell", inline: "systemctl start cockpit"

 config.vm.provision "shell", inline: "systemctl enable docker"
 config.vm.provision "shell", inline: "systemctl start docker"
 
 
 #Presentation
 config.vm.provision "shell", inline: "yum install -y nginx"
 config.vm.provision "shell", inline: "cp /vagrant/nginx.conf /etc/nginx/"
 config.vm.provision "shell", inline: "nginx"

 config.vm.provision "shell", inline: "usr/bin/bash /vagrant/pull_docker_images.sh"
end
