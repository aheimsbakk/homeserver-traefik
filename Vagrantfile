# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  #config.vm.network "forwarded_port", guest: 3142, host: 3142, host_ip: "0.0.0.0"
  config.vm.network "private_network", ip: "10.0.0.10"

  config.vm.synced_folder ".", "/vagrant", disabled: false

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
    vb.cpus = 3
    #vb.linked_clone = true
    vb.default_nic_type = "virtio"
  end

  config.vm.provision "shell", inline: <<-SHELL
    export DEBIAN_FRONTEND=noninteractive
    apt-get update
    apt-get install -y docker.io docker-compose zram-config unattended-upgrades
  SHELL

  config.vm.provision "shell", "run": "always", inline: <<-SHELL
    mkdir -p /srv/traefik
    cd /vagrant
    cp tls.yml /srv/traefik/tls.yml
    docker-compose --env-file .env.template -f docker-compose.yml -f docker-compose.override.yml.template up -d
  SHELL
end

