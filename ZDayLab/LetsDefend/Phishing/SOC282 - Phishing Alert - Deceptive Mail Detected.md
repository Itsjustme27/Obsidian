
# Incident Report

## 1. Incident Summary
- **Date/Time (UTC):** September 22, 2025, 11:58 AM  
- **Alert Type:** SOC282 - Phishing Alert - Deceptive Mail Detected  
- **Severity:** Medium  
- **Host:** Felix  
- **Event ID:** 257  
- **User Account:** Felix@letsdefend.io  

---

## 2. Description of Event
At 11:58 AM, a suspicious mail containing an attachment was detected in `Felix@letsdefend.io`'s mailbox.  
The attachment was downloaded and executed immediately. Shortly after, the threat actor gained access and executed enumeration commands on the host.

---

## 3. Technical Evidence

### Email Artifacts (Phishing Delivery)
- **Source Email Address:** `free@coffeeshooop.com`  
- **Destination Email Address:** `Felix@letsdefend.io`  
- **SMTP IP Address:** `103.80.134.63`  
- **Subject:** *Free Coffee Voucher*  
- **Attachment Name:** `Unconfirmed 500670.crdownload`  
- **Attachment Hash (SHA256):** `6f33ae4bf134c49faa14517a275c039ca1818b24fc2304649869e399ab2fb389`  
- **VirusTotal Result:** 16/65 vendors flagged as malicious  

### Execution Artifacts (Endpoint)
- **Malicious File Executed:** `Coffee.exe`  
- **File Path:** `C:/Users/Felix/Downloads/Coffee.exe`  
- **Process Created:** `Coffee.exe` (unknown malicious binary)  

### Post-Exploitation Commands Observed
- `ipconfig /all`  
- `route`  
- `tasklist.exe /svc`  

### Indicators of Compromise (IoCs)
- **Suspicious Executable:** `Coffee.exe`  
- **Malicious SHA256 Hash:** `6f33ae4bf134c49faa14517a275c039ca1818b24fc2304649869e399ab2fb389`  
- **External SMTP IP:** `103.80.134.63`  
- **Malicious Sender Domain:** `coffeeshooop.com`  

---

## 4. Analysis
- **[T1566.001] Spearphishing Attachment** → Delivered via email with malicious attachment.  
- **[T1204.002] User Execution: Malicious File** → Execution of `Coffee.exe`.  
- **[T1059] Command and Scripting Interpreter** → Enumeration commands executed.  

**Risk Justification:**  
This is a **True Positive**. The email contained malicious content and urgency, and the attachment was confirmed to be malware, leading to endpoint compromise.

---

## 5. Immediate Actions Taken
- Quarantined Endpoint `Felix`.

---

## 6. Escalation Note
> This alert is **Medium** severity and requires **L2/L3 investigation** due to confirmed malware.  
> Recommend immediate containment and full forensic review.

---

## 7. Lessons Learned
- Provide phishing awareness training for employees to reduce risk of similar incidents.  
- Reinforce reporting procedures so SOC can act before execution.  
- Implement stricter email gateway policies (e.g., block executables/attachments with low reputation).  
