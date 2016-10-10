Apigee OPDK Playbook Samples
============================

This project uses the Apigee OPDK roles written with Ansible to assemble sample playbooks that demonstrate how to 
install and configure Apigee. 

Usage Instructions
==================

* Configure Ansible to install Apigee OPDK as indicated in the 
[Apigee Setup Ansible](https://github.com/carlosfrias/apigee-setup-ansible) project for details. 
* Install Apigee OPDK ansible roles.
* Update ~/.apigee/credentials.yml.
* Update your inventory file.
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

Ansible Roles
=============

The following ansible roles will be installed with the requirements.yml file:

* [opdk-setup-apigee-user](https://github.com/carlosfrias/apigee-opdk-setup-apigee-user)
* [opdk-setup-os-common](https://github.com/carlosfrias/apigee-opdk-setup-os-common)
* [opdk-setup-os-ds](https://github.com/carlosfrias/apigee-opdk-setup-os-ds)
* [opdk-setup-os-minimum](https://github.com/carlosfrias/apigee-opdk-setup-os-minimum)
* [opdk-setup-default-settings](https://github.com/carlosfrias/apigee-opdk-setup-default-settings)
* [opdk-time-sync](https://github.com/carlosfrias/apigee-opdk-time-sync)
* [opdk-setup-openjdk](https://github.com/carlosfrias/apigee-opdk-setup-openjdk)
* [opdk-setup-bootstrap](https://github.com/carlosfrias/apigee-opdk-setup-bootstrap)
* [opdk-setup-silent-installation-config](https://github.com/carlosfrias/apigee-opdk-setup-silent-installation-config)
* [opdk-setup-component](https://github.com/carlosfrias/apigee-opdk-setup-component)
* [opdk-setup-component-installer](https://github.com/carlosfrias/apigee-opdk-setup-component-installer)
* [opdk-setup-selinux-disable](https://github.com/carlosfrias/apigee-opdk-setup-selinux-disable)
* [opdk-shutdown-iptables](https://github.com/carlosfrias/apigee-opdk-shutdown-iptables)
* [opdk-setup-org-config](https://github.com/carlosfrias/apigee-opdk-setup-org-config)
* [opdk-setup-org](https://github.com/carlosfrias/apigee-opdk-setup-org)
* [opdk-setup-validate](https://github.com/carlosfrias/apigee-opdk-setup-validate)
* [opdk-setup-validate-cleanup](https://github.com/carlosfrias/apigee-opdk-setup-validate-cleanup)
* [opdk-setup-apigee-log-files](https://github.com/carlosfrias/apigee-opdk-setup-apigee-log-files)
* [fetch-files](https://github.com/carlosfrias/apigee-fetch-files)

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
 
Updating your inventory file
============================

We use a standard Ansible inventory file with some semantic conventions applied to it. The semantic model applied to the 
Ansible inventory file is described in the following sections.
 
## Ansible Inventory Files
Ansible provides rich semantics for inventory files. We leverage the ansible model by applying a semantic convention 
that is based on the Apigee Private Cloud domain model for referencing server nodes as collections of planets and 
regions. This means that the normal Ansible inventory files are used as is with the exception of the semantic conventions
for inventory group names. 

## Inventory File Conventions
These roles depend on use of conventions in the inventory file. Specifically inventory file conventions are ansible 
groups names that are defined around Apigee semantics. These ansible groups are semantically linked to the documentation. 
The ansible groups used as conventions correspond to the installation roles and server categorizations called out in 
the Apigee Private Cloud Installation and Configuration Guide. It has been useful to use planet and region designations 
combined with the documented installation role names to create categorization semantics that should be fairly intuitive 
once you read the Apigee Private Cloud Installation and Configuration Guide. 
   
## Inventory Planet, Region and Installation Role Conventions
A planet refers to all server nodes across all data centers. These semantics are held via the use of group names for  
all nodes that fulfill a specific purpose. The installation roles provide the semantic model we followed. The inventory 
file group names for planet level semantics are listed in the template inventory file below. 

A region represents subset of a planet. The semantics used for installation roles are congruent with a region. Region 
have been referenced as data centers. The internal configurations of OPDK and BaaS support many regions as dc-1, dc-2 
and so forth. Following this historical precedent we also define the regions with their corresponding installation role
to provide a semantic model as follows:
 
    # Listing that references all data centers that compose a planet. 
    [planet]
    dc-1

    [dc-1]
    # Listing of all nodes in data center 1 (dc-1)
    
    [ds:children]
    # Listing of all the Cassandra and Zookeeper nodes across the planet
    dc-1-ds
    
    [dc-1-ds]
    # Listing of all the Cassandra and Zookeeper nodes in dc-1
    
    [dc-1-ms]
    # Listing of all the Management Server nodes in dc-1
     
    [dc-1-ldap]
    # Listing of all OpenLDAP nodes in dc-1
    
    [dc-1-rmp]
    # Listing of all Router and Message Processor nodes in dc-1
    
    [dc-1-qpid]
    # Listing of all Qpid nodes in dc-1
    
    [dc-1-pg]
    # Listing of all Postgres nodes in dc-1
    
    [dc-1-pgmaster]
    # Listing of the single Postgres master node in dc-1
    
    [dc-1-pgstandby]
    # Listing of the single Postgres standby node in dc-1
    
    [dc-1-ui]
    # Listing of the UI node in dc-1
    
## Zookeeper Observer Nodes
Zookeeper nodes can be designated as an observer node. Ansible inventory files allow variables to be assigned to servers.
These roles will update the silent installation configuration file correctly for any zookeeper node that is assigned the 
 variable zk_observer.
  
     zk_observer=true
