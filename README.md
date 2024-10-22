![Alt text](/aws-staticWebsite.png)

---

# Host a Static Website on AWS

This project demonstrates how to host a static HTML web application on AWS, utilizing a range of AWS services and resources to achieve scalability, reliability, security, and fault tolerance. The website is hosted on EC2 instances and managed with an Auto Scaling Group, with traffic distributed using an Application Load Balancer. This project is designed to follow best practices for hosting a web application on AWS, including VPC setup, secure subnets, and traffic management.

## Project Architecture Overview

The static website is deployed on AWS infrastructure configured as follows:

1. **Virtual Private Cloud (VPC)**:  
   - Configured with public and private subnets across two different availability zones for high availability and fault tolerance.

2. **Internet Gateway**:  
   - Facilitates connectivity between the instances in the VPC and the internet.

3. **Security Groups**:  
   - Act as a firewall to control inbound and outbound traffic to instances.

4. **Multi-AZ Setup**:  
   - Leverages two Availability Zones for improved fault tolerance.

5. **Public Subnets**:  
   - Contains the NAT Gateway and Application Load Balancer, ensuring that resources within private subnets can connect to the internet securely.

6. **Private Subnets**:  
   - Hosts web servers (EC2 instances) to improve security by restricting direct public access.

7. **EC2 Instance Connect Endpoint**:  
   - Securely connects to instances within both public and private subnets.

8. **NAT Gateway**:  
   - Allows instances within the private subnets to access the internet for updates and external communication.

9. **EC2 Instances**:  
   - Web servers running in private subnets to serve the static website.

10. **Application Load Balancer (ALB)**:  
    - Evenly distributes incoming web traffic across multiple EC2 instances in different availability zones for better performance and availability.

11. **Auto Scaling Group (ASG)**:  
    - Automatically adjusts the number of EC2 instances based on traffic, ensuring high availability and elasticity.

12. **GitHub Integration**:  
    - The web files are version-controlled using GitHub, allowing for easy updates and collaboration.

13. **AWS Certificate Manager (ACM)**:  
    - Secures communication between the ALB and clients via SSL certificates.

14. **Amazon Simple Notification Service (SNS)**:  
    - Sends alerts regarding activities and changes within the Auto Scaling Group.

15. **Amazon Route 53**:  
    - Manages the domain name and DNS records for the website.

## Deployment Steps

1. **VPC and Subnets Configuration**:  
   Set up a Virtual Private Cloud (VPC) with public and private subnets across two availability zones, and configure security groups, NAT Gateway, and Internet Gateway.

2. **Launch EC2 Instances**:  
   Launch EC2 instances in private subnets, ensuring they are part of an Auto Scaling Group for automatic scaling based on traffic.

3. **Install Apache Web Server**:  
   After connecting to the EC2 instance, use the script below to set up Apache and deploy the web application.

4. **Clone the GitHub Repository**:  
   Clone the website files from GitHub and serve them via Apache.

5. **Load Balancer and Auto Scaling Configuration**:  
   Configure the Application Load Balancer to distribute traffic and Auto Scaling Group to manage the EC2 instances automatically.

6. **SSL Certificates and DNS Setup**:  
   Use AWS Certificate Manager to secure communications and Route 53 for domain name management.

## Installation Script

```bash
#!/bin/bash
# Switch to the root user to gain full administrative privileges
sudo su

# Update all installed packages to their latest versions
yum update -y

# Install Apache HTTP Server
yum install -y httpd

# Change the current working directory to the Apache web root
cd /var/www/html

# Install Git
yum install git -y

# Clone the project GitHub repository to the current directory
git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git

# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R host-a-static-website-on-aws/. /var/www/html/

# Remove the cloned repository directory to clean up unnecessary files
rm -rf host-a-static-website-on-aws

# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd

# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

## Prerequisites

- AWS account with necessary IAM permissions to create VPCs, EC2 instances, NAT Gateways, and configure Route 53, ALB, and ACM.
- GitHub account for version control.
- Domain name registered with Route 53 (optional).

## Conclusion

This project showcases the deployment of a static website on AWS, leveraging a wide array of AWS services to ensure scalability, security, and fault tolerance. By using the provided architecture and scripts, you can easily deploy a static website on AWS EC2 instances, distribute traffic using an ALB, and automatically scale your infrastructure based on demand.

For more detailed information or to contribute, visit the [GitHub repository][(https://github.com/TheodoreOb3n/aws-staticWebsite).]

---
