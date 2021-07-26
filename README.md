swisscom-ansible Quickstart Guide
============================================================

This code will configure the Opensource Network Appliance VyOS (https://vyos.io) in
AWS environment and utilize it as a router to route traffic between two others sites
to demonstrate network, automation and cloud skills.

![Vyos topology](swisscom-vyos.png?raw=true "Vyos topology")

Pre-requisites
--------------

The following pre-requisites must be met prior to executing the lab:

  - The infrastructure must be created using the terraform repository. https://github.com/ramonlucas/swisscom-terraform
  - The ansible must be run from the bastion host.
  - You must have access to the Key Pair used in terraform.

Setup and Configuration
-----------------------

From you computer, transfer the Key Pair used in terraform to bastion-host using SCP command.

    chmod 600 key-pair.pem
    scp -i key-pair.pem key-pair.pem ec2-user@bastion-public-ip:~/.ssh/id_rsa

If you dont know the bastion host public IP, run "terraform output" from terraform repository.

Then, connect on ec2 bastion host instance:

    # ssh -i key-pair.pem ec2-user@bastion-public-ip

Download this repository

    [ec2-user@bastion-host]$ git clone https://github.com/ramonlucas/swisscom-ansible
    [ec2-user@bastion-host]$ cd swisscom-ansible

Ansible is already installed on bastion host. We can execute our playbook

    [ec2-user@bastion-host swisscom-ansible]$ ansible-playbook -i hosts main.yaml

After that, we can connect to our client machines to test connectivity

    [ec2-user@bastion-host]$ ssh 10.1.1.51
    [ec2-user@client-a1-1]$ ping 8.8.8.8

Check what is the nat public IP:

    [ec2-user@bastion-host]$ curl ip.ramonlucas.com

Note that IP is the same of router public ip