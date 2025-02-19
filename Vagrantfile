# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

# The most common configuration options are documented and commented below.
# For a complete reference, please see the online documentation at
# https://docs.vagrantup.com.
   
# Every Vagrant development environment requires a box. You can search for
# boxes at https://vagrantcloud.com/search.
    
Vagrant.configure("2") do |config|

  #======================================================================================#
  # Guest: Force a specific version for VirtualBox Guest Additions
  #--------------------------------------------------------------------------------------#
  # A version mismatch bug may occur with the Guest Additions (after multiple reinstalls)
  # Even the Vagrant-vbguest plugin may fail to fix it. Best to override the .iso image.
  #--------------------------------------------------------------------------------------#
  # config.vbguest.iso_path = "https://download.virtualbox.org/virtualbox/%{version}/VBoxGuestAdditions_%{version}.iso"
  #======================================================================================#
  config.vbguest.iso_path = "https://download.virtualbox.org/virtualbox/%{version}/VBoxGuestAdditions_%{version}.iso"



  #======================================================================================#
  # Image: select virtual machine image (may be architecture specific)
  #--------------------------------------------------------------------------------------#
  # Mac OSX (Intel):
  # config.vm.box = "ubuntu/jammy64"
  # 
  # Intel x86-64:
  # config.vm.box = "ubuntu/jammy64"
  #======================================================================================#
  config.vm.box = "ubuntu/jammy64"


  #======================================================================================#
  # Timeout: time to initialize machine (in secs, default = 300 = 5 mins)
  #--------------------------------------------------------------------------------------#
  # config.vm.boot_timeout = 300
  #======================================================================================#
  config.vm.boot_timeout = 600
  

  #======================================================================================#
  # Machine: Customizations for machine (memory, etc)
  #--------------------------------------------------------------------------------------#
  # vb.memory = "4096"
  #======================================================================================#
  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  #
  # View the documentation for the provider you are using for more
  # information on available options.
  #
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "2048"
  # end
  #

  config.vm.provider "virtualbox" do |vb|
     
     # Custom VM name "vbox-ubuntu-faktory"
     vb.name = "vbox-ubuntu-faktory"
     
     # Display the VirtualBox GUI when booting the machine
     vb.gui = true
  
     # Customize the amount of memory on the VM:
     vb.memory = "4096" 
  end

  

  #======================================================================================#
  # Sharing: vb guest additions are needed for shared folders (synched folders)
  #--------------------------------------------------------------------------------------#
  # config.vbguest.auto_update = true
  #======================================================================================#
  config.vbguest.auto_update = true
  
    
  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false



  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  #======================================================================================#
  # NAT forward port mappings 
  #--------------------------------------------------------------------------------------#
  # config.vm.network "forwarded_port", guest: 22, host: 2222
  #======================================================================================#
  #config.vm.network "forwarded_port", guest: 3000, host: 3333


  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"


  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  
  
  

  #======================================================================================#
  # DiskSize: root filesystem disk size (requires vagrant-disksize plugin)
  #--------------------------------------------------------------------------------------#
  # config.disksize.size = "20GB"
  #======================================================================================#
  config.disksize.size = "20GB"


  
  #======================================================================================#
  # Boostrap: configure disks, mountpoints
  #--------------------------------------------------------------------------------------#
  # ResizeFS: resize root filesystem partition
  #--------------------------------------------------------------------------------------#
  # resize2fs /dev/sda1
  #--------------------------------------------------------------------------------------#
  #  
  #--------------------------------------------------------------------------------------#
  # Directories: configure directories for mounting shared folders 
  #--------------------------------------------------------------------------------------#
  # config.vm.provision "shell", "mkdir -p /work/faktory"
  #======================================================================================#
  config.vm.provision "shell", inline: <<-SHELL

    echo ""  
    echo "resizing root filesystem"
    resize2fs /dev/sda1


    echo ""  
    echo "creating shared folders"
    mkdir -p /vagrant
    mkdir -p /mnt/work
    
    
    echo ""  
    echo "registering package repositories"
    echo "deb http://uk.archive.ubuntu.com/ubuntu/ jammy main restricted universe multiverse"               > /etc/apt/sources.list
    echo "deb-src http://uk.archive.ubuntu.com/ubuntu/ jammy main restricted universe multiverse"           >> /etc/apt/sources.list
    echo "deb http://uk.archive.ubuntu.com/ubuntu/ jammy-security main restricted universe multiverse"      >> /etc/apt/sources.list
    echo "deb-src http://uk.archive.ubuntu.com/ubuntu/ jammy-security main restricted universe multiverse"  >> /etc/apt/sources.list
    echo "deb http://uk.archive.ubuntu.com/ubuntu/ jammy-updates main restricted universe multiverse"       >> /etc/apt/sources.list
    echo "deb-src http://uk.archive.ubuntu.com/ubuntu/ jammy-updates main restricted universe multiverse"   >> /etc/apt/sources.list
    apt-get update


    echo ""  
    echo "adding apt repository tools"
    apt-get -y install apt-transport-https ca-certificates
    apt-get -y install curl gnupg
    apt-get -y install software-properties-common python-software-properties
    #apt-get -y upgrade
    apt-get update


    echo ""
    echo "installing virtualbox extensions"
    sudo apt -y install build-essential dkms linux-headers-$(uname -r)
    apt-get update


    # ?
    # Check This - not sure it's required since we're forcing the version
    # ?

    apt-get -y install dkms
    #apt-get -y install virtualbox-guest
    apt-get -y install virtualbox-guest-dkms
    apt-get -y install virtualbox-guest-utils    
    apt-get -y install virtualbox-guest-additions-iso
       
  SHELL
 
 
 
  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder ".", "/mnt/vagrant"

    
  #======================================================================================#
  # Folders: configure mountpoints for synched folders 
  #--------------------------------------------------------------------------------------#
  # config.vm.synced_folder ".", "/mnt/vagrant"
  #======================================================================================#
  #config.vm.synced_folder ".", "/vagrant"
  config.vm.synced_folder "../../", "/mnt/work"


  
  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.  
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y nginx
  # SHELL

  #
  # @see https://help.ubuntu.com/community/VirtualBox
  # @see https://askubuntu.com/questions/142549/how-to-install-ubuntu-on-virtualbox
  #
  # @see https://wiki.ubuntulinux.org/wiki/Docker

  config.vm.provision "shell", inline: <<-SHELL
  
    echo ""
    echo "configuring basic system"
    cp /vagrant/motd                /etc
    # todo certificates and credentials
    # warning: do not overwrite the vagrant credentials (~/.ssh/authorized_keys)
    # if using an ssh-agent, ssh-keys should already be preloaded (ssh-add -L) 
            

    # ?
    # Check this - this was to copy stuff from the host into the box
    # ?

    echo ""  
    echo "creating source directories"
    mkdir -p /mnt/work/faktory  
        

    #========================================================================#
    # System
    #========================================================================#

    #apt-get update

    echo ""
    echo "updating core linux utils"
    apt-get -y install syslinux
    apt-get -y install coreutils
    apt-get -y install util-linux
    #apt-get -y install procps
    #apt-get -y install iotop
        
    echo ""
    echo "updating ubuntu linux utils"
    apt-get -y install systemd.d
    #apt-get -y install init.d
    apt-get -y install rc

    
    #------------------------------------------------------------------------#
    # Archive
    #------------------------------------------------------------------------#

    echo ""
    echo "installing file archive utils"
    #apt-get -y install tar
    apt-get -y install zip
    apt-get -y install unzip
    #apt-get -y install gzip
    #apt-get -y install bzip2
    apt-get -y install sharutils


    #------------------------------------------------------------------------#
    # Network
    #------------------------------------------------------------------------#

    echo ""
    echo "installing basic network utils"
    #apt-get -y install ifupdown
    apt-get -y install net-tools
    apt-get -y install dnsutils    
    apt-get -y install wget
    #apt-get -y install curl


    
    #------------------------------------------------------------------------#
    # Security
    #------------------------------------------------------------------------#

    echo ""
    echo "installing secure network utils"
    apt-get -y install gnutls
    apt-get -y install openssh
    apt-get -y install openssl
    apt-get -y install openssl-dev
    apt-get -y install stunnel

    # gpg is v1. gnupg is v2
    #apt-get -y install gpg
    #apt-get -y install gnupg    

    # ?
    # Check this - common libraries for FIPS security compliance
    # ?

    echo ""
    echo "installing common compression libraries"
    #apt-get -y install zlib zlib-dev
    #apt-get -y install zlib1g zlib1g-dev


    echo ""
    echo "installing common crypto libraries"
    apt-get -y install libgcrypt20-dev

     
    #------------------------------------------------------------------------#
    # Utilities
    #------------------------------------------------------------------------#

    echo ""
    echo "installing console tools"
    apt-get -y install ncurses
    apt-get -y install vim
    #apt-get -y install nano




    #========================================================================#
    # Development
    #========================================================================#

    
    echo ""
    echo "installing common dev utils"
    apt-get -y install bc
    apt-get -y install dos2unix

    echo ""
    echo "installing source control tools"
    apt-get -y install diffutils
    apt-get -y install patchutils
    apt-get -y install git

    
    # ?
    # Check this
    # We definitely want GNU POSIX, glibc, java, scala, and R
    # We will most certainly need crypto, perl, python, ruby.
    # Do we need go, rust, cargo, possibly erlang or haskell ?
    # ?


    #------------------------------------------------------------------------#
    # Glibc C / C++
    #------------------------------------------------------------------------#

    echo ""
    echo "installing GNU libc"
    apt-get -y install libc-bin
    apt-get -y install libc6
    apt-get -y install libc6-dev
    
    echo ""
    echo "installing basic C and C++ compiler"
    apt-get -y install gcc
    apt-get -y install g++
    apt-get -y install gdb    
    
    echo ""
    echo "installing basic compiler tools"
    apt-get -y install libtool
    apt-get -y install binutils
    apt-get -y install make
    apt-get -y install automake
    apt-get -y install autoconf
   

    #------------------------------------------------------------------------#
    # Misc libs, EBNF grammar tools, processors
    #------------------------------------------------------------------------#

    echo ""
    echo "installing grammar parser tools"
    apt-get -y install guile
    apt-get -y install bison
    apt-get -y install flex
    apt-get -y install swig
    apt-get -y install ctags


    echo ""
    echo "installing common io protocols"
    apt-get -y installd cpio
    apt-get -y install protobuf-compiler

    
    echo ""
    echo "installing dependency libs"
    #apt-get -y install libreadline-dev
    

    #------------------------------------------------------------------------#
    # .NET
    #------------------------------------------------------------------------#
    # see: https://learn.microsoft.com/en-us/dotnet/core/install/linux-ubuntu-install?tabs=dotnet8&pivots=os-linux-ubuntu-2204

    # .NET runtime: pick either .NET or ASP.NET
    #echo ""
    #echo "installing .NET runtime"
    #echo ""
    #apt-get install -y dotnet-runtime-8.0
    #apt-get install -y aspnetcore-runtime-8.0

    # .NET SDK comes wit the full runtime
    echo ""
    echo "installing .NET SDK and runtime"
    echo ""
    apt-get install -y dotnet-host
    apt-get install -y dotnet-sdk-8.0

    #echo ""
    #echo "installing .NET msbuild tools"
    #echo ""
    #apt-get update

    # Mono
    echo ""
    echo "installing .NET Mono cross-platform development"
    echo ""
    gpg --homedir /tmp --no-default-keyring --keyring /usr/share/keyrings/mono-official-archive-keyring.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
    echo "deb [signed-by=/usr/share/keyrings/mono-official-archive-keyring.gpg] https://download.mono-project.com/repo/ubuntu stable-focal main" | sudo tee /etc/apt/sources.list.d/mono-official-stable.list
    apt update

    apt-get -y install mono-develop


    #------------------------------------------------------------------------#
    # Java
    #------------------------------------------------------------------------#

    echo ""
    echo "installing Java compilation tools"
    echo ""
    apt-get -y install openjdk-21-jdk-headless
    apt-get -y install maven
   

    #------------------------------------------------------------------------#
    # Scala
    #------------------------------------------------------------------------#

    echo ""
    echo "installing Scala functional language tools"
     apt-get -y install scala
    
    
    #------------------------------------------------------------------------#
    # R-lang 
    #------------------------------------------------------------------------#

    echo ""
    echo "installing R functional language tools"
    apt-get install -y r-base
   

    #------------------------------------------------------------------------#
    # Perl (for apache, misc, cloud ops, dev-ops)
    #------------------------------------------------------------------------#

    echo ""
    echo "installing perl development tools"
    apt-get -y install perl
    apt-get -y install cpanminus


    #------------------------------------------------------------------------#
    # PHP (for apache, composer, cloud ops, dev-ops)
    #------------------------------------------------------------------------#

    echo ""
    echo "installing PHP development tools"
    apt-get -y install php



    #------------------------------------------------------------------------#
    # Python (for aws-cli, cloud ops, dev-ops)
    #------------------------------------------------------------------------#

    # python required for many tools, including aws-cli

    echo ""
    echo "installing python development tools"
    apt-get -y install python
    apt-get -y install python-dev
    apt-get -y install python-pip
    # patch broken pip by using easy_install
    easy_install pip
    cp /usr/local/bin/pip /usr/bin
    pip install --upgrade pip
    

    
    #------------------------------------------------------------------------#
    # Ruby (for vagrant, puppet, cloud ops, dev-ops)
    #------------------------------------------------------------------------#
        
    # ruby,gems, rails required for vagrant, puppet

    echo ""
    echo "installing ruby development tools"
    apt-add-repository ppa:brightbox/ruby-ng
    apt-get update
    
    apt-get -y install ruby ruby-dev
    apt-get -y install gems rubygems-integration
    apt-get -y install ruby-rails ruby-railties
    apt-get -y install ruby-builder ruby-bundler

    
    #------------------------------------------------------------------------#
    # Go-Lang (for docker, cloud-ops, dev-ops)
    #------------------------------------------------------------------------#

    
    echo ""
    echo "installing Go development tools"
    apt-get update
    apt-get -y install golang-go
    


    #========================================================================#
    # Services, Servers, Runtimes
    #========================================================================#


    #------------------------------------------------------------------------#
    # Databases
    #------------------------------------------------------------------------#
    
