# -*- mode: ruby -*-
# vi: set ft=ruby :
# Test line

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

    config.vm.define :bullseye64 do |bullseye64|
      bullseye64.vm.box = "debian/bullseye64"
      bullseye64.vm.hostname = "bullseye64"
    end
    config.vm.define :ubuntu2010 do |ubuntu2010|
      ubuntu2010.vm.box = "generic/ubuntu2010"
      ubuntu2010.vm.hostname = "ubuntu2010"
    end
    config.vm.define :ubuntu2204 do |ubuntu2204|
      ubuntu2204.vm.box = "generic/ubuntu2204"
      ubuntu2204.vm.hostname = "ubuntu2204"
    end
    config.vm.define :rocky9 do |rocky9|
      rocky9.vm.box = "generic/rocky9"
      rocky9.vm.hostname = "rocky9"
    end
    config.vm.define :centos8 do |centos8|
      centos8.vm.box = "generic/centos8"
      centos8.vm.hostname = "centos8"
    end
    config.vm.define :centos7 do |centos7|
      centos7.vm.box = "centos/7"
      centos7.vm.hostname = "centos7"
    end
    config.vm.define :ubuntu1604 do |ubuntu1604|
      ubuntu1604.vm.box = "generic/ubuntu1604"
      ubuntu1604.vm.hostname = "ubuntu1604"
    end
    config.vm.define :ubuntu2404 do |ubuntu2404|
      ubuntu2404.vm.box = "cloud-image/ubuntu-24.04"
      ubuntu2404.vm.hostname = "ubuntu2404"
    end
    config.vm.provision "shell", inline: <<-SHELL
      export "$(cat /etc/os-release  | grep -E '^ID_LIKE=' || echo ID_LIKE=debian)"
      dir=/home/vagrant
      aliasesfile=aliases
      packages="bat htop vim"
      create_aliases() {
         # echo "alias ls='exa -l'" > ${dir}/${aliasesfile}
         echo "alias top='htop'" >> ${dir}/${aliasesfile}
         echo "alias vi=vim" >> ${dir}/${aliasesfile}
         [ "$ID_LIKE" == "debian" ] && bat=batcat || bat=bat
         echo "alias cat='${bat}'" >> ${dir}/${aliasesfile}
      }
      if [ "$ID_LIKE" == "debian" ] ; then
        export DEBIAN_FRONTEND=noninteractive
        aliasesfile=.bash_${aliasesfile}
        apt-get update
        apt-get install -y $packages
      else
        if [ "$ID_LIKE" == '"rhel fedora"' ] ; then
          # detect if centos version is 7
          # this is needed to update repo url's
          export $(cat /etc/os-release  | grep -E '^VERSION_ID')
          if [ "${VERSION_ID}" == '"7"' ] ; then
             sed -i s/mirror.centos.org/vault.centos.org/g /etc/yum.repos.d/CentOS-*.repo
             sed -i s/^#.*baseurl=http/baseurl=http/g /etc/yum.repos.d/CentOS-*.repo
             sed -i s/^mirrorlist=http/#mirrorlist=http/g /etc/yum.repos.d/CentOS-*.repo
          fi
        fi
        yum check-update
        yum install -y $packages
        [ $? -eq 0 ] && { dir=${dir}/.bashrc.d; mkdir -p $dir; }
      fi
      [ $? -eq 0 ] && { create_aliases; chown -R vagrant:vagrant ${dir}; }
    SHELL
end
