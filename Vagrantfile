# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "debian/buster64"

  #config.vm.network "forwarded_port", guest: 3142, host: 3142, host_ip: "0.0.0.0"
  config.vm.network :private_network, ip: "10.0.0.10"
  config.vm.synced_folder ".", "/vagrant", type: "nfs", nfs_version: 3

  config.vm.provider :libvirt do |l|
    l.memory = "4096"
    l.cpus = 2
    l.qemu_use_session = false
  end

  config.vm.provision "shell", inline: <<-SHELL
    export DEBIAN_FRONTEND=noninteractive
    apt-get update
    apt-get install -y docker.io python3-pip zram-tools unattended-upgrades
    pip3 install docker-compose
  SHELL

  config.vm.provision "shell", "run": "always", inline: <<-SHELL
    mkdir -p /srv/traefik
    cd /vagrant
    cp tls.yml /srv/traefik/tls.yml
    docker-compose --env-file .env.template -f docker-compose.yml -f docker-compose.override.yml.template up -d
  SHELL
end

