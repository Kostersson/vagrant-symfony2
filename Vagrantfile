is_windows = (RbConfig::CONFIG['host_os'] =~ /mswin|mingw|cygwin/)

Vagrant.configure("2") do |config|
  config.vm.box = "covex/ubuntu1204-x64"

  config.vm.provider :virtualbox do |v|
    v.customize ["modifyvm", :id, "--nictype1", "virtio"]
    v.customize ["modifyvm", :id, "--nictype2", "virtio"]
    v.customize ["modifyvm", :id, "--nictype3", "virtio"]
    v.customize ["modifyvm", :id, "--memory", 2048]
    v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end

  config.vm.network :private_network, ip: "192.168.80.80"
  config.vm.hostname = "miehisto.local"

  if not is_windows
    config.vm.synced_folder ".", "/vagrant", nfs: true
  end

  config.vm.synced_folder "vagrant/config/", "/srv/config"

  config.vm.provision "shell", path: "vagrant/provision/apt-get.sh"
  config.vm.provision "shell", path: "vagrant/provision/mysql.sh"
  config.vm.provision "shell", path: "vagrant/provision/apache.sh"
  config.vm.provision "shell", path: "vagrant/provision/compass.sh"
  config.vm.provision "shell", path: "vagrant/provision/samba.sh"
  config.vm.provision "shell", path: "vagrant/provision/composer.sh"
  
  config.vm.synced_folder "../slps-messi-legacy/", "/var/www/miehisto"
  config.vm.synced_folder "../smps-messi-legacy/", "/var/www/messi"
  config.vm.synced_folder "../tf2/", "/var/www/tf2"
  config.vm.synced_folder "../svn/statusboard", "/var/www/statusboard"
  
  config.vm.network "forwarded_port", guest: 80, host: 80, host_ip: "127.0.0.1", host_protocol: 'tcp'
  config.vm.network "forwarded_port", guest: 3306, host: 3306, host_ip: "127.0.0.1", host_protocol: 'tcp'
end
