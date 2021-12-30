# set up the default terminal
ENV["TERM"]="linux"

Vagrant.configure("2") do |config|

  # set the image for the vagrant box
  config.vm.box = "opensuse/Leap-15.3.x86_64"

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  config.vm.network "forwarded_port",  guest: 6443, host: 6443 # API Access

  # st the static IP for the vagrant box
  config.vm.network "private_network", ip: "192.168.50.4"

  # consifure the parameters for VirtualBox provider
  config.vm.provider "virtualbox" do |vb|
    vb.name="node1"
    vb.memory = "4096"
    vb.cpus = 4
    vb.customize ["modifyvm", :id, "--ioapic", "on"]
  end
  config.vm.provision "shell", inline: <<-SHELL
    # install a k3s cluster
    curl -sfL https://get.k3s.io | INSTALL_K3S_VERSION=v1.19.3+k3s1 K3S_KUBECONFIG_MODE="644" sh -
    # install iptables
    sudo zypper --non-interactive install iptables
    # install Helm
    curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
  SHELL
end
