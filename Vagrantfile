Vagrant.configure(2) do |config|
config.vm.define "sumanvm" do |sumanvm|
  sumanvm.vm.box = "ubuntu/jammy64" # Box name or URL
  sumanvm.vm.hostname = "sumanvm-V4" # Hostname for the second VM
  sumanvm.vm.box_check_update = false
  sumanvm.vm.network "private_network", ip: "192.168.62.101" # Private network IP address
  sumanvm.vm.provider "virtualbox" do |vb|
    vb.memory = "4096" # 4 GB RAM for the second VM
  end
  sumanvm.vm.provision "shell", inline: <<-SHELL
    export DEBIAN_FRONTEND=noninteractive
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

    sudo apt-key fingerprint 0EBFCD88

    sudo add-apt-repository \
       "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
       $(lsb_release -cs) \
       stable"

    sudo apt-get update
    rm /etc/resolv.conf
    echo "nameserver 8.8.8.8" > /etc/resolv.conf

    sudo apt-get update

  SHELL
end
end