#    echo ""
#    echo "installing mysql and postgresql clients"
#    apt-get -y install myresql-client postgresql-client


    # ?
    # Check this: mssql-cli may require a specific python version!
    #
    # see: https://pypi.org/project/mssql-cli/
    # see: https://dbafromthecold.com/2022/05/13/install-mssql-cli-on-ubuntu-22-04/
    # see: https://github.com/dbcli/mssql-cli/issues/531
    # ?

    echo ""
    echo "installing msqsql client"
    pip install --upgrade --force cli_helpers
    pip install --upgrade --force tabulate
    pip install mssql-cli
    # apt-get -y install msqql-cli



    #------------------------------------------------------------------------#
    # Node.js
    #------------------------------------------------------------------------#

#     echo ""
#     echo "installing nodejs engine"
#     apt-get -y install nodejs
#     apt-get -y install npm
#     cd; touch install_nvm.sh; chmod a+x install_nvm.sh
#     curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh > install_nvm.sh
#     ./install+nvm.sh
#     source ~/.profile




    #========================================================================#
    # Cloud Ops, Cluster Ops, Dev Ops
    #========================================================================#



    #------------------------------------------------------------------------#
    # jquery, onigura (for aws-cli, cloud-ops, dev-ops)
    #------------------------------------------------------------------------#

    echo ""
    echo "installing oniguruma regexp lib"
    apt-get -y install libonig
    apt-get -y install libonig-dev    
    
    
    echo ""
    echo "installing jq/yq json/yaml processors"
    # jq json processor
    apt-get -y install jq
    # yq yaml processor (wrapper for jq)
    pip install 'yq < 2.0.0'
    

  
    #------------------------------------------------------------------------#
    # Docker
    #------------------------------------------------------------------------#

    # Docker written in go
       
    # ?
    # Check this
    # If this is for a generic Jenkins faktory VM on kube,
    # We may need an exotic docker-wihin-docker VM setup.
    # At minimum we need a local docker engine + client.
    # Do we also need kube-cli, AWS-cli, etc?
    # ?
 
    echo ""
    echo "configuring docker repostories"
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    apt-get update
    echo ""
    echo "installing docker engine"
    apt-get -y install docker.io


    # Composer wriiten in php

    apt-get -y install composer
    

    # Packer ?

    #------------------------------------------------------------------------#
    # Kubernetes
    #------------------------------------------------------------------------#

    # seems to install from ubuntu-20-xenial instead of ubuntu-22-jammy

    curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add
    apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
    apt-get update

    #apt-get install -y containerd
    #apt-get install -y kubeadm kubelet 

    apt-get install -y kubectl


    # Terraform ?


    # KOps ?


    # Helm ?



    #------------------------------------------------------------------------#
    # Amazon AWS
    #------------------------------------------------------------------------#

    echo ""
    echo "installing AWS=client"
    apt-get -y install awscli    
        
        


    echo ""
    echo "Done."
    #reboot

  SHELL


end
