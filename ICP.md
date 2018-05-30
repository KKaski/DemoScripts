#IBM Private Cloud (ICP)

## Installation
As a prereq have linux image with wget and docker installed

1. Make static IP so that the IP does not change on boot. Copy this to /etc/sysconfig/network-scripts/ifcfg-eth1 and modify to match on you need

``` 
DEVICE=eth1
IPADDR=192.168.27.100
NETMASK=255.255.255.0
NETWORK=192.168.27.0
BROADCAST=192.168.27.255
ONBOOT=yes
``` 
2. Instal prereqs and get ICP installation container
```
sudo sysctl -w vm.max_map_count=262144
sudo yum instal -y wget yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo install docker
sudo systemctl start docker
sudo systemctl enable docker
sudo docker pull ibmcom/icp-inception:2.1.0.3
mkdir /opt/ibm-cloud-private-ce-2.1.0.3
cd /opt/ibm-cloud-private-ce-2.1.0.3
sudo docker run -e LICENSE=accept -v "$(pwd)":/data ibmcom/icp-inception:2.1.0.3 cp -r cluster /data

sudo ssh-keygen -b 4096 -f ~/.ssh/id_rsa -N ""
sudo cat ~/.ssh/id_rsa.pub | sudo tee -a ~/.ssh/authorized_keys
sudo systemctl restart sshd
sudo cp ~/.ssh/id_rsa ./cluster/ssh_key
ssh-copy-id -i ~/.ssh/id_rsa root@192.168.27.100
```

Prepare your hostname
```
hostnamectl set-hostname icp

vi /etc/hosts
127.0.0.1       localhost
192.168.27.100  icp
```

3. Configuration and installation
Add your host ip to ICP hosts file
```
cd /opt/ibm-cloud-private-ce-2.1.0.3/cluster
vi hosts
```

Set the firewall mode enable
```
vi config.yml
firewall_enabled: true
```
4. Install ICP
```
sudo docker run -e LICENSE=accept --net=host -t -v "$(pwd)":/installer/cluster ibmcom/icp-inception:2.1.0.3 install
```

## Demo Application Creation

## Demo Application Deployment

