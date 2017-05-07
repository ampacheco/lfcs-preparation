# Defines our Vagrant environment
#
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # create master node
  config.vm.define :master do |master_config|
      master_config.vm.box = "centos/7"
      master_config.vm.hostname = "master"
      master_config.vm.network :private_network, ip: "10.0.13.10"
      master_config.vm.provider "virtualbox" do |vb|
        vb.memory = "256"
      end
      # Por Ahora no vamos a crear ningun bootstrap scritp.
      # master_config.vm.provision :shell, path: "bootstrap-mgmt.sh"
  end

  #
  # Hay dos alternativas, crear los dos nodos independientes o 
  # crear los dos nodos en un ciclo, que es la que vamos usar para probar esta tecnica
  # 

  # create some networks servers
  # https://docs.vagrantup.com/v2/vagrantfile/tips.html
  # Comentamos el port forwarding, porque no es necesario
  # mantenemos la sentencia porque eventualmente podria ser util esa configuracion
  
  (1..2).each do |i|
    config.vm.define "server#{i}" do |node|
        node.vm.box = "centos/7"
        node.vm.hostname = "server#{i}"
        node.vm.network :private_network, ip: "10.0.13.2#{i}"
        node.vm.network "forwarded_port", guest: 80, host: "808#{i}"
        node.vm.provider "virtualbox" do |vb|
          vb.memory = "256"
        end
    end
  end

end