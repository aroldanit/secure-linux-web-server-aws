# Secure Linux Web Server on AWS

## Overview

This project deploys a **hardened Linux web server** on AWS using an EC2 instance, with a focus on:

- Basic **infrastructure setup** (EC2, security groups)
- **Linux administration** (user management, packages, services)
- **Security hardening** (SSH, firewall, updates, logging)
- Serving a simple web page over HTTP (optionally HTTPS later)

It’s designed to demonstrate that I can manage a Linux server in the cloud **securely**, not just “get something running.”

---

## What This Demonstrates to Employers

- Ability to launch and configure an **EC2 instance** on AWS.
- Understanding of **security groups** and basic network restrictions.
- Practical **Linux admin skills**:
  - Users, groups, permissions
  - Package management
  - Services (`systemctl`)
- Awareness of **security best practices**:
  - SSH key-based access
  - Disabling password login
  - Basic OS hardening
  - Firewall rules
- Clear documentation of what was done and why.

---

## Tech Stack

- **Cloud:** AWS (EC2, Security Groups)
- **OS:** Ubuntu Server (or Amazon Linux – specify which)
- **Web Server:** NGINX or Apache
- **Security:** SSH hardening, firewall (UFW or `iptables`), least privilege

---

## Architecture

_See `docs/architecture-diagram.png`_

**High-level design:**

- A single EC2 instance in a **public subnet**.
- An **SSH security group** allowing access only from my IP.
- An **HTTP security group** allowing access on port 80 (and optionally 443).
- A hardened Linux server running a simple web app (static HTML page).

---

## How to Reproduce This Setup

> **Warning:** This will create billable resources in AWS.  
> Remember to **stop/terminate** the EC2 instance when finished.

### 1️⃣ Launch EC2 Instance

1. Log in to the AWS console.
2. Navigate to **EC2 → Instances → Launch instance**.
3. Choose an AMI (e.g., **Ubuntu 22.04 LTS**).
4. Choose instance type (e.g., `t2.micro` or `t3.micro`).
5. Create or select an **SSH key pair**.
6. Configure **networking**:
   - Public subnet
   - Auto-assign public IP: **Enabled**
7. Create a **security group**:
   - Allow **SSH (22)** from your IP only.
   - Allow **HTTP (80)** from `0.0.0.0/0` (for public access).
8. Launch the instance.

### 2️⃣ Connect via SSH

```bash
ssh -i /path/to/your-key.pem ubuntu@<ec2-public-ip>
