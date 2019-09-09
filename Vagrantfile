# -*- mode: ruby -*-
# vi: set ft=ruby :

# Every Vagrant development environment requires a box. You can search for
# boxes at https://atlas.hashicorp.com/search.
BOX_IMAGE = "bento/ubuntu-16.04"
COUNT = 2
HOSTNAME = "alexey"

Vagrant.configure("2") do |config|
    config.vm.box = BOX_IMAGE
    config.vm.hostname = HOSTNAME
    config.vm.network :private_network, ip: "10.0.0.10"
  
  (1..COUNT).each do |i|
    config.vm.define "#{HOSTNAME}#{i}" do |subconfig|
      subconfig.vm.box = BOX_IMAGE
      subconfig.vm.hostname = "ubuntu-#{i}-#{HOSTNAME}"
      subconfig.vm.network :private_network, ip: "10.0.0.#{i + 10}"
    end
  end

  # Install git and pull file
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y avahi-daemon libnss-mdns
    apt-get install -y git
    mkdir myrepo
    cd myrepo
    git init
    git remote add origin https://github.com/Bronetapochka/babah/
    git pull origin module-2
    cat module-2/module2.txt
  SHELL
end