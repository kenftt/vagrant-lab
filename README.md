# Vagrant Lab Environment

This repository contains a basic Vagrant lab setup designed for creating a multi-machine environment. It includes several Ubuntu Focal Fossa (Ubuntu 20.04) virtual machines configured to work together for development and testing purposes. The setup consists of one master server, three web servers, one database server, and one load balancer.

## Prerequisites

Before you begin, ensure you have the following software installed on your system:

- [Vagrant](https://www.vagrantup.com/downloads.html)
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

These tools are necessary to create and manage the virtual machines defined in the `Vagrantfile`.

## Getting Started

To use this Vagrant lab, follow these steps:

1. **Clone the repository**

   Clone this repository to your local machine using the following command:

   ```bash
   git clone https://github.com/kenftt/vagrant-lab
   ```

2. **Navigate to the repository directory**

   Change into the repository directory:

   ```bash
   cd vagrant-lab
   ```

3. **Start the virtual machines**

   Execute the following command to start and provision all the virtual machines defined in the Vagrantfile:

   ```bash
   vagrant up
   ```

   This command reads the Vagrantfile, creates the virtual machines, and configures them according to the specifications provided.

3. **Accessing the virtual machines** (2 methods)

    a. ***Vagrant ssh***
   
      You can SSH into any of the virtual machines using Vagrant's ssh command:
  
      ```bash
      vagrant ssh <hostname>
      ```
      
    b. ***SSH directly from your terminal***

   Or you can SSH into any of the virtual machines using ssh command into your terminal:

      ```bash
      # save the config to a file
      vagrant ssh-config > vagrant-ssh

      # run ssh with the file.
      ssh -F vagrant-ssh <hostname>
      ```
   Replace <hostname> with the name of the virtual machine you wish to access, such as master, web01, web02, web03, db, or LoadBalancer.

# How to install Ansible on hosts

To manage the virtual machines with Ansible, follow these steps to install and configure Ansible on the host machine:

1. **Update and upgrade the system and install Python, Pip and Ansible**

   ```bash
   sudo apt-get update && sudo apt-get upgrade -y
   sudo apt install python3-pip -y
   pip install ansible
   ```

2. **Add Ansible to PATH**

   ```bash
   echo 'export PATH=$PATH:~/.local/bin' >> ~/.bashrc
   source ~/.bashrc
   ```

3. **Copy SSH Keys**

   Create a directory to store SSH keys and copy them from Vagrant:

   ```bash
   mkdir -p ~/ansible_keys
   for machine in /vagrant/.vagrant/machines/*; do
     cp "$machine/virtualbox/private_key" ~/ansible_keys/$(basename $machine)_private_key
   done
   ```

4. **Set correct permissions for Keys**
   ```
   chmod 600 ~/ansible_keys/*
   ```

5. **Update Ansible inventory file**
6. 
   Add the following to your inventory.ini file to define your hosts and their respective SSH settings:
   
   ```ini
   [myhosts]
   web01 ansible_host=192.168.56.101 ansible_user=vagrant ansible_ssh_private_key_file=~/ansible_keys/web01_private_key
   web02 ansible_host=192.168.56.102 ansible_user=vagrant ansible_ssh_private_key_file=~/ansible_keys/web02_private_key
   web03 ansible_host=192.168.56.103 ansible_user=vagrant ansible_ssh_private_key_file=~/ansible_keys/web03_private_key
   db ansible_host=192.168.56.104 ansible_user=vagrant ansible_ssh_private_key_file=~/ansible_keys/db_private_key
   LoadBalancer ansible_host=192.168.56.105 ansible_user=vagrant ansible_ssh_private_key_file=~/ansible_keys/LoadBalancer_private_key
   ```

7. **Test Ansible connectivity**
8. 
   Once Ansible is installed and configured, you can test connectivity to your hosts:
   
   ```bash
   ansible myhosts -m ping -i inventory.ini
   ```



