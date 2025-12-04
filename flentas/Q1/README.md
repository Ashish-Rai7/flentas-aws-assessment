# Terraform-Based AWS Basic Network Configuration

 This project shows how to use Terraform to create a simple yet production-style AWS networking design.  One Virtual Private Cloud (VPC), two public and private subnets, an Internet gateway, and a NAT gateway to regulate internet access are all part of the configuration.  This project aims to comprehend the design and configuration of a secure and scalable cloud network utilising Infrastructure as Code.

 ## Overview of Architecture

 The following elements make up the architecture:

 Two Public Subnets (across two Availability Zones) and one VPC
 Two private subnets (spanning two zones of availability)
 One NAT gateway, one Internet gateway, and two route tables (public and private)

 Private subnets are kept segregated and can only contact the internet via the NAT Gateway for outgoing traffic, whereas public subnets are used for resources that front the internet.

 ## 📐 CIDR Design and Description

 | CIDR Range | Resource |
 |----------|------------–|
 10.0.0.0/16 | VPC |
 10.0.1.0/24 | Public Subnet 1 |
 10.0.2.0/24 | Public Subnet 2 |
 10.0.11.0/24 | Private Subnet 1 |
 10.0.12.0/24 | Private Subnet 2 |

 **Why these ranges were chosen:**

 To enable good scalability, the VPC uses a /16 range.
 For simple IP management, a /24 block is used to form each subnet.
 To reduce confusion and enhance readability, public and private subnets are located in different ranges.
 For high availability, subnets are dispersed over various availability zones.

 ## 🌐 NAT Gateway & Internet Configuration

 To allow public subnets to access the internet, the Internet Gateway (IGW) is connected to the VPC.
 One public subnet contains the NAT Gateway.
 In order to provide secure internet access without being exposed to incoming traffic, private subnets route their outgoing traffic to the NAT Gateway.

 ---

 ## 🛣️ Configuration of Route Table

 ### Table of Public Routes:
 Route: `0.0.0.0/0 → Internet Gateway`
 It is connected to both public subnets.

 ### Table of Private Routes:
 Route: `0.0.0.0/0 → NAT Gateway`
 It is connected to both private subnets.

 ## ⚙️ Tools & Services Used

- AWS (VPC, Subnets, IGW, NAT Gateway, Route Tables)
- Terraform (for Infrastructure as Code)
- GitHub (for version control)


Important !! 

The VPC and networking setup was intended to be automated using Terraform.  But as I'm still learning how to use Infrastructure as Code tools, this process was done by hand using the AWS Management Console to make sure the network design was correct.  As part of my ongoing education, I intend to use Terraform to construct the same configuration because I recognise its significance for automation.