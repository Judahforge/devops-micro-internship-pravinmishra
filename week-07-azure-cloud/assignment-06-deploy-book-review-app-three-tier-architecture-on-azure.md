# Assignment 6 — Capstone: Deploy Book Review App (Three-Tier Architecture) on Azure

Part of the DevOps Micro Internship (DMI) with Agentic AI

---

## Purpose

This is the most important assignment of the course. You will deploy the Book Review App in a production-ready, best-practice-compliant three-tier architecture on Azure: separated presentation, application, and database tiers, least-privilege network access, a controlled public entry point, protected secrets, and availability/monitoring evidence.

---

# Task 1 — Design the Azure Three-Tier Architecture

## Goal

Create an architecture diagram and implementation plan identifying the presentation, application, and database components, the chosen Azure services, the public entry point, and the internal traffic paths.

### Evidence

#### Screenshot 1 — Architecture diagram showing the public entry point, three tiers, network boundaries, and traffic flow

![Architecture diagram showing the public entry point, three tiers, network boundaries, and traffic flow](./screenshots/AS06-Architechture-diagram.png)

---

#### Screenshot 2 — Written architecture assumptions and selected Azure services

![Written architecture assumptions and selected Azure services](./screenshots/AS06-Architechture-assumption.png)

---

# Task 2 — Create the Azure Network Foundation

## Goal

Create a dedicated Resource Group and VNet with separate subnets for the web, application, and database tiers, keeping the application and database tiers without direct public access.

### Evidence

#### Screenshot 3 — Resource Group overview showing the assignment resources

![Resource Group overview showing the assignment resources](./screenshots/AS06-RG.png)

---

#### Screenshot 4 — VNet overview showing the address space and all required subnets

![VNet overview showing the address space and all required subnets](./screenshots/AS06-Book-Review-VNet.png)

---

#### Screenshot 5 — Route-table or Private DNS evidence where applicable

![Route-table or Private DNS evidence where applicable](./screenshots/AS06-Route-table.png)

---

# Task 3 — Configure Security and Secret Management

## Goal

Apply least-privilege NSG rules so traffic flows Internet → public entry point → web tier → application tier → database tier, and store credentials in Azure Key Vault or another approved secure mechanism.

### Evidence

#### Screenshot 6 — NSG rules proving least-privilege access between the tiers

![NSG rules proving least-privilege access between the tiers](./screenshots/AS06-DB-Rule.png)
![NSG rules proving least-privilege access between the tiers](./screenshots/AS06-APP-rule.png)
![NSG rules proving least-privilege access between the tiers](./screenshots/AS06-Web-rule.png)

---

#### Screenshot 7 — Key Vault or approved secret-management configuration (without displaying secret values)

![Key Vault or approved secret-management configuration (without displaying secret values)](./screenshots/AS06-KeyVault-Secrets.png)

---

# Task 4 — Deploy the Presentation (Web) Tier

## Goal

Deploy the Book Review App presentation layer on the approved web-tier compute service, configured to route requests to the internal application-tier endpoint, and not directly exposed except through the public entry service.

### Evidence

#### Screenshot 8 — Web-tier compute overview showing subnet and availability configuration

![Web-tier compute overview showing subnet and availability configuration](./screenshots/AS06-Web-tier-overview.png)

---

#### Screenshot 9 — Terminal or service output proving the presentation layer is running

![Terminal or service output proving the presentation layer is running](./screenshots/AS06-PresentationLayer-Running.png)

---

# Task 5 — Deploy the Business (Application) Tier

## Goal

Deploy the Book Review App backend privately in the application subnet, configured to use the private database endpoint and secured environment values, reachable only through its internal endpoint.

### Evidence

#### Screenshot 10 — Application-tier compute overview showing private subnet placement

![Application-tier compute overview showing private subnet placement](./screenshots/AS06-App-vm.png)

---

#### Screenshot 11 — Backend process, service, or listening-port evidence

![Backend process, service, or listening-port evidence](./screenshots/AS06-listening-port-evidence.png)

---

#### Screenshot 12 — Internal health-check or API response (without exposing secrets)

![Internal health-check or API response (without exposing secrets)](./screenshots/AS06-API-response.png)

---

# Task 6 — Deploy the Managed Database Tier

## Goal

Create a private Azure managed database (public access disabled), with availability/backup/retention settings, the Book Review App schema imported, and access restricted to the application tier only.

### Evidence

#### Screenshot 13 — Database overview showing private connectivity and public access disabled

