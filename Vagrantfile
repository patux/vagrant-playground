# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

    config.vm.define :nodo1 do |nodo1|
      nodo1.vm.box = "debian/bullseye64"
      nodo1.vm.hostname = "nodo1"
    end
    config.vm.define :nodo2 do |nodo2|
      nodo2.vm.box = "generic/ubuntu2010"
      nodo2.vm.hostname = "nodo2"
	config.vm.provider :libvirt do |libvirt|
	  libvirt.memory = 1024
	  libvirt.cpus = 2
	end
    end
    config.vm.define :nodo3 do |nodo3|
        nodo3.vm.box = "generic/ubuntu2204"
        nodo3.vm.hostname = "nodo3"
    end
   config.vm.provision "shell", inline: <<-SHELL
     apt-get update
     apt-get install -y bat exa htop
     echo "alias ls='exa -l'" > /home/vagrant/.bash_aliases
     echo "alias top='htop'" >> /home/vagrant/.bash_aliases
     echo "alias cat='batcat'" >> /home/vagrant/.bash_aliases
   SHELL

end
