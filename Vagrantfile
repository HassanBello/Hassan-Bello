
# v: set ft=ruby :

ENV['VAGRANT_DEFAULT_PROVIDER'] = 'libvirt'
Vagrant.configure(2) do |config|
config.vm.provider :libvirt do |libvirt|
libvirt.host = '192.168.122.1'
libvirt.username = "4kvm"
libvirt.connect_via_ssh = true
libvirt.driver = "kvm"
libvirt.storage_pool_name = "VMS"
libvirt.storage :file, :size => '40G', :type => 'raw'
end

config.vm.box = "https://s3.otlabs.fr/index.php/s/tPeoTjFJ7I870GQ/download"
config.vm.provision "shell",
 run: "always",
 inline: " echo nameserver 8.8.8.8 > /etc/resolv.conf"
	config.vm.define :hassan1 do |hassan1|
	  hassan1.vm.hostname = "hassan1"
	  hassan1.vm.network :public_network, ip: '192.168.7.106', netmask: "22", :dev => "enp4s0", :mode => 'bridge'
	  hassan1.vm.network :public_network, ip: '10.10.12.1', netmask: "22", :dev => "enp7s0.4", :mode => 'bridge'
	  hassan1.vm.synced_folder "./script", "/vagrant", disabled: false
	  hassan1.vm.provision "shell" , path: "script/update.sh"
	  hassan1.vm.provision "shell" , path: "script/provision-hdd.sh"
	  hassan1.vm.provision "shell" , path: "script/install-docker.sh"
	  hassan1.vm.provision "shell" , path: "script/deploy-gluster.sh"
	  hassan1.vm.provision "shell" , path: "script/deploy-gogs.sh"
	  hassan1.vm.provision "shell" , path: "script/install-config-zabbixagent.sh"
	  hassan1.vm.provider :libvirt do |domain|
		domain.storage :file, :size => '40G'
	    domain.memory = 1024
	    domain.cpus = 1
	  end
	end
	 config.vm.define :hassan2 do |hassan2| 
          hassan2.vm.hostname = "hassan2"
		  hassan2.vm.network :public_network, ip: '192.168.7.105', netmask: "22", :dev => "enp4s0", :mode => 'bridge'
		  hassan2.vm.network :public_network, ip: '192.168.2.171', netmask: "22", :dev => "enp7s0.4", :mode => 'bridge'
	      hassan2.vm.network :public_network, ip: '10.10.12.2', netmask: "22", :dev => "enp7s0.4", :mode => 'bridge'
          hassan2.vm.synced_folder "./script", "/vagrant", disabled: false
          hassan2.vm.provision "shell" , inline: "/vagrant/provision-hdd.sh"
          hassan2.vm.provision "shell" , inline: "/vagrant/install-docker.sh"
	      hassan2.vm.provision "shell" , inline: "/vagrant/deploy-gluster.sh"
          hassan2.vm.provision "shell" , inline: "/vagrant/deploy-gogs.sh"
          hassan2.vm.provision "shell" , inline: "/vagrant/install-config-zabbixagent.sh"
          hassan2.vm.provider :libvirt do |domain|
			domain.storage :file, :size => '40G'
            domain.memory = 1024
            domain.cpus = 1
          end
        end
         config.vm.define :hassan3 do |hassan3|
          hassan3.vm.hostname = "hassan3"
		  hassan3.vm.network :public_network, ip: '192.168.7.109', netmask: "22", :dev => "enp4s0", :mode => 'bridge'
	  hassan3.vm.network :public_network, ip: '192.168.2.210', netmask: "22", :dev => "enp7s0.4", :mode => 'bridge'
	  hassan3.vm.network :public_network, ip: '10.10.12.3', netmask: "22", :dev => "enp7s0.4", :mode => 'bridge'
           hassan3.vm.synced_folder "./script", "/vagrant", disabled: false
           hassan3.vm.provision "shell" , inline: "/vagrant/update.sh"
           hassan3.vm.provision "shell" , inline: "/vagrant/provision-hdd.sh"
           hassan3.vm.provision "shell" , inline: "/vagrant/install-docker.sh"
		   hassan3.vm.provision "shell" , inline: "/vagrant/deploy-gluster.sh"
          hassan3.vm.provision "shell" , inline: "/vagrant/install-config-zabbixagent.sh"
          hassan3.vm.provider :libvirt do |domain|
			domain.storage :file, :size => '40G'
            domain.memory = 1024
            domain.cpus = 1
          end
        end
end
