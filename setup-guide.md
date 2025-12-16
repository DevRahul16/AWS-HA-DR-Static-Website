# Setup Guide – AWS HA & DR Static Website

This guide explains how to deploy a **multi-region HA & DR static website** on AWS.

---

## 🏗 Step 1: Create VPCs
- **Mumbai:** CIDR 10.0.0.0/16
- **Virginia:** CIDR 20.0.0.0/16

---

## ⚙️ Step 2: EC2 & Auto Scaling
- Amazon Linux 2 AMI
- Instance type: t2.micro
- Install Apache web server

---

## 🌐 Step 3: Load Balancers
- Create Application Load Balancer
- Configure Target Groups per region

---

## 🌍 Step 4: Route 53 Failover
- Primary record → Mumbai ALB
- Secondary record → Virginia ALB
- Routing policy: Failover

---

## 🔍 Step 5: DR Testing
- Stop EC2 instances in Mumbai
- Verify traffic shifts to Virginia
