# Creating the EC2 Instance with Terraform

The first step was creating the EC2 instance using Terraform.

The instance configuration included the required AWS provider, AMI, instance type and networking configuration.

I also attached a VPC security group to the instance so that the required traffic could reach the server.

The security group allowed HTTP traffic so the web server could be accessed from the internet.

<img width="488" height="537" alt="tf_p2 main tf p1" src="https://github.com/user-attachments/assets/9bcb27d6-832b-4458-a8ec-261cbdf66745" />

<img width="355" height="605" alt="tf_p2 main tf p2" src="https://github.com/user-attachments/assets/1ebcffa0-f11e-44c8-b8f9-00344e30ebd1" />



# Creating the Cloud-Init Configuration

I then created a cloud-init.yaml file.

Cloud-init is responsible for configuring the operating system when the EC2 instance first boots.
package_update: true tells cloud-init to update the package repositories before installing the required software.
package's: tells it to download the packages that we need , in our case it was NGINX.
runcmd: tells it to run and start these packages

<img width="282" height="242" alt="tf_p2 yaml " src="https://github.com/user-attachments/assets/117bccdf-0d36-4c7c-8b1b-f20c79e5c648" />



# Connecting Cloud-Init to Terraform

The next step was passing the cloud-init file to the EC2 instance through Terraform.
Terraform reads the contents of cloud-init.yaml and passes it to the EC2 instance as user data.



# Terraform Variables and Outputs

I used Terraform variables to avoid hardcoding values directly into the configuration.

The outputs were used to make useful information available after deployment, such as the instance’s public IP address.

After applying the configuration, Terraform displayed the output values in the terminal.


<img width="329" height="196" alt="tf_p2 variable" src="https://github.com/user-attachments/assets/ff1747ec-c67f-4033-a75f-07aac4142dc9" />



# Cloud-Init Configuration on Boot

After the EC2 instance started, cloud-init automatically executed the configuration.

This handled the initial setup without requiring any manual commands on the server.

This is the main purpose of the project: the server should be ready automatically after deployment.



# Testing the Deployment

Once the instance had finished booting, I used the Terraform output to find the public IP address.

I then accessed the server through its public address to confirm that the web server was running successfully.

This confirmed that:

The EC2 instance was created successfully
The security group allowed the required traffic
Cloud-init executed correctly
The required software was installed
The web server was accessible


<img width="406" height="86" alt="tf_p2 outputs" src="https://github.com/user-attachments/assets/adc12c44-f29c-4e37-9a77-d1ed7e3f1c28" />
<img width="1273" height="661" alt="tf_p2 nginx" src="https://github.com/user-attachments/assets/5d0a9050-6620-4141-be4c-43a170060126" />




This project helped me understand how Terraform and cloud-init complement each other.

Terraform is responsible for creating the infrastructure, while cloud-init handles the initial configuration of the operating system.

The result is a repeatable deployment where a new EC2 instance can be created and configured automatically rather than manually setting up every server.


# Troubleshooting

During the deployment, I initially had an issue where the EC2 instance was created successfully, but the web server was not accessible.

After checking the Terraform configuration, I found that the VPC security group was not correctly associated with the EC2 instance.

This meant that although the instance and cloud-init configuration were working, the required incoming HTTP traffic was not being allowed.

I fixed this by attaching the correct security group to the EC2 instance in Terraform.



