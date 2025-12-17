# Setup Guide – High Availability & Disaster Recovery on AWS

This guide provides step-by-step instructions to implement the **HA & DR architecture** described in `README.md`.

---

## 🏗️ Step 1: Create VPCs in Two Regions

### Region A – Primary (ap-south-1: Mumbai)
1. Go to **VPC Dashboard**
2. Create a VPC
   - CIDR block: `10.0.0.0/16`
3. Create **2 public subnets** in different Availability Zones

---

### Region B – Secondary / DR (us-east-1: N. Virginia)
1. Switch to **us-east-1**
2. Create a VPC
   - CIDR block: `20.0.0.0/16`
3. Create **2 public subnets** in different Availability Zones

---

## ⚙️ Step 2: Launch EC2 Instances & Auto Scaling

### Region A
1. Go to **EC2 Dashboard**
2. Create a **Launch Template**
   - AMI: Amazon Linux 2 / Ubuntu
   - Instance type: `t2.micro`
   - Security Group:
     - SSH (22)
     - HTTP (80)
     - HTTPS (443)

3. User Data (optional):
```bash
#!/bin/bash
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "Hello from Region A" > /var/www/html/index.html

