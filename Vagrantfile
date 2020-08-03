# -*- mode: ruby -*-
# vim: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define "bal" do |node|
    node.vm.box = "centos/7"
    node.vm.hostname = "bal"
    node.vm.network "private_network", ip: "192.168.70.11"
    node.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "256"]
      vb.customize ["modifyvm", :id, "--cpus", "1"]
    end
    node.vm.provision "shell", inline: <<-SHELL
      mkdir -p ~root/.ssh; cp ~vagrant/.ssh/auth* ~root/.ssh
      yum install -y epel-release
      yum install -y mc haproxy ntp
    SHELL
  end

  (1..2).each do |i|
    config.vm.define "web#{i}" do |web|
      web.vm.box = "centos/7"
      web.vm.hostname = "web#{i}"
      web.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "512"]
        vb.customize ["modifyvm", :id, "--cpus", "2"]
      end
      web.vm.network "private_network", ip: "192.168.70.2#{i}"
      web.vm.provision "shell", inline: <<-SHELL
        mkdir -p ~root/.ssh; cp ~vagrant/.ssh/auth* ~root/.ssh
        localectl set-locale ru_RU.UTF-8
        localectl set-x11-keymap us,ru grp:ctrl_shift_toggle
        localedef -i ru_RU -f UTF-8 ru_RU-UTF-8
        yum install -y epel-release
        yum install -y mc nginx wget unzip ntp
        yum install -y php php-gd php-mysqli php-imap php-mbstring php-intl php-json php-xml php-apcu php-opcache php-fpm
      SHELL
    end
  end

  (1..3).each do |i|
    config.vm.define "rc#{i}" do |node|
      node.vm.box = "centos/7"
      node.vm.hostname = "rc#{i}"
      node.vm.network "private_network", ip: "192.168.70.3#{i}"
      node.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "256"]
        vb.customize ["modifyvm", :id, "--cpus", "1"]
      end
      node.vm.provision "shell", inline: <<-SHELL
        mkdir -p ~root/.ssh; cp ~vagrant/.ssh/auth* ~root/.ssh
        yum install -y epel-release
        yum install -y mc ntp
      SHELL
    end
  end

  (1..3).each do |i|
    config.vm.define "pxc#{i}" do |node|
      node.vm.box = "centos/7"
      node.vm.hostname = "pxc#{i}"
      node.vm.network "private_network", ip: "192.168.70.4#{i}"
      node.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "512"]
        vb.customize ["modifyvm", :id, "--cpus", "2"]
      end
      node.vm.provision "shell", inline: <<-SHELL
        mkdir -p ~root/.ssh; cp ~vagrant/.ssh/auth* ~root/.ssh
        yum install -y epel-release
        yum install -y mc ntp
      SHELL
    end
  end

end
