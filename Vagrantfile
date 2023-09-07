Vagrant.configure(2) do |config|
  config.vm.define "vm1" do |vm1|
    vm1.vm.box = "ubuntu/jammy64"
    vm1.vm.hostname = "vm1"
    vm1.vm.box_check_update = false
    vm1.vm.network "private_network", ip: "192.168.62.101"
    vm1.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
  end
  vm1.vm.provision "shell", inline: <<-SHELL
  export DEBIAN_FRONTEND=noninteractive

  rm /etc/resolv.conf
  echo "nameserver 8.8.8.8" > /etc/resolv.conf
  sudo apt-get update


  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

  sudo apt-key fingerprint 0EBFCD88

  sudo add-apt-repository \
     "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
     $(lsb_release -cs) \
     stable"

  sudo apt-get update

  SHELL
end
config.vm.define "vm2" do |vm2|
  vm2.vm.box = "ubuntu/jammy64" # Box name or URL
  vm2.vm.hostname = "vm2-V4" # Hostname for the second VM
  vm2.vm.box_check_update = false
  vm2.vm.network "private_network", ip: "192.168.62.100" # Private network IP address
  vm2.vm.provider "virtualbox" do |vb|
    vb.memory = "4096" # 4 GB RAM for the second VM
  end
  vm2.vm.provision "shell", inline: <<-SHELL
    export DEBIAN_FRONTEND=noninteractive

    rm /etc/resolv.conf
    echo "nameserver 8.8.8.8" > /etc/resolv.conf

    sudo apt-get update

    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

    sudo apt-key fingerprint 0EBFCD88

    sudo add-apt-repository \
       "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
       $(lsb_release -cs) \
       stable"

    sudo apt-get update

  SHELL
end
end