![Database overview showing private connectivity and public access disabled](./screenshots/AS06-MYSQL-Overview.png)

---

#### Screenshot 14 — Availability, backup, and retention configuration

![Availability, backup, and retention configuration](./screenshots/AS06-High-Availability.png)
![Availability, backup, and retention configuration](./screenshots/AS06-Backup.png)

---

#### Screenshot 15 — Successful schema or connectivity verification (without exposing credentials)

![Successful schema or connectivity verification (without exposing credentials)](./screenshots/AS06-Successful-Schema.png)

---

# Task 7 — Configure Traffic Management, Availability, and Monitoring

## Goal

Configure the approved public entry service with health probes and backend pools, internal routing for the application tier where required, and enable Azure Monitor/diagnostics/logs/alerts for the key resources.

### Evidence

#### Screenshot 16 — Public entry service showing listener, frontend endpoint, and healthy web targets

![Public entry service showing listener, frontend endpoint, and healthy web targets](./screenshots/AS06-Internal-LB.png)

---

#### Screenshot 17 — Internal application-tier load-balancing or routing configuration where applicable

![Internal application-tier load-balancing or routing configuration where applicable](./screenshots/AS06-LB-rule.png)

---

#### Screenshot 18 — Azure Monitor, diagnostic settings, logs, metrics, or alert evidence

![Azure Monitor, diagnostic settings, logs, metrics, or alert evidence](./screenshots/AS06-AzureMonitor-Diagnostics.png)

---

# Task 8 — Validate the Production-Style Deployment

## Goal

Confirm the Book Review App works end to end through the public endpoint, with at least one database read and one write, confirm private tiers are not internet-reachable, and complete a safe availability test.

### Evidence

#### Screenshot 19 — Browser showing the Book Review App through the public endpoint

![Browser showing the Book Review App through the public endpoint](./screenshots/AS06-PublicEndpoint-App.png)

---

#### Screenshot 20 — Proof of successful database-backed read and write operations

![Proof of successful database-backed read and write operations](./screenshots/AS06-DB-Write-Proof.png)

---

#### Screenshot 21 — Evidence that private tiers are not publicly accessible

![Evidence that private tiers are not publicly accessible](./screenshots/AS06-Private-Tier-Notpublic.png)
![Evidence that private tiers are not publicly accessible](./screenshots/AS06-Private-Tier-Notpublic1.png)
![Evidence that private tiers are not publicly accessible](./screenshots/AS06-Private-Tier-Notpublic2.png)

---

#### Screenshot 22 — Availability-test and healthy-target evidence

![Availability-test and healthy-target evidence](./screenshots/AS06-LB-Healthy-Targets.png)
![Availability-test and healthy-target evidence](./screenshots/AS06-LB-Healthy-Targetsb.png)

---

#### Public Endpoint

Paste your public endpoint URL here:

`http://40.125.109.57`

---

### Notes

Summarize what worked, issues encountered and how they were fixed, and the availability/security/secrets/monitoring/backup choices made.

