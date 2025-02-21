# AWS Security using Security Groups and NACL 

AWS (Amazon Web Services) provides multiple layers of security to protect resources and data within its cloud infrastructure. Two important components for network security in AWS are Security Groups and Network Access Control Lists (NACLs). Let's explore how each of them works:


## Project Architecture Diagram

![Screenshot 2023-06-29 at 12 14 32 AM](https://github.com/iam-veeramalla/aws-devops-zero-to-hero/assets/43399466/30bbc9e8-6502-438b-8adf-ece8b81edce9)

## Project Setup:
1️⃣ Setting Up the AWS Environment

1. Create a VPC (Virtual Private Cloud)
2. Created a custom VPC with CIDR block 10.0.0.0/16
3. Ensured that the VPC spans across multiple availability zones

- ✅ Subnet Configuration | Created public and private subnets within the VPC

1. Public Subnet: Assigned an internet gateway for external access
2. Private Subnet: No direct internet access (secured for internal resources)

- ✅ Attach Internet Gateway

1. Created an Internet Gateway (IGW) and attached it to the VPC
2. Configured route tables to allow internet access to the public subnet

##

2️⃣ Configuring Security Groups (Instance-Level Security)

- ✅ Created a Security Group for Public EC2 Instance
1. Inbound Rules:
   - Allowed SSH (port 22) access only from a specific IP (your public IP)
   - Allowed HTTP (port 8000) for web traffic

2. Outbound Rules:
   - Allowed all outbound traffic (0.0.0.0/0)

##

3️⃣ Configuring Network ACLs (Subnet-Level Security)
- ✅ Created a Network ACL for the Public Subnet

1. Inbound Rules:
   - Allowed SSH (port 22) from a trusted IP range
   - Allowed HTTP (port 8000)

2. Outbound Rules:
   - Allowed all traffic to any destination

##

4️⃣ Testing & Validation
- ✅ Testing SSH & HTTP Access

1. Verified that SSH access works only from the allowed IP
2. Checked that HTTP/HTTPS traffic is accessible from the internet

- ✅ Testing Private Subnet Restrictions
1. Tried accessing the private EC2 directly (should fail)
2. Verified that only the Public EC2 can connect to the Private EC2

- ✅ Testing NACLs Restrictions
1. Blocked an IP in NACL and checked if it was denied access
2. Logged access attempts using VPC Flow Logs

# Output & Learnings

✔️ Secure Public EC2: Only accessible via SSH from a trusted IP and allows HTTP/HTTPS traffic
  
✔️ Secure Private EC2: No direct internet access, only accessible via Public EC2
  
✔️ Network ACLs Enforcing Rules: Prevent unauthorized access at the subnet level
  
✔️ Security Groups Ensuring Fine-Grained Control: Instance-level access restrictions applied