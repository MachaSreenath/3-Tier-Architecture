# 🌐 3-Tier Architecture on AWS

## 📖 What is 3-Tier Architecture?

A **3-tier architecture** is a common software architecture pattern used in web applications. It divides an application into **three distinct layers**:

1. **Web Tier (Presentation Layer)** – Handles user interactions. Hosts front-end web servers accessed by users through a browser.
2. **Application Tier (Logic Layer)** – Processes business logic and handles data communication between the web and database layers.
3. **Database Tier (Data Layer)** – Stores and manages data securely. Only the application layer can directly access it.

This architecture promotes **scalability**, **security**, and **maintainability** by isolating responsibilities across the layers.

---

## 🛠️ Project Overview

This project demonstrates the implementation of a **3-tier architecture on AWS** by provisioning network components, compute instances, load balancers, and a managed database. The entire setup is created manually using AWS Management Console.

---

## ⚙️ Implementation Steps

### ✅ **Step 1: VPC and Networking Setup**
- Created a **custom VPC**
- Created **6 subnets**:
  - 2 Public Subnets (for Web Tier)
  - 4 Private Subnets (2 for App Tier, 2 for DB Tier)
- Created and attached an **Internet Gateway**
- Created **2 Route Tables**:
  - Public Route Table associated with public subnets and Internet Gateway
  - Private Route Table connected to **NAT Gateway** for internet access from private subnets

---

### ✅ **Step 2: EC2 Instance Launch**
- Launched **2 EC2 instances in public subnets** (Web Tier)
- Launched **2 EC2 instances in private subnets** (App Tier)

---

### ✅ **Step 3: Load Balancers**
- Created **2 Target Groups**:
  - One for Web Tier instances
  - One for App Tier instances
- Configured:
  - **Public Application Load Balancer** (Internet-Facing) for Web Tier
  - **Private Application Load Balancer** (Internal) for App Tier

---

### ✅ **Step 4: Create AMIs**
- Created **Amazon Machine Images (AMI)** of EC2 instances for auto scaling

---

### ✅ **Step 5: Auto Scaling Groups**
- Created **Launch Templates** and **Auto Scaling Groups** for both:
  - Public Web Tier
  - Private App Tier
- Auto scaling configured to launch additional instances as needed

---

### ✅ **Step 6: Subnet Group**
- Created a **Subnet Group** to use with the RDS database in private subnets

---

### ✅ **Step 7: RDS Database (DB Tier)**
- Launched a **MySQL RDS instance** in private subnets
- Database is **not publicly accessible**

---

### ✅ **Step 8: Connectivity and Testing**
Connected to the App Tier EC2 instance and installed MySQL client:
```bash
sudo -i
apt update -y
apt install mysql-server -y
