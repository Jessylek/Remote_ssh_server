# Remote_ssh_server

## Update system
sudo apt update  
sudo apt upgrade -y

## Install and enable OpenSSH
sudo apt install -y openssh-server
sudo systemctl enable --now ssh

## Allow SSH through Ubuntu firewall (UFW)
sudo ufw allow ssh
sudo ufw enable
sudo ufw status

## Create a dedicated SSH user
sudo adduser adminuser
sudo usermod -aG sudo adminuser

## Set up SSH key authentication
### On host machine
ssh-keygen -t ed25519
### Copy key to the VM 

type $env:USERPROFILE\.ssh\id_ed25519.pub | ssh jessyssh@192.168.150.129 "mkdir -p ~/.ssh && chmod 700 ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys"

### Test
ssh adminuser@SERVER_IP

