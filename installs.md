
sudo apt-get update
sudo apt-get upgrade

#net-tools, the collection of base networking utilities for Linux.
sudo apt install net-tools

#set static ip example
sudo nano /etc/network/interfaces
#example static ip for eth0
iface eth0 inet static    
    address 192.168.1.100
    network 192.168.1.0
    netmask 255.255.255.0
    broadcast 192.168.1.255
    gateway 192.168.1.1
    dns-nameservers 8.8.8.8 8.8.4.4


#use cockpit (preferred usecase) https://cockpit-project.org/running.html
. /etc/os-release
sudo apt install -t ${VERSION_CODENAME}-backports cockpit


Cockpit on your server, point your web browser to: https://ip-address-of-machine:9090



##############
Install Ansible:

sudo apt update

sudo apt install software-properties-common

sudo apt-add-repository --yes --update ppa:ansible/ansible

sudo apt install ansible -y

################
