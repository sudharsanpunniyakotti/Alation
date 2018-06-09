
# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
   config.vm.box = "centos/7"
  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", 256]
  end

  config.vm.define :haproxy, primary: true do |haproxy_config|

    haproxy_config.vm.hostname = 'haproxy'
    haproxy_config.vm.network :private_network, ip: "192.168.33.40"
	haproxy_config.vm.provision :shell, inline: <<-SHELL
	  yum install ansible git -y
  ansible-pull -i inventory -U https://github.com/sudharsanpunniyakotti/Alation  playbook.yml -e 'host_name=localhost, playbooks=haproxy'
  SHELL
  end
  
  config.vm.define :web1 do |web1_config|

    web1_config.vm.hostname = 'web1'
    web1_config.vm.network :private_network, ip: "192.168.33.50"
	web1_config.vm.provision :shell, inline: <<-SHELL
	yum install ansible git -y
  ansible-pull -i inventory -U https://github.com/sudharsanpunniyakotti/Alation  playbook.yml -e 'host_name=localhost , playbooks=apache'
    
    SHELL

  end
  config.vm.define :web2 do |web2_config|

    web2_config.vm.hostname = 'web2'
    web2_config.vm.network :private_network, ip: "192.168.33.60"
	web2_config.vm.provision :shell, inline: <<-SHELL
	yum install ansible git -y
  ansible-pull -i inventory -U https://github.com/sudharsanpunniyakotti/Alation  playbook.yml  -e 'host_name=localhost , playbooks=apache'
  SHELL

  end
end

