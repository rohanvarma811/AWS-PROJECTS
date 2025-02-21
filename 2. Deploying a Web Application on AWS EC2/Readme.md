# Jenkins Deployment on AWS EC2
This project demonstrates the deployment of Jenkins on an AWS EC2 instance, configuring security settings, and making it accessible over the internet. This showcases skills in AWS cloud computing, Linux server administration, and infrastructure setup.

## AWS Services & Tools Used
✅ Amazon EC2 – Virtual server to host Jenkins

✅ Security Groups – Configured inbound rules to allow access on port 8080

✅ SSH (Secure Shell) – Connected securely to the instance

✅ Ubuntu (Linux OS) – Hosted Jenkins on a Linux-based server

✅ Jenkins (CI/CD Tool) – Installed and configured for automation

## Implementation Steps
1️⃣ Launch EC2 Instance – Started an Ubuntu EC2 instance and set up an SSH key pair for secure access.

2️⃣ Connect via SSH – Used command "ssh -i "AWS-Login.pem" ubuntu@<Public-IP>" in your downloads folder to connect, ensuring secure permissions with chmod 600 AWS-Login.pem.

3️⃣ Update System – Run "sudo apt update" & "sudo apt upgrade -y" to keep everything up to date.

4️⃣ Install Java & Jenkins – Install OpenJDK 11 and followed the official steps to set up Jenkins.

5️⃣ Start & Verify Jenkins – Check if Jenkins was running using systemctl status jenkins.

6️⃣ Configure Security Groups – Open port 8080 in AWS Security Groups to allow external access.

7️⃣ Access Jenkins – Open http://<EC2-Public-IP>:8080, enter the admin password, and log-in successfully.

# Output & Learnings
✔️ Successfully deployed Jenkins on AWS EC2 and made it publicly accessible.

✔️ Gained hands-on experience with AWS EC2, SSH, Linux server administration, networking (Security Groups), and Jenkins configuration.

✔️ Demonstrated the ability to set up a CI/CD automation tool in a cloud environment.