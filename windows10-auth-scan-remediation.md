# 🖥️ Windows 10 Authenticated Vulnerability Scan & Remediation

## Overview
This lab demonstrates how to conduct an **Authenticated Vulnerability Scan** on a Windows 10 VM using Tenable.io.  
It covers: provisioning, introducing vulnerabilities, scanning, remediating, and validating fixes.  
The exercise highlights the **full vulnerability lifecycle** used in SOC and vulnerability management operations.  

---

## Steps

### 1. Provision Windows 10 VM 
- Create a Windows 10 Pro (Gen2) VM in Azure.  
- Use a **strong username/password** (do not use `labuser/Cyberlab123!`).  
- Disable Windows Firewall (`wf.msc`).  

Enable remote administrative access with this PowerShell command (run **as Administrator**):  

```powershell
Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" -Name "LocalAccountTokenFilterPolicy" -Value 1 -Type DWord -Force
2. Configure & Run Initial Authenticated Scan
In Tenable.io, create a scan based on Windows 10 DISA/STIG User Defined Template.

Scanner Type: Internal Scanner (or Cloud Scanner with public IP if required).

Enter VM credentials for authentication.

Launch the scan and export results.

📸 Screenshot:

win10-auth-before.png → Scan summary before remediation.

3. Introduce Vulnerabilities
Manually add common vulnerabilities to simulate a real environment:

Missing updates → Leave VM unpatched “out of the box.”

Enable SMBv1 → Legacy insecure protocol.

Install insecure software → Example: Firefox (older version).

Restart the VM.

📸 Optional Screenshots:

win10-vuln-added.png → SMBv1 enabled or insecure software installed.

4. Re-run Authenticated Scan
Run another scan in Tenable.io.

Observe new vulnerabilities detected.

📸 Screenshot:

win10-scan-after-vuln.png → Scan results after introducing vulnerabilities.

5. Remediation
Apply all pending Windows Updates.

Disable SMBv1.

Disable Internet Explorer.

Uninstall insecure software (appwiz.cpl).

Restart VM.

📸 Screenshot:

win10-remediation.png → Proof of updates installed or SMBv1 disabled.

6. Validate with Rescan
Launch another authenticated scan.

Compare results before and after remediation.

📸 Screenshot:

win10-auth-after.png → Scan summary showing reduced vulnerabilities.

📊 Vulnerability Comparison
Stage	Critical	High	Medium	Low
Before Remediation	?	?	?	?
After Introducing Vulns	?	?	?	?
After Remediation	?	?	?	?

(Fill in actual numbers from your Tenable scan reports.)

Screenshots
🔎 Before Remediation

⚠️ Vulnerabilities Introduced

🛠️ Remediation

✅ After Remediation

Key Takeaways
Authenticated scans provide deep system visibility compared to unauthenticated scans.

Introducing vulnerabilities helps simulate real-world attack surfaces.

The remediation cycle = Detect → Analyze → Fix → Validate.

This workflow mirrors what SOC analysts and vulnerability management teams do daily.
