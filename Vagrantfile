# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "debian/jessie64"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  # std: is not a tty
  config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"

  config.vm.provision "shell", inline: <<-SHELL
    progress() {
        echo "@@ $1"
    }
    
    clone() {
        progress "Cloning $2"
        if [[ -d "$1" ]]; then
            cd ${1}
            git pull
            cd ..
        else
            git clone --recursive "https://github.com/Fibbing/$1"
        fi
    }
    
    progress "Installing dependencies"
    sudo apt-get update
    sudo apt-get install -y git bridge-utils bird python bash \
                            python-dev python-pip gcc build-essential \
                            automake autoconf libtool gawk libreadline-dev \
                            texinfo console-data

    clone fibbingnode "the fibbing sources"
    clone labs "the fibbing labs"

    progress "Installing the fibbing controller"
    progress "... Adding quagga user/group"
    groupadd quagga
    useradd -g quagga quagga
    progress "... Executing the install script"
    cd fibbingnode
    sudo bash ./setup.sh
  SHELL
end
