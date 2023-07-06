# -*- mode: ruby -*-
# vi: set ft=ruby :

hosts = {
	"vm1" => "ip_addr1",
	"vm2" => "ip_addr2",
	"vm3" => "ip_addr3"
}

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.ssh.insert_key = false
  config.ssh.forward_agent = true
  config.ssh.username = "vagrant"
  config.ssh.password = "vagrant"
   

  hosts.each do |name, ip|
   config.vm.define name do |machine|
    machine.vm.network :private_network, ip: ip
    machine.vm.provider "virtualbox" do |vb|
     vb.name = name
     vb.gui = false
     vb.memory = "2048"
     vb.cpus = 1
    end
   end
  end

  config.vm.provision "shell", inline: <<-SHELL
    # python3 -c "import crypt;print(crypt.crypt('uservagrant'))" - for generate a hash for passwd
    useradd -m -s /bin/bash -p '$6$2tpC4O.ffP/TRB.s$ioTG28/GVXHNNgTpRsRLvNgPFl6.Sdh222ghT16jBgjYonGOfBpGMYslNMoEHH5xq.J2aVv5t.fjvo0xLmTEU1' user
    echo 'vagrant:newvagrant' | sudo chpasswd
  SHELL

end
