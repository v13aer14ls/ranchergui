BOX_IMAGE = "ubuntu/xenial64"
NODE_COUNT = 2

Vagrant.configure("2") do |config|
  config.vm.define "master" do |subconfig|
    if Vagrant.has_plugin?("vagrant-vbguest") then
      config.vbguest.auto_update = false
end
    subconfig.vm.box = BOX_IMAGE
    subconfig.vm.hostname = "master"
    subconfig.vm.network :private_network, ip: "10.0.0.10"
    subconfig.vm.network "public_network", bridge: "wlp3s0", ip: "192.168.0.10"
    subconfig.vm.provider "virtualbox" do |vb|
      vb.memory = 8192 
      vb.cpus = 2
    end
  end
  
  (1..NODE_COUNT).each do |i|
    config.vm.define "node#{i}" do |subconfig|
    if Vagrant.has_plugin?("vagrant-vbguest") then
      config.vbguest.auto_update = false
end
      subconfig.vm.box = BOX_IMAGE
      subconfig.vm.hostname = "node#{i}"
      subconfig.vm.network :private_network, ip: "10.0.0.#{i + 10}"
      subconfig.vm.network "public_network", bridge: "wlp3s0", ip: "192.168.0.#{i +10}"
      subconfig.vm.provider "virtualbox" do |vb|
        vb.memory = 2048 
        vb.cpus = 2
      end
    end
  end
  config.vm.provision "shell", inline: <<-SHELL
  curl -fsSL https://get.docker.com | sh
  SHELL
end
