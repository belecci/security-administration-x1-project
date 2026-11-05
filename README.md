# security-administration-x1-project
# 🛡️ Secure Cloud Infrastructure & Web Application Deployment

## 📋 Project Overview
This project focuses on the design, deployment, and security hardening of a cloud-based infrastructure hosted on Microsoft Azure. It implements robust Security Administration principles—focusing on network segmentation, access control rules, encryption, system hardening, monitoring, and automated backup strategies.

---

## 🏗️ Architecture & Network Security
* **Network Segmentation:** Built an Azure Virtual Network (VNet) separated into isolated subnets for the compute tier (`vm-subnet`, `192.168.1.0/24`) and database tier (`database-subnet`, `192.168.2.0/24`).
* **Database Isolation:** Completely blocked public internet access to the Azure SQL Database, routing internal traffic strictly via a secure Private Endpoint.
* **Network Security Groups (NSGs) & Firewall:** Implemented stateful traffic filtering allowing only trusted administrative SSH/Testing traffic, public HTTP/80 & HTTPS/443, and dropping all other unsolicited traffic. Augmented with UFW (Uncomplicated Firewall) at the OS level.
* **DDoS & Web Application Firewall (WAF):** Enabled Azure DDoS Protection and deployed an Azure WAF policy running OWASP Top-10 rule sets to inspect Layer 7 traffic and mitigate automated bot threats.

---

## 🔒 Identity, Access Management & System Hardening
* **Azure RBAC:** Created custom roles (Developers, Project Managers, QA Testers) adhering strictly to the Principle of Least Privilege (PoLP) to restrict cloud management permissions.
* **Linux Hardening:** Disabled root login and password authentication on Ubuntu, enforcing secure SSH public-key pairs.
* **PAM Security:** Configured Pluggable Authentication Modules (`/etc/pam.d/common-password`) to enforce robust password complexity standards and `yescrypt` hashing.
* **Brute-Force Mitigation:** Deployed Fail2ban to automatically monitor authentication logs and temporarily ban IPs after repeated failed login attempts.

---

## 🔐 Data Protection & Encryption
* **Data in Transit:** Enforced TLS 1.2+ across SQL connections and configured Nginx with self-signed SSL/TLS certificates to secure user web traffic.
* **Data at Rest:** Enabled Transparent Data Encryption (TDE) on the Azure SQL database and AES-256 storage encryption on Azure Blob Storage.
* **Secrets Management:** Provisioned an Azure Key Vault featuring Soft-Delete (90-day retention) and Purge Protection.

---

## 📊 Logging, Monitoring & Backup Automation
* **Centralized Logging:** Configured rsyslog paired with custom `logrotate` policies to safely manage system and application log lifecycles.
* **Automated Patching:** Configured `unattended-upgrades` on Ubuntu for automated, timely security patch deployment.
* **Disaster Recovery & Scripting:** 
  * Scheduled automated daily backups via Linux `cron` jobs.
  * Developed a custom Bash backup-verification script that autonomously checks backup file integrity, size, and recency within a 24-hour window, appending results to a secure log file.

---

## 🚀 How to View Assets & Documentation
* **Architecture Diagram:** View the visual topology map in `AWS Diagram.png`.
* **Full Reports:** Read the detailed academic and technical breakdown in `Secuirty Administration Project.pdf`.

---

## 🛠️ Tech Stack & Tools
* **Cloud Provider:** Microsoft Azure (Azure VMs, Azure SQL, Blob Storage, VNet, WAF, Key Vault)
* **OS & Web Server:** Ubuntu Server 22.04 LTS, Nginx
* **Security Tooling:** Fail2ban, UFW, OpenSSL, Azure RBAC
* **Scripting & Automation:** Bash, Cron
