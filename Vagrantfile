# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

    config.vm.define :nodo1 do |nodo1|
      nodo1.vm.box = "debian/bullseye64"
      nodo1.vm.hostname = "nodo1"
	config.vm.provider :libvirt do |libvirt|
	  libvirt.memory = 1024
	  libvirt.cpus = 2
	end
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
	config.vm.provider :libvirt do |libvirt|
	  libvirt.memory = 1024
	  libvirt.cpus = 2
	end
    end
    config.vm.define :nodo4 do |nodo4|
        nodo4.vm.box = "generic/rocky9"
        nodo4.vm.hostname = "nodo4"
	config.vm.provider :libvirt do |libvirt|
	  libvirt.memory = 1024
	  libvirt.cpus = 2
	end
    end
    config.vm.define :nodo5 do |nodo5|
        nodo5.vm.box = "generic/centos8"
        nodo5.vm.hostname = "nodo5"
	config.vm.provider :libvirt do |libvirt|
	  libvirt.memory = 1024
	  libvirt.cpus = 2
	end
    end
    config.vm.define :nodo6 do |nodo6|
        nodo6.vm.box = "centos/7"
        nodo6.vm.hostname = "nodo6"
	config.vm.provider :libvirt do |libvirt|
	  libvirt.memory = 1024
	  libvirt.cpus = 2
	end
    end


   config.vm.provision "shell", inline: <<-SHELL
     export "$(cat /etc/os-release  | grep -E '^ID_LIKE=')"
     dir=/home/vagrant
     aliasesfile=aliases
     packages="bat exa htop vim"
     if [ "$ID_LIKE" == "debian" ] ; then
        export DEBIAN_FRONTEND=noninteractive
        apt-get update
        apt-get install -y $packages
        aliasesfile=.bash_${aliasesfile}
      else
        yum check-update
        yum install -y $packages
        dir=${dir}/.bashrc.d
        mkdir -p $dir
      fi
      echo "alias ls='exa -l'" > ${dir}/${aliasesfile}
      echo "alias top='htop'" >> ${dir}/${aliasesfile}
      echo "alias vi=vim" >> ${dir}/${aliasesfile}
      [ "$ID_LIKE" == "debian" ] && bat=batcat || bat=bat
      echo "alias cat='${bat}'" >> ${dir}/${aliasesfile}
      chown -R vagrant:vagrant ${dir}
  SHELL

end
