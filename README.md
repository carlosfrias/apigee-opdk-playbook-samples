Apigee OPDK Playbook Samples
============================

This project uses the Apigee OPDK roles written with Ansible to assemble sample playbooks that demonstrate how to 
install and configure Apigee. 

Usage Instructions
==================

* Configure Ansible to install Apigee OPDK as indicated in the 
[Apigee Setup Ansible](https://github.com/carlosfrias/apigee-opdk-playbook-setup-ansible) project for details. 
* Install Apigee OPDK ansible roles.
* Update ~/.apigee/credentials.yml.
* Update your inventory file [Updating your Inventory File](https://github.com/carlosfrias/apigee-opdk-playbook-setup-ansible/blob/master/inventory.md).
* Update your ansible configuration file with your inventory file or folder name, the remote-user and ssh private_key_file.

Functionality Available
=======================

The Apigee OPDK Roles enable you to manage the installation and configuration the OPDK. The following is a list of 
functionality provided by these roles:

 * Installation of an arbitrarily sized data center
 * Selective rollback of an installed component to assist in troubleshooting
 * Silent installation file is dynamically generated to the defined planet and data center.
 * Roles install Apigee Edge OPDK 4.16.01, 4.16.05 and 4.16.09 by simply specifying the desired version
 * Integrated with AWS is available to manage the lifecycle of AMI instances 
 * Roles adjust to account for either CentOS 6 or greater; Oracle Linux 6 or greater and RHEL 6 or greater. 
 * Roles adjust to also account for whether they are executed in within the virtualized environments provisioned by AWS 
  and Vagrant or a non-virtualized server.  
 * Check that ports are accessible and available prior to installing any component.
 * Check that all expected ports are in use post-installation.

Requirements
============

* Apigee account for downloading binaries
* Apigee license file
* Ansible 2.1 or greater  
* Internet accessible machine either for full installation or to create an Apigee mirror.

Folder Structure
================

Two folders are provided to help you setup your workspace. The folders are named environments and installations.
 
## environments folder

Contains accelerator files for using Vagrant. 

## installations folder 

Contains configurations to support installing a single node aio profile.

Installing Ansible Roles
========================

It is necessary to install the Ansible roles on your control server. This can be accomplished with the provided 
requirements.yml. Please use ansible-galaxy to download and install the roles: 

    ansible-galaxy install -r requirements.yml
    
Please note that you can obtain any updates by using -f (force): 
 
     ansible-galaxy install -f -r requirements.yml


Vagrant and Virtualbox
======================
 
A sample Vagrant file has been provided that will provision a VM on Virtualbox. The steps to complete include:

* Creating a settings file for your environment
* Provisioning the VM
* Update your inventory file.
* Invoking the installation.yml script with the settings for your environment. 
    
Creating a settings file for your environment
=============================================

Please review the README of the [opdk-setup-default-settings](https://github.com/carlosfrias/apigee-opdk-setup-default-settings) role for details regarding the settings file. This project 
also contains a starter file you can use in the defaults folder.

Provisioning the VM
===================

Regardless of your choice of VM the usage of Vagrant simplifies provisioning your environment. Please navigate to the 
folder of your choice and provision the VM with: 

    vagrant up

You can stop the VM with: 

     vagrant halt

You can dispose of the VM to recover disk space with:

    vagrant destroy -f
 