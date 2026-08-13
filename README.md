# Assignment 2 – EC2 Deployment with Cloud-Init

This project demonstrates how Terraform and cloud-init can be used together to automatically deploy and configure an AWS EC2 instance.

The goal was to have the EC2 instance come online fully configured without requiring any manual setup.

What I Built

* Provisioned an EC2 instance using Terraform
 
* Created a cloud-init YAML configuration
  
* Used cloud-init to update packages and install/configure a web server
  
* Passed the cloud-init configuration to EC2 using Terraform user_data
  
* Configured the required VPC and security group settings
  
* Used Terraform variables and outputs to keep the configuration organised
  
* Verified that the web server was accessible once the instance finished booting
