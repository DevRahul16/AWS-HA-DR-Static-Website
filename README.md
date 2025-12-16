# AWS High Availability & Disaster Recovery – Static Website

## 📌 Project Overview
This project demonstrates a **High Availability (HA)** and **Disaster Recovery (DR)** architecture on **AWS** for hosting a **static website** using a **multi-region deployment**.

- **Primary Region:** ap-south-1 (Mumbai)
- **Disaster Recovery Region:** us-east-1 (N. Virginia)
- **Traffic Management:** Amazon Route 53 (DNS Failover)

---

## 🏗 Architecture Diagram
![HA-DR Architecture](./HA-&DM.png)

---

## 🧩 Architecture Components
- **Route 53:** DNS failover with health checks
- **VPC:** Separate VPC per region
- **ALB:** Highly available load balancing
- **ASG:** Automatic scaling of EC2 instances
- **EC2:** Apache web server hosting static site

---

## 🚀 Traffic Flow
1. User accesses the domain
2. Route 53 routes traffic to the Primary region
3. ALB forwards traffic to EC2 instances
4. On failure, traffic shifts automatically to DR region

---

## 📘 Setup Guide
For detailed implementation steps, refer to:
👉 [Setup Guide](./setup-guide.md)

---

