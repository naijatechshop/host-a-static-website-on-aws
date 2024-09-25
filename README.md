# Static Website Hosting on AWS

This project demonstrates how to host a static HTML web app on AWS using an array of AWS services to ensure reliability, fault tolerance, scalability, and security. The infrastructure is automated using AWS resources and scripts, as outlined below.

## Architecture Overview

The architecture includes a robust, scalable system design, leveraging key AWS services:

1. **VPC Configuration**: A Virtual Private Cloud (VPC) is set up with both public and private subnets spanning two different Availability Zones, enhancing fault tolerance.
   
2. **Internet Gateway**: An Internet Gateway is deployed to enable communication between the VPC instances and the internet.

3. **Security Groups**: Network firewall mechanisms are established through Security Groups to allow controlled access to the necessary services.

4. **Public Subnets**: Public subnets are utilized for key infrastructure components like the NAT Gateway and the Application Load Balancer.

5. **Private Subnets**: EC2 instances hosting the static website are placed within private subnets for enhanced security, ensuring that they are not directly exposed to the internet.

6. **NAT Gateway**: Instances within private subnets access the internet securely through a NAT Gateway.

7. **Auto Scaling Group**: An Auto Scaling Group is implemented to maintain desired instance capacity, ensuring website availability, fault tolerance, and elasticity.

8. **Application Load Balancer**: An Application Load Balancer evenly distributes incoming traffic to the EC2 instances within the Auto Scaling Group, improving reliability and load distribution across Availability Zones.

9. **SSL Encryption**: AWS Certificate Manager is used to secure application communications via HTTPS.

10. **Monitoring and Notifications**: AWS Simple Notification Service (SNS) is configured to alert you about changes in the Auto Scaling Group.

11. **DNS Configuration**: The domain name for the web app is registered and managed through Route 53, with DNS records set up accordingly.

## Getting Started

To replicate this project, follow the instructions below.

### Prerequisites

- AWS account with administrative access.
- Git installed locally.
- Domain name registered via Route 53.
- SSL Certificate provisioned using AWS Certificate Manager (ACM).

### Deployment Steps

1. **VPC Setup**: Create a VPC with public and private subnets across two Availability Zones, and deploy an Internet Gateway for public subnet instances to access the internet.

2. **Configure NAT Gateway**: Deploy a NAT Gateway within the public subnet to enable private subnet instances to communicate with the internet securely.

3. **Security Groups**: Set up Security Groups allowing only necessary traffic (e.g., HTTP/HTTPS and SSH for the bastion host).

4. **EC2 Instance Setup**: Launch EC2 instances within private subnets and associate them with the Auto Scaling Group.

5. **Install Apache & Deploy Web App**: Use the following bash script to configure your EC2 instances and deploy the static website:

    ```bash
    #!/bin/bash
    sudo su
    yum update -y
    yum install -y httpd
    cd /var/www/html
    yum install git -y
    git clone https://github.com/naijatechshop/host-a-static-website-on-aws.git
    cp -R host-a-static-website-on-aws/. /var/www/html/
    rm -rf host-a-static-website-on-aws
    systemctl enable httpd
    systemctl start httpd
    ```

6. **Auto Scaling and Load Balancer**: Configure an Auto Scaling Group to manage the EC2 instances and an Application Load Balancer to distribute traffic.

7. **SSL and DNS Setup**: Use AWS Certificate Manager to secure your website with HTTPS, and Route 53 to configure the domain name DNS records.

## Monitoring & Notifications

- Set up AWS SNS to receive alerts on EC2 scaling activities, load balancer health checks, or instance health issues.


This project is open-source and hosted on GitHub for collaboration and version control. View the project [here](https://github.com/naijatechshop/host-a-static-website-on-aws).
