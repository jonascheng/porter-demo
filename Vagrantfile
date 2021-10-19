$dockercompose = <<-SCRIPT
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
SCRIPT

$export_porter = <<-SCRIPT
echo 'export PATH=$PATH:~/.porter' >> /home/vagrant/.profile
echo 'export PORTER_ALLOW_DOCKER_HOST_ACCESS=true' >> /home/vagrant/.profile
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "boxomatic/ubuntu-18.04"
  config.vm.box_version = "20210723.0.1"
  config.vm.provision "docker"
  # config.vm.provision "shell", inline: $dockercompose
  config.vm.provision "shell", path: "install-porter.sh"
  config.vm.provision "shell", inline: $export_porter

  config.vm.define "web" do |node|
    node.vm.network "private_network", type: "dhcp"
  end
end
