# Remote_ssh_server
**Project URL:** https://roadmap.sh/projects/ssh-remote-server-setup <br>

These are the key steps to setup an ssh remote connection <br>

Prerequisites
- Ubuntu server 24.04LTS as the remote server
- Windows 11 as the host machine
## Update system
> sudo apt update  
> sudo apt upgrade -y

## Install and enable OpenSSH
>```sudo apt install -y openssh-server```
> sudo systemctl enable --now ssh

## Allow SSH through Ubuntu firewall (UFW)
> sudo ufw allow ssh
> sudo ufw enable
> sudo ufw status

## Create a dedicated SSH user
> sudo adduser adminuser
> sudo usermod -aG sudo adminuser

## Set up SSH key authentication
**On host machine**
> ssh-keygen -t ed25519
**Copy key to the VM**
> type $env:USERPROFILE\.ssh\id_ed25519.pub | adminuser@SERVER_IP "mkdir -p ~/.ssh && chmod 700 ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys" which is the equivalent of *ssh-copy-id adminuser@SERVER_IP* if you are working on a linux host
**Test**
> ssh adminuser@SERVER_IP
> You are going to be asked for a password on the first connection but no password will be expected for future connections.

## Secure SSH configuration
**Edit config**
> sudo vim /etc/ssh/sshd_config
**Set**
> PermitRootLogin no
> PasswordAuthentication no
> PubkeyAuthentication yes
**Reload SSH**
> sudo systemctl reload ssh

## Install Fail2ban
This is done to add extra security to our ssh server by blockin brute force attacks for instance 
> sudo apt install -y fail2ban
> sudo systemctl enable --now fail2ban













