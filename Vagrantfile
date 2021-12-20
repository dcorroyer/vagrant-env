# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.box = "generic/debian9"
  config.vm.define "vagrant"
  config.vm.hostname = "vagrant"
  config.vm.network "private_network", ip: "192.168.33.12"
  config.vagrant.plugins = ["vagrant-scp", "vagrant-disksize", "vagrant-reload"]

  config.vm.synced_folder "./projects/", "/home/vagrant/projects/", owner: "vagrant", group: "vagrant"
  config.vm.synced_folder "./prerequisites/", "/home/vagrant/prerequisites/", owner: "vagrant", group: "vagrant"

  config.vm.provision "shell", inline: "chmod +x /home/vagrant/prerequisites/install-prerequisites", run: "once"
  config.vm.provision "shell", inline: "/home/vagrant/prerequisites/install-prerequisites", run: "once"
  config.vm.provision "shell", inline: "source ~/.bashrc", run: "once" , privileged: false
  config.vm.provision "shell", inline: "sudo usermod -aG docker vagrant", run: "once"
  config.vm.provision :reload, run: "once"

  config.ssh.forward_agent = true
  config.vm.provision "file", source: "~/.ssh/id_rsa", destination: "~/.ssh/id_rsa"
  config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/id_rsa.pub"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "3072"
  end
  config.disksize.size = '40GB'
end
