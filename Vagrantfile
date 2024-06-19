Vagrant.configure("2") do |config|
  (1..4).each do |i|
    config.vm.define "node#{i}" do |node|
      node.vm.box = "ubuntu/bionic64"
      node.vm.hostname = "node#{i}"
      node.vm.network "private_network", ip: "192.168.50.#{i+10}"
      node.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"
      end
      node.vm.provision "shell", inline: <<-SHELL
        # Instalação do Docker
        sudo apt-get update
        sudo apt-get install -y docker.io
        sudo systemctl start docker
        sudo systemctl enable docker
      SHELL
    end
  end
end
