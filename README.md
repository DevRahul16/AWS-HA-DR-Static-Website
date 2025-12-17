# AWS High Availability & Disaster Recovery – Static Website

## 📌 Project Overview
This project demonstrates a **High Availability (HA)** and **Disaster Recovery (DR)** architecture on **AWS** designed to ensure continuous uptime, fault tolerance, and automatic failover across multiple regions.

The architecture is built to handle:
- EC2 instance failures
- Availability Zone outages
- Complete regional failures

---

## 🏗️ Architecture

![HA-DR Architecture](./HA-&DM.png)

The architecture consists of:

- **Two VPCs** in different AWS regions (for fault isolation and disaster recovery)
- **Auto Scaling Groups (ASG)** in each region to automatically scale EC2 instances
- **Two EC2 instances per region** to ensure in-region redundancy
- **Application / Elastic Load Balancer (ALB/ELB)** in each region to distribute traffic
- **Amazon Route 53** configured with DNS failover to route traffic between regions

---

## 📌 Traffic Flow

1. User accesses the application domain
2. **Route 53** routes traffic to the nearest healthy region
3. **Load Balancer** distributes requests to EC2 instances
4. **Auto Scaling** adjusts instance count based on demand
5. If one region becomes unavailable, **Route 53 automatically redirects traffic** to the secondary region

---

## ⚙️ AWS Services Used

| Service | Purpose |
|------|------|
| **VPC** | Isolated networking environment |
| **EC2** | Web / application server instances |
| **Auto Scaling** | Automatic scaling and self-healing |
| **ALB / ELB** | Traffic distribution |
| **Route 53** | DNS failover and disaster recovery |
| **S3 (Optional)** | Static content & backups |
| **CloudWatch** | Monitoring and alerts |

---

## 🚀 Deployment Steps (High Level)

1. Create **VPCs** in two different AWS regions
2. Launch **Auto Scaling Groups** with EC2 instances in each VPC
3. Attach **Load Balancers** to distribute traffic
4. Configure **Route 53 Failover Policy**
   - **Primary:** Region 1 Load Balancer
   - **Secondary:** Region 2 Load Balancer
5. Test failover by stopping instances or simulating regional failure

---

## 📊 High Availability & Disaster Recovery Benefits

- **Fault Tolerance:**  
  Even if one EC2 instance fails, others in the ASG continue serving traffic

- **Regional Redundancy:**  
  If an entire AWS region fails, traffic is redirected to another region

- **Scalability:**  
  Auto Scaling adjusts resources based on traffic demand

- **Business Continuity:**  
  Ensures uptime and service availability during disasters

---

## 📘 Setup Guide
For detailed step-by-step implementation instructions, refer to:

👉 **[Setup Guide](./setup-guide.md)**

---


