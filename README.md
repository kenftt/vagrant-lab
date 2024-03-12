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
