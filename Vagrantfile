Vagrant.configure("2") do |config|

  config.vm.box = "generic/ubuntu2004"

  config.vm.provider "libvirt" do |libvirt|
    libvirt.memory = "2048"
    libvirt.cpus = 2
  end

  # Updating the Ubuntu kernel and packages
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get -y install python3-pip
  SHELL

  # Set the Ekaterinburg time to synchronize with the host system
  config.vm.provision "shell", inline: <<-SHELL
    sudo timedatectl set-timezone Asia/Yekaterinburg
  SHELL

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/playbook.yaml"
  end

  config.vm.network "forwarded_port", guest: 3000, host: 3000, protocol: "tcp"

end
