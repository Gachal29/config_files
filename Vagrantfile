# python3.9 develop machine

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"
  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "6144"
  end
  config.ssh.forward_agent = true
  # config.disksize.size = "40GB"
  # config.vm.synced_folder "#{Dir.home}/work", "/work"
  config.vm.provision :shell, inline:<<-EOS
    # Add deadsnakes repository
    add-apt-repository -y ppa:deadsnakes/ppa

    # Update package list
    export DEBIAN_FRONTEND=noninteractive
    apt-get update --allow-unauthenticated

    # Generic development
    apt-get install -y \
      tree \
      zip \
      unzip \
      build-essential \
      language-pack-ja-base \
      language-pack-ja
    
    # Japanese locale
    update-locale LANG=ja_JP.UTF-8

    # Set timezone
    timedatectl set-timezone Asia/Tokyo

    # Python development
    apt-get install -y \
      python3.9 \
      python3.9-dev \
      python3.9-venv
    
    # NodeJS development
    curl -fsSL https://deb.nodesource.com/setup_16.x | sudo -E bash -
    apt-get install -y nodejs

    # Requirements
    apt-get install -y \
      curl \
      git \
      libmysqlclient-dev \
      libsqlite3-dev \
      wget
    
    # MySQL development
    debconf-set-selections <<< 'mysql-server mysql-server/root_password password root'
    debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password root'
    apt-get install -y \
      mysql-server \
      mysql-client \
      libmysqlclient-dev
      
  EOS
end
