## Summary

This is a simple VM that acts as a DHCP server and gateway for a RBP device
that is directly plugged to the bridged network device. The intended use
case is for lab environments where students/teachers need the ability to easily
access their RBP over the network while still providing it Internet access.

## Requirements

You need to have the following installed on your system:

* Virtualbox (https://www.virtualbox.org)
* Vagrant (http://www.vagrantup.com)

For host routing to work properly, you'll need to set a static IP on the
bridged ethernet interface on the 192.168.123.0/24 subnet through your OS.
A good address to use would be 192.168.123.20.

## Usage

To launch the gateway after installing dependencies you can run:

* vagrant up

Upon launch you will be prompted for the network device to bridge to. Select
the ethernet device on your system where you will connect your RBP device.

You can destroy the VM using:

* vagrant destroy

Once the VM is booted, you can turn on your RBP and connect. It will DHCP and 
use the VM as its network gateway. If the laptop has external connectivity (via
wireless) the RBP will be NAT'd through the VM to the Internet via the VM's
eth0 device. You can connect to the RBP using the address assigned from dnsmasq
on 192.168.123.0/24.

Note, once booted if you reboot your VM you will need to reprovision as some
settings are not persisted. That can be done by simply running:

* vagrant provision
