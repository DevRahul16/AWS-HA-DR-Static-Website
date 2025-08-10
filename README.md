# High Availability (HA) & Disaster Recovery (DR) – Static Website Deployment

## 📌 Scenario
Host a static website in **Mumbai Region** (Primary) with a backup in **Singapore Region** (Disaster Recovery).  
The setup ensures automatic failover using **Route 53** if the primary site becomes unavailable.

---

## 🛠 Architecture Overview

![Route53-HR-DR](/uploads/899c865192fae1f548902b8e073e8a0b/Route53-HR-DR.png)


---

## 🚀 Deployment Steps

### **1️⃣ Mumbai Region – Primary Setup**

#### Launch EC2 Instance
- **Name:** `server-1`
- **AMI:** Amazon Linux (latest version)
- **Instance type:** `t2.micro`
- **Key Pair:** Choose existing or create a new one
- **Security Group:** Allow **SSH (22)** and **HTTP (80)** from anywhere (0.0.0.0/0)
- **User Data:**
```bash
#!/bin/bash
sudo su -
yum install httpd -y
systemctl enable httpd --now
echo "This is Mumbai server - INDIA" > /var/www/html/index.html


**Create & Copy AMI**
1. Create an AMI from the EC2 instance.

2. Copy the AMI to Singapore Region.

Launch Template
. Create a Launch Template in Mumbai using the AMI created.

Application Load Balancer (ALB)
. Name: loadbalancer1
. Scheme: Internet-facing
. Select Availability Zones & Subnets.
. Target Group:
  . Type: instance
  . Register EC2 instances.
. Attach target group to ALB.

Auto Scaling Group (ASG)
. Name: ASG-1
. Launch template: Mumbai template
. Minimum capacity: 1
. Maximum capacity: 2
. Attach to the target group.

2️⃣ Singapore Region – DR Setup
Repeat the same steps as Mumbai:

Launch Template
. Create a Launch Template using the copied AMI.

Application Load Balancer
. Create ALB in Singapore.
. Create a Target Group and register DR instances.

Auto Scaling Group
. Name: ASG-2
. Minimum capacity: 1
. Maximum capacity: 2
. Attach to the target group.

3️⃣ Route 53 – DNS & Failover Setup
Create Hosted Zone
. Domain: routeninja.xyz
. Type: Public Hosted Zone.

Create Health Checks
. Health Check 1: Mumbai ALB DNS
. Health Check 2: Singapore ALB DNS

Create DNS Records
. Primary Record:
  . Name: www.routeninja.xyz
  . Type: A (Alias)
  . Alias to Mumbai ALB DNS
  . Routing Policy: Failover → Primary
  . Associate with Mumbai Health Check

. Secondary Record:
  . Name: www.routeninja.xyz
  . Type: A (Alias)
  . Alias to Singapore ALB DNS
  . Routing Policy: Failover → Secondary
  . Associate with Singapore Health Check

Update Domain Registrar
. Copy Name Servers from Route 53 Hosted Zone.
. Update them in your domain registrar settings.

✅ End Result
. Website serves from Mumbai Region by default.
. If Mumbai fails, traffic automatically routes to Singapore Region.
