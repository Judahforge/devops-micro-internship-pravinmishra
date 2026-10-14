# Assignment 6 — Capstone Assignment — Deploy Book Review App (Three-Tier Architecture) on AWS

Part of the DevOps Micro Internship (DMI) with Agentic AI

---

## Purpose

This is the most important assignment of the course. You will deploy the Book Review App in a fully production-style three-tier architecture on AWS: a Next.js Web Tier behind Nginx and a public ALB, a private Node.js/Express App Tier behind an internal ALB, and a private Multi-AZ MySQL RDS database with a read replica. You are expected to design, deploy, isolate, debug, and document the result independently.

---

# Task 1 — Architecture Diagram

## Goal

Create an architecture diagram showing the custom VPC (10.0.0.0/16), the six subnets across two Availability Zones (two public Web Tier, two private App Tier, two private Database Tier), the public ALB, Web Tier EC2/Nginx, internal ALB, private App Tier EC2, private Multi-AZ RDS with its read replica, and the permitted traffic flow.

### Evidence

#### Diagram image or link

![Diagram image or link](./screenshots/AS06-Architecture-Diagram.png)

---

# Task 2 — AWS Region & Services Used

## Goal

Record the AWS Region used and list every AWS service used across networking, compute, load balancing, security, and the database.

### Notes

**Region:**

us-east-1

---

**Services:**

VPC, Subnets, Internet Gateway, NAT Gateway, Elastic IP, Route Tables, Security Groups, EC2, Application Load Balancer, Target Groups, RDS for MySQL, Multi-AZ, Read Replica, DB Subnet Group, Nginx, Node.js, PM2, Git, CloudWatch optional.

---

# Task 3 — Public Entry Point

## Goal

Confirm the Book Review App loads through the public ALB DNS name.

### Evidence

#### Public ALB DNS

Paste your public ALB DNS name here:

`http://book-review-web-alb-1637490299.us-east-1.elb.amazonaws.com/`

---

# Task 4 — Evidence Screenshots

## Goal

Capture visual proof of every tier and load balancer.

### Evidence

#### Web EC2

![Web EC2](./screenshots/AS06-Web-EC2.png)

---

#### App EC2

![App EC2](./screenshots/AS06-App-EC2.png)

---

#### Public ALB

![Public ALB](./screenshots/AS06-Public-ALB.png)

---

#### Internal ALB

![Internal ALB](./screenshots/AS06-Internal-ALB.png)

---

#### RDS + Replica

![RDS + Replica](./screenshots/AS06-RDS+Replica.png)

---

#### App UI proof

![App UI proof](./screenshots/AS06-App-UI-proof.png)

---

# Task 5 — Summary

## Goal

Summarize what worked in the final deployment, the issues encountered and how each was fixed, and the tools or sources used to research and debug.

### Notes

**What worked:**

The three-tier architecture deployed successfully: Public ALB → Web EC2/Nginx → Internal ALB → App EC2/Node.js → private Multi-AZ RDS MySQL. Target groups showed healthy, PM2 kept both frontend and backend running, and the app loaded through the public ALB DNS.

---

**Issues + fixes:**

App EC2 had no public IP → used Web EC2 as a bastion/jump host.

Nginx showed default page → enabled the book-review site and removed default.

API requests hit wrong path → used proxy_pass without trailing slash to preserve /api/.

Backend stopped after SSH closed → moved to PM2 and enabled PM2 startup with systemd.

Target unhealthy → checked App SG allowed port 3001 from App SG, and backend was running.

CORS errors → added public ALB DNS to ALLOWED_ORIGINS

---

**Tools/sources used:**

AWS documentation, PM2 docs, Nginx docs, Next.js docs, course notes, curl, pm2 logs, nginx -t, browser DevTools.

---

# LinkedIn Post (Required)

## Goal

Publish a LinkedIn post sharing the capstone deployment, including the public ALB DNS (or a redacted screenshot), three to five lines on what you built and why it is production-style, and one proof screenshot.

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`https://lnkd.in/p/dzwZdvTs`

---

#### Screenshot of LinkedIn post

![Screenshot of LinkedIn post](./screenshots/AS06-Linkedin.png)

---

# Submission Instructions

- Add all required screenshots and links in your submission
- Do not expose passwords, RDS credentials, connection strings, private keys, or account IDs

---

# Completion Checklist

- [ ] Task 1: Architecture diagram completed
- [ ] Task 2: AWS Region and services documented
- [ ] Task 3: Public ALB DNS confirmed working
- [ ] Task 4: All six evidence screenshots captured (Web Tier, App Tier, both ALBs, RDS + replica, app UI)
- [ ] Task 5: Deployment summary completed (what worked, issues/fixes, tools/sources)
- [ ] LinkedIn post published and URL submitted
- [ ] App Tier and Database Tier confirmed not publicly accessible
- [ ] No sensitive data exposed

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 University: https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 Discord Community: https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 Blog: https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) — Agentic AI Track.*