if Vagrant::VERSION < "2.0.0"
  $stderr.puts "Must redirect to new repository for old Vagrant versions"
  Vagrant::DEFAULT_SERVER_URL.replace('https://vagrantcloud.com')
end

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.box_check_update = true
  config.vm.synced_folder "shared/", "/home/vagrant/shared", create: true, type: 'virtualbox'

  config.vm.define "mongodb-m042" do |server|
    server.vm.provider "virtualbox" do |vb|
	     vb.customize ["modifyvm", :id, "--cpus", "2"]
       vb.name = "mongodb-m042"
       vb.memory = 2048
    end
    server.vm.hostname = "m042.university.mongodb"
    server.vm.network :private_network, ip: "192.168.42.100"
    server.vm.provision :shell, path: "provision_m042", args: ENV['ARGS']
  end
end
