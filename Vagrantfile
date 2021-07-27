BOX_IMAGE = "ubuntu/xenial64" # Aqui voce pode alterar a box utilizada para subir as maquinas.
NODE_COUNT = 2 #Aqui voce pode aumentar ou diminuir a quantidade de nodes.

# Aqui a maquina que vai ter o rancher instalado é provisionada
Vagrant.configure("2") do |config|
  config.vm.define "master" do |subconfig|
    if Vagrant.has_plugin?("vagrant-vbguest") then
      config.vbguest.auto_update = false
end
    subconfig.vm.box = BOX_IMAGE
    subconfig.vm.hostname = "master"
    subconfig.vm.network :private_network, ip: "10.0.0.10"
    subconfig.vm.network "public_network", bridge: "wlp3s0", ip: "192.168.0.10" # Alterar a interface de rede para a da sua maquina em caso de erro 'wlp3s0'
    subconfig.vm.provider "virtualbox" do |vb|
      vb.memory = 4096 #Voce pode aumentar ou dimunir os recursos disponibilizados aqui.
      vb.cpus = 2      # Aqui tambem 
    end
  end

  
  # Aqui sao configurados os  recursos dos nodes do rancher
  (1..NODE_COUNT).each do |i|
    config.vm.define "node#{i}" do |subconfig|
    if Vagrant.has_plugin?("vagrant-vbguest") then
      config.vbguest.auto_update = false
end
      subconfig.vm.box = BOX_IMAGE
      subconfig.vm.hostname = "node#{i}"
      subconfig.vm.network :private_network, ip: "10.0.0.#{i + 10}"
      subconfig.vm.network "public_network", bridge: "wlp3s0", ip: "192.168.0.#{i +10}" #Altere a interface de rede para a  correta em caso de erro.
      subconfig.vm.provider "virtualbox" do |vb|
        vb.memory = 2048 # Cuidado ao aumentar os recursos aqui uma vez que eles serao multiplicados pelo numero de nodes.
        vb.cpus = 1 # Aqui tambem
      end
    end
  end
  # a unica coisa que eu achei necessaria foi a instalacao do docker nas maquinas, mas voce pode criar um script de provisionamento e passar ele aqui. 
  config.vm.provision "shell", inline: <<-SHELL
  curl -fsSL https://get.docker.com | sh
  SHELL
end
