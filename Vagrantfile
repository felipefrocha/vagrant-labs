# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  
  config.vm.box         = "hashicorp/bionic64"
  config.vm.hostname    = "shounen"
  config.vm.define "base"
  config.vm.network "public_network", use_dhcp_assigned_default_route: true
  config.vm.box_check_update = true

  config.vm.provider "virtualbox" do |vb|
      vb.name = "lab1"
      vb.memory = "2048"
  end
  
  config.vm.provision "shell", inline: <<-SHELL
     apt-get update && apt-get full-upgrade -y && apt-get install curl wget git python3 python3-pip jq
     curl -fsSL https://get.docker.com | bash
     usermod -aG docker vagrant
     echo "Installing docker compose"
	 wget $(curl -s https://api.github.com/repos/docker/compose/releases/latest | jq ".assets[].browser_download_url" -r | grep $(uname -s)-$(uname -m)| head -n 1)  -o /usr/local/bin/docker-compose && chmod +x /usr/local/bin/docker-compose && ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
   SHELL
end
