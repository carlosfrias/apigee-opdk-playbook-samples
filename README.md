Apigee OPDK Playbook Samples
============================

This project uses the Apigee OPDK roles written with Ansible to assemble sample playbooks that demonstrate how to 
install and configure Apigee. 

Requirements
============

* Apigee account for downloading binaries
* Apigee license file
* Vagrant and Virtualbox or an AWS account
* Ansible 2.1  
* Understanding of how to use Ansible

Introduction
============

Two folders are provided to help you setup your workspace.
 
* environments folder: Contains accelerator files for using either Vagrant or AWS. 
* installations folder: Contains configurations to support installing either a single node aio profile or a multi-node 
installation. 

Installing Ansible Roles
========================

It is necessary to install the Ansible roles on your control server. This can be accomplished with the provided 
install_roles.yml. Please use ansible-galaxy to download and install the role: 

    ansible-galaxy install -r install_roles.yml
    
Please note that you can obtain any updates by using -f (force): 
 
     ansible-galaxy install -fr install_roles.yml

Vagrant and Virtualbox
======================
 
A sample Vagrant file has been provided that will provision a VM on Virtualbox. The steps to complete include:

* Creating a settings file for your environment
* Provisioning the VM
* Invoking the installation.yml script with the settings for your environment. 

Provisioning the VM
===================

Regardless of your choice of VM the usage of Vagrant simplifies provisioning your environment. Please navigate to the 
folder of your choice and provision the VM with: 

    vagrant up

You can stop the VM with: 

     vagrant halt

You can dispose of the VM to recover disk space with:

    vagrant destroy -f
    
