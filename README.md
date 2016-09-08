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

Two folders are provided to help you setup your workspace. The folders are named environments and installations.
 
## environments folder

Contains accelerator files for using Vagrant. 

## installations folder 

Contains configurations to support installing a single node aio profile.

Installing Ansible Roles
========================

It is necessary to install the Ansible roles on your control server. This can be accomplished with the provided 
install_roles.yml. Please use ansible-galaxy to download and install the roles: 

    ansible-galaxy install -r install_roles.yml
    
Please note that you can obtain any updates by using -f (force): 
 
     ansible-galaxy install -fr install_roles.yml

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

## Inventory Planet and Installation Role Conventions 
A planet refers to all server nodes across all data centers. These semantics are held via the use of group names for  
all nodes that fulfill a specific purpose. The installation roles provide the semantic model we followed. The inventory 
file group names for planet level semantics are listed as follows: 

    [planet]
    # Listing of all nodes
    
    [ds]
    # Listing of all the Cassandra and Zookeeper nodes
    
    [ms]
    # Listing of all the Management Server nodes
    
    [ldap]
    # Listing of all the OpenLDAP nodes
    
    [rmp]
    # Listing of all the Router and Message Processor nodes
     
    [qpid]
    # Listing of all Qpid nodes
    
    [pg]
    # Listing of all Postgres nodes
    
    [pgmaster]
    # Listing of the single Postgres master node
    
    [pgstandby]
    # Listing of the single Postgres standby node
    
    [ui]
    # Listing of all UI nodes
    
## Inventory Region and Installation Role Conventions
A region represents subset of a planet. The semantics used for installation roles are congruent with a region. Region 
have been referenced as data centers. The internal configurations of OPDK and BaaS support many regions as dc-1, dc-2 
and so forth. Following this historical precedent we also define the regions with their corresponding installation role
to provide a semantic model as follows:
 
    [dc-1]
    # Listing of all nodes in data center 1 (dc-1)
    
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
 

