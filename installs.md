
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

###
sudo apt-get -y update
sudo apt-get -y install podman

###

##############
Install Ansible:

sudo apt update

sudo apt install software-properties-common

sudo apt-add-repository --yes --update ppa:ansible/ansible

sudo apt install ansible -y

################
#
#Clone Ansible-NAS:

git clone https://github.com/davestephens/ansible-nas.git && cd ansible-nas

#Create your own inventory and config files by copying inventories/sample to your own directory:

cp -rfp inventories/sample inventories/my-ansible-nas

#Review group_vars/all.yml. Change settings by overriding them in inventories/my-ansible-nas/group_vars/nas.yml.
sudo nano group_vars/all.yml
sudo nano inventories/my-ansible-nas/group_vars/nas.yml
#Update inventories/my-ansible-nas/inventory.
sudo nano inventories/my-ansible-nas/inventory
#Install the dependent roles: ansible-galaxy install -r requirements.yml (you might need sudo to install Ansible roles).
sudo ansible-galaxy install -r requirements.yml 
#Run the playbook - something like ansible-playbook -i inventories/my-ansible-nas/inventory nas.yml -b -K should do you nicely.

#
sudo apt install zfsutils -y
lsblk
ls /dev/disk/by-id/
#returns example
ata-QEMU_DVD-ROM_QM00001  virtio-ansiblenas1  virtio-ansiblenas2
#create pool example 
sudo zpool create -o ashift=12 ansiblepools1 mirror virtio-ansiblenas1 virtio-ansiblenas2
zpool status ansiblepools1
#use destroy to destroy
sudo zpool destroy ansiblepools1


sudo ansible-playbook -i inventories/my-ansible-nas/inventory nas.yml -b -K 

sudo apt install libnvpair1linux libuutil1linux libzfs2linux libzpool2linux zfs-zed zfsutils-linux nfs-kernel-server samba-common-bin zfs-initramfs | zfs-dracut zfsutils -y













