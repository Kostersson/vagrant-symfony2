Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu1204"

  # Use https://github.com/covex-nn/packer-templates to create "ubuntu1204" base box
  #
  # config.vm.box_url = "http://vagrantstore.apnet.ru/ubuntu1204.box"

  config.vm.provider :virtualbox do |v|
    v.customize ["modifyvm", :id, "--nictype1", "virtio"]
    v.customize ["modifyvm", :id, "--nictype2", "virtio"]
    v.customize ["modifyvm", :id, "--nictype3", "virtio"]
    v.customize ["modifyvm", :id, "--memory", 2048]
  end

  config.vm.network :private_network, ip: "127.0.0.2"
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.hostname = "www.local"

  # /srv/config/
  #
  # If a server-conf directory exists in the same directory as your Vagrantfile,
  # a mapped directory inside the VM will be created that contains these files.
  # This directory is currently used to maintain various config files for php and
  # nginx as well as any pre-existing database files.
  #
  config.vm.synced_folder "vagrant/config/", "/srv/config"

  # Provisioning
  #
  config.vm.provision "shell", path: "vagrant/provision/provision.sh"
end
