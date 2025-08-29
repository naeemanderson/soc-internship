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
- Credentials left blank  

📸 Unauthenticated scan results:  
![Linux Unauthenticated Scan Results](./images/linux-unauth-results.png)

- Exported results  
- Duration: 6 mins  

---

### 2. Authenticated Scan

- Enabled root login on Ubuntu  
- Configured Tenable scan with valid credentials  
- Reran scan  

📸 Authenticated scan results:  
![Linux Authenticated Scan Results](./images/linux-auth-results.png)

```bash
sudo passwd root
sudo grep -q '^PermitRootLogin' /etc/ssh/sshd_config && \
sudo sed -i 's/^PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config || \
echo 'PermitRootLogin yes' | sudo tee -a /etc/ssh/sshd_config > /dev/null && \
sudo systemctl restart sshd

Edited same Tenable scan → added valid root credentials

Reran the scan

📸 Authenticated scan results:  
![Linux Authenticated Scan Results](./images/linux-auth-results.png)

Exported results

Duration: 5 mins


3. Cleanup

Deleted Ubuntu VM from Azure

Verified resource group cleanup

| Metric                | Unauthenticated | Authenticated  |
| --------------------- | --------------- | -------------- |
| Total Vulnerabilities | (19)            | (59)           |
| Critical              | (0)             | (0)            |
| High                  | (0)             | (1)            |
| Scan Duration         | 6 mins          | 5 mins         |
| Visibility            | Surface only    | Full system    |


📖 Key Takeaways

Unauthenticated scans = attacker’s external perspective

Authenticated scans = deeper visibility into misconfigurations & patch levels

SOC analysts need both perspectives, but authenticated scans are essential for accurate remediation

