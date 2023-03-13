## ref 
https://github.com/docker/awesome-compose/tree/master/plex

## wakatime swarm02
https://wakatime.com/@spcn12/projects/offfhsprcp



## Create VM template 
  * Os Ubuntu 22.04
  * Cpu 2 core
  * Memory 2024 MB
  * Storege 32 GB
#### After create VM 
 * Set timezone Bangkok Thailand
``` 
 timedatectl set-timezone Asia/Bangkok
``` 
 * Install docker engine for Ubuntu
 ``` 
 apt update ; apt upgrade -y
apt-get install \
    ca-certificates \
    curl wget \
    gnupg \
    lsb-release -y

mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" |  tee /etc/apt/sources.list.d/docker.list > /dev/null

apt-get update
apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
``` 
  * Update services after install Docker
``` 
apt update
apt upgrade -y
``` 
  * One time reboot node
``` 
reboot
``` 
### Run this code for set VM config to clone
```
cp /dev/null /etc/machine-id
rm /var/lib/dbus/machine-id
ln -s /etc/machine-id /var/lib/dbus/machine-id
init 0
```
### Run this code for docker authorited
```
sudo usermod -aG docker $USER
docker ps
```

## Prepare node Ubuntu 22.04 clon from template
  * Node1 manager node 
  * Node2 work1
  * Node3 work2
 
### After clone node
 * Use sudo mode for set time and hostname (all three node)
``` 
 sudo -i 
``` 
 * Set hostname for in each node
   * Node 1 set hostname to "manager"
   * Node 2 set hostname to "work1"
   * Node 3 set hostname to "work2"
``` 
 hostnamectl set-hostname “Change-me”
``` 
## In manager node
#### Can run this command to see node ip for remote ssh with VS code (manager node) and Vs code requires extension ssh remote
``` 
 ip a
```
#### After ss้h remote with vs code. Install this extensions
  * Docker
  * Git hub
  * Wakatime and enter api key
#### Run this command to gennarate token for run on work node
``` 
 docker swarm init
```
  * And copy token for run on work node
#### After enter token on work node can run this code for check member node
``` 
 docker node ls
```
#### Deploy portainer for swarm 
``` 
 curl -L https://downloads.portainer.io/ce2-17/portainer-agent-stack.yml -o portainer-agent-stack.yml
docker stack deploy -c portainer-agent-stack.yml portainer
```
  * go to this port https://localhost:9443
## In work node ( work1,work2 )
  * Can switch manager node to work node by this code ( on Vs code )
``` 
 ssh target_ip_local
```
  * Paste token on work node (all two node)

## Switch to manager mode agian 
  * Create file git config
``` 
 git config --global user.name "github_username"
 git config --global user.email "github_useremail"
```
  * Create folder swarm01 and swarm02
``` 
mrkdir swarm01
mrkdir swarm02
```
  * Git init in swarm01 and swarm02
``` 
Git init
```
  * Go to swarm01 for choose application potainer frome (https://github.com/docker/awesome-compose/tree/master/portainer)
  * Create README.md and compose.yaml file
  * Run this command to commit file
``` 
git commit -m "openProject"
```
  * Run this command for push to github
``` 
git push origin master
```

## ยังไม่สมบูรณ์นะครับบบ