What worked end-to-end. The Book Review App was deployed as a three-tier architecture on Azure: a Public Load Balancer as the sole internet entry point, a Web VM running Next.js under PM2 behind Nginx (reverse proxy), an Internal Load Balancer forwarding /api/* traffic to an App VM running the Express backend under PM2, and a private Azure Database for MySQL Flexible Server (VNet-integrated, no public access). The full chain — browser → Public LB → Nginx → Next.js → Nginx /api/ proxy → Internal LB → Express → MySQL — was verified with curl at each hop and confirmed in the browser with real data from the book_review_db database (books list rendering, user registration persisting to the users table).

Issues encountered and fixes.

Region/SKU availability on Free Trial. Standard_B1s was unavailable in West Central US (NotAvailableForSubscription), and MySQL Flexible Server could not be provisioned in that region. Fixed by rebuilding in a region where MySQL creation validated (West US 2), using Standard_B2ats_v2 as the B-series v2 equivalent.

NAT Gateway SKU mismatch. A StandardV2 NAT Gateway rejected a Standard-SKU public IP. Fixed by creating a matching StandardV2 public IP for the NAT Gateway.

Frontend architecture mismatch. The repo's frontend is a Next.js App Router application, not a React CRA app — there is no build/ directory. The initial Nginx static-serve config returned 403 Forbidden because /var/www/book-review was empty. Fixed by running Next.js under PM2 (next start on port 3000) and reconfiguring Nginx as a reverse proxy (proxy_pass http://localhost:3000).

Browser unable to reach private endpoints. Setting NEXT_PUBLIC_API_URL=http://10.0.2.100:5000 caused fetches to fail because the browser cannot route to a private IP. Fixed architecturally: the frontend now calls a relative /api/* path, and Nginx proxies /api/ to the Internal LB. This removes CORS preflight and keeps private endpoints truly private.

Double slash in API URL. NEXT_PUBLIC_API_URL with a trailing slash produced //api/books, bypassing Nginx's location /api/ block and hitting Next.js's 404. Fixed by removing the trailing slash and rebuilding (Next.js NEXT_PUBLIC_* values are baked at build time).

Missing /api prefix in services/api.js. Registration and login POSTed to /users/register and /users/login instead of /api/users/register. Fixed by changing API_URL to append /api, making all six service functions consistent with the backend's mount paths.

PM2 port/name collisions. The backend briefly crash-looped with EADDRINUSE :::3001 and duplicate PM2 process names (frontend vs book-review-frontend) caused further confusion. Fixed by standardising on one process per tier, using an ecosystem.config.js with an explicit PORT, and registering PM2 with systemd (pm2 startup + pm2 save) so both VMs survive reboots.

MySQL hostname typo. A doubled .mysql.database.azure.com suffix caused ERROR 2005. Fixed by copying the hostname directly from the MySQL Overview page.

"Unknown database 'book_review_db'." The database had not been created on the Azure MySQL server. Fixed by connecting without a database argument and running CREATE DATABASE book_review_db;, after which Sequelize sync() created the schema and PM2 started cleanly.

Availability choices. MySQL Flexible Server is configured with High Availability enabled and automated backups with a 7-day retention window (configurable 1–35 days). Both load balancers use health probes (TCP:80 on the Public LB, TCP:5000 on the Internal LB) with backend pools showing Healthy targets. Application processes are supervised by PM2 with systemd startup registration, so both the frontend and backend recover automatically after a VM reboot. The two-VM-per-LB backend pool design allows additional VMs to be added horizontally without reconfiguring the load balancers.

Security choices. The App VM and MySQL server have no public IP addresses — only the Public Load Balancer's frontend is internet-facing. Network Security Groups restrict traffic per subnet: web-nsg allows HTTP (80) from the internet and SSH (22) only from the admin IP; app-nsg allows port 5000 only from the Web subnet (10.0.1.0/24) and SSH from the admin IP; db-nsg allows MySQL (3306) only from the App subnet. The MySQL server uses Private access (VNet Integration) with public network access Disabled, and connections from the backend enforce SSL (require: true).

Secrets management. Secrets are stored in Azure Key Vault (DB-HOST, DB-USER, DB-PASS, DB-NAME) rather than being hardcoded or committed to source. The App VM's system-assigned managed identity is granted the Key Vault Secrets User role (least privilege — read-only), following the Azure RBAC permission model. Database credentials are also present in the App VM's .env/ecosystem config for runtime, chmod 600, and excluded from all screenshots.

Monitoring and backup. Diagnostic settings on the load balancers and key resources stream logs and metrics to a Log Analytics workspace, providing a single pane for audit and troubleshooting. Azure Monitor metrics are used to observe Health Probe Status for both load balancers and VM CPU/memory. MySQL's automated backups with 7-day retention (and optional geo-redundant backup) satisfy the recovery point objective; the backup blade in the portal shows the latest restore point timestamp.

Public endpoint. http://40.125.109.57 — verified to load the Book Review App via the Public Load Balancer, with the book list rendering from book_review_db, and user registration performing a successful INSERT visible via SELECT on the App VM.

---

# Submission Instructions

- Add all required screenshots and links in your submission
- Do not expose passwords, keys, connection strings, or subscription IDs

---

# Completion Checklist

- [ ] Task 1: Architecture diagram and assumptions documented (Screenshots 1–2)
- [ ] Task 2: Network foundation created with isolated tiers (Screenshots 3–5)
- [ ] Task 3: Least-privilege security and secret management configured (Screenshots 6–7)
- [ ] Task 4: Presentation tier deployed (Screenshots 8–9)
- [ ] Task 5: Application tier deployed privately (Screenshots 10–12)
- [ ] Task 6: Managed database tier deployed privately (Screenshots 13–15)
- [ ] Task 7: Public entry, internal routing, and monitoring configured (Screenshots 16–18)
- [ ] Task 8: End-to-end validation and availability test completed (Screenshots 19–22, Public Endpoint, Notes)
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
