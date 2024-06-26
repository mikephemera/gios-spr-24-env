# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  # 16.04 - config.vm.box = "ubuntu/xenial64"
  # 18.04 - config.vm.box = "ubuntu/bionic64"
  config.vm.box = "bento/ubuntu-20.04"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = true

    # Customize the amount of memory on the VM:
    vb.memory = "1024"

    # Increase the # of CPUs for stressing MT if you'd like
    vb.cpus = "2"
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # For those trying to use Hyper-V, you may wish to uncomment the applicable
  # configuration lines below.
  #
  # Share folder between host and guest. Must explicily set these properites
  #config.vm.synced_folder ".", "/vagrant", type: "smb", create: true, mount_options: ["vers=3.0"]
  #
  # Hyper-V specific configurations
  # https://www.vagrantup.com/docs/hyperv/configuration.html
  config.vm.provider "hyperv" do |h|
    # this should enable sharing via SMB, but I haven't verified it works
    #h.synced_folder ".", "/vagrant", type: "smb", create: true, mount_options: ["vers=3.0"]
    h.enable_virtualization_extensions = true
    h.linked_clone = true
    h.vm_integration_services = {
      guest_service_interface: true
    }
  end


  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
config.vm.provision "shell", inline: <<-SHELL

    curl -s --compressed "https://gt-cs6200.github.io/ppa/KEY.gpg"|apt-key add -
    curl -s --compressed -o /etc/apt/sources.list.d/gt-cs6200.list "https://gt-cs6200.github.io/ppa/gt-cs6200.list"

    sudo apt-get -y update && \
    sudo DEBIAN_FRONTEND=noninteractive apt-get upgrade -y -o Dpkg::Options::="--force-confdef" -o Dpkg::Options::="--force-confold" && \
    sudo DEBIAN_FRONTEND=noninteractive apt-get -y install \
      git \
      python3 \
      python3-pip \
      python3-dev \
      libgmp-dev \
      gcc-multilib \
      valgrind \
      portmap \
      rpcbind \
      libcurl4-openssl-dev \
      bzip2 \
      libssl-dev \
      llvm \
      net-tools \
      libtool \
      pkg-config \
      zlib1g-dev \
      grpc-cs6200 \
      protobuf-cs6200

    sudo pip install --upgrade pip
    sudo pip install --upgrade requests future cryptography pyopenssl ndg-httpsclient pyasn1
  SHELL
end
