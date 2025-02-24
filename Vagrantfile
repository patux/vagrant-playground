# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.vm.provider "virtualbox"
    config.vm.provider "libvirt"

    config.vm.provider :virtualbox do |virtualbox|
      virtualbox.memory = 1024
      virtualbox.cpus = 2
    end

    config.vm.provider :libvirt do |libvirt|
      libvirt.memory = 1024
      libvirt.cpus = 2
    end if Vagrant.has_plugin?('vagrant-libvirt')

    config.vm.define :node1 do |node1|
      node1.vm.box = "debian/bullseye64"
      node1.vm.hostname = "node1"
    end
    config.vm.define :node2 do |node2|
      node2.vm.box = "generic/ubuntu2010"
      node2.vm.hostname = "node2"
    end
    config.vm.define :node3 do |node3|
      node3.vm.box = "generic/ubuntu2204"
      node3.vm.hostname = "node3"
    end
    config.vm.define :node4 do |node4|
      node4.vm.box = "generic/rocky9"
      node4.vm.hostname = "node4"
    end
    config.vm.define :node5 do |node5|
      node5.vm.box = "generic/centos8"
      node5.vm.hostname = "node5"
    end
    config.vm.define :node6 do |node6|
      node6.vm.box = "centos/7"
      node6.vm.hostname = "node6"
    end
    config.vm.provision "shell", inline: <<-SHELL
      export "$(cat /etc/os-release  | grep -E '^ID_LIKE=' || echo ID_LIKE=debian)"
      dir=/home/vagrant
      aliasesfile=aliases
      packages="bat htop vim"
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
      # echo "alias ls='exa -l'" > ${dir}/${aliasesfile}
      echo "alias top='htop'" >> ${dir}/${aliasesfile}
      echo "alias vi=vim" >> ${dir}/${aliasesfile}
      [ "$ID_LIKE" == "debian" ] && bat=batcat || bat=bat
       echo "alias cat='${bat}'" >> ${dir}/${aliasesfile}
       chown -R vagrant:vagrant ${dir}
    SHELL
end
