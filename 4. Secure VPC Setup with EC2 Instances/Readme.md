# AWS Deployment with Bastion Host, Private Subnet EC2, and Load Balancer

This project demonstrates secure deployment of a Python-based web application inside a **private subnet** with access via a **Bastion Host**, and **load-balanced** using an Application Load Balancer (ALB). It closely simulates real-world cloud architecture used in production.

---

## 📌 Project Architecture Diagram

![AWS Private Subnet Architecture](https://github.com/user-attachments/assets/d0da4504-e2b5-4895-9330-926e630050f1) <!-- Replace with your own if needed -->

---

## 🏗️ 1️⃣ AWS VPC + Subnet Setup

- ✅ **Create VPC**  
  CIDR block: `10.0.0.0/16`  
  Name: `Prod-VPC`

- ✅ **Create Subnets**
  - `Public-Subnet-A` (10.0.1.0/24)
  - `Public-Subnet-B` (10.0.2.0/24)
  - `Private-Subnet-A` (10.0.3.0/24)
  - `Private-Subnet-B` (10.0.4.0/24)

- ✅ **Attach Internet Gateway**
  - Create IGW and attach to `Prod-VPC`
  - Update Route Table of public subnets to allow `0.0.0.0/0` via IGW


## 🔐 2️⃣ Bastion Host Setup (Public Subnet)

- ✅ Launch EC2 instance (Ubuntu, t2.micro) in `Public-Subnet-A`
- ✅ Enable auto-assign public IP
- ✅ Attach Security Group:
  - Inbound: SSH (22) from your IP
  - Outbound: All

- ✅ Save `.pem` key on local machine for SSH
- ✅ Copy `.pem` to Bastion Host:
```bash
scp -i your-key.pem your-key.pem ubuntu@<bastion-public-ip>:/home/ubuntu
```


## 🧱 3️⃣ Private EC2 Setup (Private Subnet)

- ✅ Launch 2 EC2 instances in private subnets with **no public IP**
- ✅ Use same `.pem` key
- ✅ Access via Bastion Host:
```bash
# From local → Bastion
ssh -i your-key.pem ubuntu@<bastion-ip>

# From Bastion → Private EC2
ssh -i your-key.pem ubuntu@<private-ec2-ip>
```


## 🌐 4️⃣ Deploy Python Web App

- ✅ On 1 Private EC2 instance:
```bash
echo '<h1>My First AWS Project - Private Subnet</h1>' > index.html
python3 -m http.server 8000
```

- ❌ Leave 2nd EC2 without app to demonstrate unhealthy instance in load balancer


## 🎯 5️⃣ Application Load Balancer (Public Subnet)

- ✅ Go to EC2 > Load Balancers > Create
- Type: Application Load Balancer (Layer 7)
- Scheme: Internet-facing
- Subnets: Attach both `Public-Subnet-A` and `Public-Subnet-B`
- Security Group:
  - Inbound: HTTP (80)
  - Outbound: All


## 🧩 6️⃣ Target Group Configuration

- ✅ Create Target Group:
  - Type: Instances
  - Protocol: HTTP
  - Port: 8000
  - Health Check Path: `/`
  - Attach both private EC2 instances

- ✅ Listener: HTTP 80 → Target Group

- 🔄 If health check fails:
  - Make sure Python server runs on port 8000
  - Ensure SG allows 8000 inside VPC


## 🔁 7️⃣ Load Balancing Test

- ✅ Access Load Balancer DNS:
```bash
http://<load-balancer-dns>
```

---

## ✅ Summary & Learnings

✔️ **Private EC2 Access** only via Bastion Host (SSH Jump)  
✔️ **Python App Deployed** inside private subnet  
✔️ **Application Load Balancer** enables public access  
✔️ **Target Group Health Checks** control traffic routing  
✔️ **Security Groups** manage instance-level access  
✔️ **Highly Scalable** and secure cloud design

---

## 👨‍💻 Author

**Rohan Varma**  
_Cloud & DevOps Enthusiast | Python + AWS Projects | Passionate Learner_

---
