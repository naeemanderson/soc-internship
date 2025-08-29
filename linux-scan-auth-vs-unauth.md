# 🐧 Scanning a Linux (Ubuntu) VM: Authenticated vs. Unauthenticated

## 🎯 Objective
Compare the results of scanning an Ubuntu 22 VM in Azure using Tenable with **unauthenticated** vs **authenticated** credentials. Document differences in findings, scan duration, and why authenticated scans are more effective.  

---

## 🛠️ Tools Used
- Azure (Ubuntu 22 Virtual Machine)  
- Tenable Vulnerability Management  
- SSH (Secure Shell)  

---

## ⚙️ Lab Setup
- Created Ubuntu 22 VM in Azure (with a strong password)  
- Configured NSG inbound rules → allowed all traffic for testing  
- Verified connectivity:  
  - Ping VM’s public IP  
  - SSH login to VM  

---

## 📌 Steps Taken

### 1. Unauthenticated Scan
- Logged into Tenable  
- Created Basic Network Scan  
- Scanner: **Internal Scanner (LOCAL-SCAN-ENGINE-01)**  
- Target: VM private IP (preferred) or public IP if needed  
- Discovery:  
  - [x] Ping the remote host  
  - [x] Use fast network discovery  
- Credentials: left blank  

📸 *Paste screenshot of Unauthenticated scan setup*  
📸 *Paste screenshot of Unauthenticated findings*  

- Exported results  
- Duration: X mins  

---

### 2. Authenticated Scan
- Enabled root login on the Ubuntu VM:  

```bash
sudo passwd root
sudo grep -q '^PermitRootLogin' /etc/ssh/sshd_config && \
sudo sed -i 's/^PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config || \
echo 'PermitRootLogin yes' | sudo tee -a /etc/ssh/sshd_config > /dev/null && \
sudo systemctl restart sshd

Edited same Tenable scan → added valid root credentials

Reran the scan

Exported results

Duration: Y mins

📸 Paste screenshot of Authenticated scan setup
📸 Paste screenshot of Authenticated findings

3. Cleanup

Deleted Ubuntu VM from Azure

Verified resource group cleanup

| Metric                | Unauthenticated | Authenticated  |
| --------------------- | --------------- | -------------- |
| Total Vulnerabilities | (paste number)  | (paste number) |
| Critical/High         | (paste number)  | (paste number) |
| Scan Duration         | X mins          | Y mins         |
| Visibility            | Surface only    | Full system    |
