# 🟩 Project 2: Configuring & Securing a Linux Server (Ubuntu)
---

 📄 **Full Lab Report:**  
👉 [Click here to open the complete lab report](https://github.com/Pelumi-Johnson/Don-associates-cloud-migration/blob/main/Executive%20Summary%20Template%20(4)%20(1).docx.pdf)

### 🛡️ Secure Linux Server Build (Apache • SSH Hardening • UFW • Fail2ban)
Hands-on project where I configured an Ubuntu Linux server to host a web page, enabled secure remote administration, locked down network access with firewall rules, and implemented automated intrusion prevention through log monitoring.

---

## ✅ What I Built
This project focused on turning a fresh Ubuntu VM into a **working, secured server** by setting up:
- 🌐 A live web server (Apache) serving a custom page  
- 🔐 SSH remote access with stronger authentication practices  
- 🧱 Firewall rules (UFW) allowing only required traffic  
- 👁️ Log monitoring + automated bans (Fail2ban) for brute-force defense  

---

## 🧰 Lab Environment
- 🐧 OS: Ubuntu Linux (Virtual Machine)
- 🖥️ Platform: VirtualBox (NAT networking used)
- 🌐 Web Server: Apache2
- 🔑 Remote Access: OpenSSH Server (host → VM via port forwarding)
- 🧱 Firewall: UFW
- 🚫 Intrusion Prevention: Fail2ban

---

## 🌐 Step 1: — Install & Configure Apache Web Server
### ✅ Steps Completed
- Updated packages:
  - `sudo apt update`
  - `sudo apt upgrade -y`
- Installed Apache:
  - `sudo apt install apache2 -y`
- Verified it was running:
  - `sudo systemctl status apache2`
- Identified VM IP:
  - `ip a`
- Confirmed Apache default page loaded in browser
- Built a custom homepage:
  - Edited `/var/www/html/index.html`
  - Restarted Apache and confirmed the custom page loads

📌 Notes I captured:
- `lo` = loopback interface (system talks to itself)
- `enp0s3` = active network interface
- VM IPv4 used for testing: `10.0.2.15`

---

## 🔐 Step 2: Set Up & Secure SSH Access
### ✅ Steps Completed
- Installed OpenSSH Server:
  - `sudo apt install openssh-server`
- Verified SSH service:
  - `sudo systemctl status ssh`
- Configured VirtualBox NAT Port Forwarding:
  - Host port **2222** → VM port **22**
- Connected from Windows PowerShell:
  - `ssh <username>@localhost -p 2222`
- Enabled key-based authentication:
  - `ssh-keygen`
  - `ssh-copy-id`
- Disabled password authentication in:
  - `/etc/ssh/sshd_config`
- Restarted SSH service after changes

---

## 🧱 Step 3: Configure Firewall (UFW)
### ✅ Rules Implemented
I configured UFW to allow only the essential ports:
- 🔐 SSH (22) — secure remote admin
- 🌐 HTTP (80) — web traffic
- 🔒 HTTPS (443) — encrypted web traffic (TLS/SSL)

Then I verified firewall rules using:
- `sudo ufw status`

---

## 👁️ Step 4: Log Monitoring + Fail2ban Defense
### ✅ What Fail2ban Did
Fail2ban watched authentication logs for repeated failed logins and automatically banned suspicious IPs (especially SSH brute-force behavior).

### ✅ Steps Completed
- Installed Fail2ban:
  - `sudo apt install fail2ban`
- Verified it was active:
  - `sudo systemctl status fail2ban`
- Confirmed SSH protection was running:
  - `fail2ban-client status`
  - Checked the `sshd` jail

---

## 🧠 Reflection: Challenges & Lessons Learned
### ⚠️ Challenges Encountered
- SSH timing out due to NAT networking → fixed via **port forwarding (2222 → 22)**
- “Permission denied” errors → caused by incorrect username (learned to verify with `whoami` and `/home`)
- Unsure if Fail2ban was working → confirmed with `fail2ban-client status` and jail output


### ✅ Lessons Learned
- `/var` (“variable”) contains changing system data like logs (`/var/log`) — critical for security monitoring
- How **UFW + SSH hardening + Fail2ban** work together as layered defense
- Stronger confidence troubleshooting services, networking, and Linux server administration


---

## 🧾 Evidence Checklist
- ✅ Apache running + custom page displayed
- ✅ SSH working through host port forwarding
- ✅ Firewall rules restricted to 22/80/443
- ✅ Fail2ban active and monitoring SSH logs

---

