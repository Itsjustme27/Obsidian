
| Description:   | EventID: 214            |
| -------------- | ----------------------- |
| Incident Type: | Exchange                |
| Created Date:  | Sep, 23, 2025, 04:04 PM |


# Incident Report – Quishing Alert (QR Code Phishing)

## 1. Incident Summary
- **Date/Time (UTC):** Sep 23, 2025, 04:04 PM  
- **Alert Type:** SOC251 – Quishing Detected (QR Code Phishing)  
- **Severity:** Medium  
- **Host:** Claire  
- **OS:** Windows 10  
- **User Account:** claire@letsdefend.io  

---

## 2. Description of Event
At 04:04 PM UTC, the user **Claire@letsdefend.io** received a suspicious email from:

- **From:** security@microsecmfa.com  
- **To:** claire@letsdefend.io  
- **Subject:** New Year's Mandatory Security Update: Implementing Multi-Factor Authentication (MFA)  
- **Date:** Jan 01, 2024, 12:00 PM  
- **Action:** Allowed  

The email contained a **QR code**, which is identified as a malicious Quishing attempt. The user **did not interact** with the email.

---

## 3. Technical Evidence
- **SPF/DKIM/DMARC:** Pass  
- **Indicators of Compromise (IOCs):**
  - SMTP IP: `158.69.201.47` (flagged for phishing on VirusTotal)  
  - Domains: [list]  

- **System/Network Findings:**  
  - No suspicious processes observed  
  - No malicious URLs in browser history  
  - No unusual network connections detected  

---

## 4. Analysis
- **MITRE ATT&CK Mapping:**  
  - **T1660 – Quishing**: Adversaries deliver malicious QR codes to redirect users to phishing websites.  

- **Risk Assessment:**  
  - This alert is a **True Positive**, as the email was indeed malicious.  
  - **No compromise occurred**, as the user did not engage with the email and no IOCs were observed on the host or network.  

---

## 5. Immediate Actions Taken
- The email was **quarantined** for further analysis.  
- User was reminded not to interact with suspicious emails.  

---

## 6. Escalation Note
> Medium severity alert requires L2/L3 awareness.  
> No system compromise detected, but continue monitoring similar IOCs to prevent potential future incidents.

---

## 7. Incident Classification
- **Alert:** True Positive ✅  
- **Impact:** None – no compromise observed  
- **Status:** Contained / Prevented  
