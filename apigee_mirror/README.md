Apigee Mirror Playbook Sample
=============================

This playbook demonstrate how to work with an Apigee OPDK mirror. This playbook creates an installation with the 
components needed to carry out the following activities: 
 
 * Create an Apigee Mirror
 * Retrieve an Apigee Mirror
 * Upload an Apigee Mirror
 * Install an Apigee Mirror
 
# Creating and Retrieving an Apigee Mirror
Assuming you need to create an Apigee mirror, then you can use the following playbook with default settings to create a 
minimum environment that will create and download an Apigee mirror: 

    ansible-playbook create_download_apigee_mirror.yml -vv -b
    
## Create an Apigee Mirror
Assuming you have a working instance of Apigee OPDK and you need to create an Apigee mirror with the playbook default 
settings, then you can use the following:

    ansible-playbook create_download_apigee_mirror.yml -vv -b --tags=create
    
## Retrieve an Apigee Mirror
Assuming you have created an Apigee OPDK mirror with the default settings and you need to download an Apigee mirror, 
then you can use the following playbook: 
 
    ansible-playbook create_download_apigee_mirror.yml -vv -b --tags=download

# Uploading and Installing an Apigee Mirror
Assuming you need to upload and install an Apigee mirror with the playbook default settings, then you can use the 
following:
   
    ansible-playbook upload_install_apigee_mirror.yml -vv -b
    
## Upload an Apigee Mirror
Assuming you have an Apigee OPDK mirror in the location set by the playbook default settings and you need to upload the
mirror to a server, then you can use the following:

    ansible-playbook upload_install_apigee_mirror.yml -vv -b --tags=upload

## Install an Apigee Mirror
Assuming you have an Apigee OPDK mirror already uploaded to the location set by the playbook default settings and you 
need to install that Apigee mirror, then you can use the following:

    ansible-playbook upload_install_apigee_mirror.yml -vv -b --tags=install
