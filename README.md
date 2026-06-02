# High-Availability Web Tier (Project 2)

This repository documents the deployment of a resilient, scalable web architecture on AWS. It demonstrates the transition from manual server management to automated, self-healing infrastructure.

**Live Site:** [portfolio-alb-1039296210.us-east-2.elb.amazonaws.com](http://portfolio-alb-1039296210.us-east-2.elb.amazonaws.com)

---
<p align="center">
  <img src="./EC2 Architecture Diagram" alt="EC2 Architecture Diagram" width="650">
</p>
---

## 📐 Infrastructure Design

The architecture uses a multi-tier approach to ensure 99.9% availability:

* **Networking:** A custom VPC with Public Subnets across two Availability Zones (AZs).
* **Compute:** EC2 instances running a Flask web application, managed by an Auto Scaling Group (ASG).
* **Traffic Management:** An Application Load Balancer (ALB) acting as a single entry point for all users.
* **Automation:** Launch Templates using a "Golden Image" (AMI) for instant server replication.

---

## 🛠️ Key Achievements & Challenges

### **1. Solving the "Timed Out" Error**
During the initial deployment, the site was unreachable. I successfully troubleshot this by identifying that the **ALB Security Group** was blocking traffic.
* **Fix:** Opened Port 80 to `0.0.0.0/0`.
* **Result:** Established a secure flow where only the Load Balancer can talk to the private backend servers.

### **2. Self-Healing Test**
To verify fault tolerance, I manually terminated a running instance. 
* **Outcome:** The Auto Scaling Group detected the failure via **ELB Health Checks** and launched a new instance automatically, keeping the site live without manual intervention.

---

## 🚀 Deployment Steps

1.  **Image Creation:** Created a custom AMI from a configured Flask environment.
2.  **VPC Setup:** Manually mapped subnets, route tables, and an internet gateway.
3.  **Load Balancing:** Configured an ALB with a Target Group monitoring instance health.
4.  **Auto Scaling:** Set scaling limits (Min: 1, Max: 3) to handle traffic spikes and hardware failures.

---

## 📂 Project Structure
* `app.py`: The Flask web application backend.
* `README.md`: Documentation of the architecture and deployment process.
