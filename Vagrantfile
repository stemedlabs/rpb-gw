# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "trusty64"

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "512"]
  end

  config.vm.define :gw do |gw|
    gw.vm.hostname = "neutrino-gw"
    gw.vm.network "public_network", ip: "192.168.123.10"

    # Provisioning steps
    gw.vm.provision "shell", inline: "sudo aptitude -y install dnsmasq"
    gw.vm.provision "file", source: "files/dnsmasq.conf", destination:
                    "/tmp/dnsmasq.conf"
    gw.vm.provision "shell", inline: "sudo mv /tmp/dnsmasq.conf /etc/dnsmasq.conf"
    gw.vm.provision "shell", inline: "sudo service dnsmasq restart"
    gw.vm.provision "shell", inline: "sudo sysctl -w net.ipv4.ip_forward=1"
    gw.vm.provision "shell", inline: "sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE"
  end

end
