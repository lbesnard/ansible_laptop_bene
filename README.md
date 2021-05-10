# Ansible - provision laptop :computer:

This repo aims at provisionning my personal laptop (debian base) 

It will install:
  * anaconda3 python environment 
  * git repositories
  * conda environment for data-services
  * NetCDF libraries

# Installation
## 1.1 install private key
install key (usually ```id_rsa```)to $HOME/.ssh (600)
```bash
chmod 600 ~/.ssh/config
chmod 644 ~/.ssh/id_rsa.pub
chmod 600 ~/.ssh/id_rsa
```
## 2. provision localhost debian based machine with Ansible
### 2.1 with sudo privileges

Run the following command in bash. (will install git, ansible; good for a new OS)
```bash
curl -L https://raw.githubusercontent.com/lbesnard/ansible_laptop_bene/master/install.sh | bash
```

OR if ansible is already installed on the machine
```
/usr/bin/ansible-pull -U https://github.com/lbesnard/ansible_laptop_bene.git -K -i hosts
```

### 2.2 Without sudo (and if ansible priorly installed via linuxbrew)
```bash
ansible-pull -U https://github.com/lbesnard/ansible_laptop_bene.git remote.yml -i hosts
```

### 2.3 Install specific tag with no sudo privileges
```bash

ansible-pull -i hosts -U https://github.com/lbesnard/ansible_laptop_bene.git -t conda
```

### 2.4 Run locally (examples)
```bash
git clone https://github.com/lbesnard/ansible_laptop_bene.git
cd ansible_laptop_bene

# run as root
/usr/bin/ansible-playbook -i hosts local.yml -K

# run as non sudo user
ansible-playbook -i hosts remote.yml --skip-tags apt

# run as non sudo user with a specific tag
ansible-playbook -i hosts remote.yml -t conda
```
## 3 Post Installation
install manuall vbox ext pack because of manual licencing
```sudo apt-get install virtualbox-ext-pack```
