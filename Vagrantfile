# Créditos: Supertutorial: https://www.supertutorial.com.br/usando-vagrant-configuracao-vagrantfile-ssh-multiplas-maquinas-id4953
BOX_IMAGE = "ubuntu/trusty64" # Ubuntu 14.04
#Qualquer VM em: https://app.vagrantup.com/boxes/search
NODE_COUNT = 3 # Quantidade de VM's 

Vagrant.configure("2") do |config|
  config.vm.define "master" do |subconfig|
  subconfig.vm.box = BOX_IMAGE
    subconfig.vm.hostname = "master"
    subconfig.vm.network "forwarded_port", guest: 80, host: 8081
    subconfig.vm.network :private_network, ip: "192.168.56.10"
    subconfig.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.cpus = 1
      end
  end

  (1..NODE_COUNT).each do |i|     config.vm.define "node#{i}" do |subconfig|
  subconfig.vm.box = BOX_IMAGE
      subconfig.vm.hostname = "node#{i}"
      subconfig.vm.network :private_network, ip: "192.168.56.#{i + 10}"
      subconfig.vm.provider "virtualbox" do |vb|
	vb.memory = "512"
	vb.cpus = 1
	end
    end
  end

 # Instalar o avahi-daemon em todas as vms - necessário para bom funcionando do cluster
config.vm.provision "shell", inline: <<-SHELL
    apt-get install -y avahi-daemon libnss-mdns
  SHELL
end
