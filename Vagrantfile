# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define "gitlab" do |subconfig|
    subconfig.vm.box = "debian/jessie64"
    subconfig.vm.hostname = "gitlab"
    subconfig.vm.provider "virtualbox" do |vb|
      vb.memory = "4096"
    end
    subconfig.vm.network "forwarded_port", guest: 80, host: 8080
    subconfig.vm.network "forwarded_port", guest: 80, host: 443
    subconfig.vm.network :private_network, ip: "10.0.0.10"

    subconfig.vm.provision "shell", inline: <<-SHELL
       sed -i '$ a 10.0.0.11 gitlab-runner' /etc/hosts           
    SHELL
  end
  config.vm.define "gitlab-runner" do |subconfig|
    subconfig.vm.box = "debian/jessie64"
    subconfig.vm.hostname = "gitlab-runner"
    subconfig.vm.network :private_network, ip: "10.0.0.11"

    subconfig.vm.provision "shell", inline: <<-SHELL
       sed -i '$ a 10.0.0.10 gitlab' /etc/hosts           
    SHELL
  end

  # ["gitlab-server", "gitlab-runner"].each_with_index do |name, index|
  #   config.vm.define "#{name}" do |subconfig|
  #     subconfig.vm.box = "debian/jessie64"
  #     subconfig.vm.hostname = "#{name}"
  #     # subconfig.vm.network :private_network, ip: "10.0.0.#{index + 10}"
  #     subconfig.vm.memory = 4096 if name == "gitlab-server"
  #     subconfig.vm.network "forwarded_port", guest: 80, host: 8080 if name == "gitlab-server"
  #   end
  # end

  # Install avahi on all machines  
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get install -y avahi-daemon libnss-mdns
  # SHELL

  # config.vm.provision "ansible" do |ansible|
  #   ansible.playbook = "ansible/00_playbook.yaml"
  #   ansible.become = true
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
