
**1. Incident Summary**

- **Date/Time (UTC)**: [YYYY-MM-DD HH:MM]
    
- **Alert Type**: [Phishing / Malware / Recon / Privilege Escalation / Lateral Movement]
    
- **Severity**: [Low / Medium / High / Critical]
    
- **Host**: [Hostname]
    
- **OS**: [Operating System & Version]
    
- **User Account**: [User involved or SYSTEM]
    

---

**2. Description of Event**

> At [Time UTC], the host **[hostname]** running **[OS]** executed the following suspicious activity:  
> **Commands / Actions**: `[list commands or observed activity]`  
> **Attachment / File**: `[filename]`  
> **URLs (if any)**: `[list]`
> 
> Source process chain: `[Grandparent → Parent → Child process]`

---

**3. Technical Evidence**

- **SPF/DKIM/DMARC**: [Pass/Fail] (for email incidents)
    
- **Malware Scan Results**: [VT/Malware sandbox results, hash]
    
- **Indicators of Compromise (IOCs)**:
    
    - **File Hash**: SHA256/MD5
        
    - **IP Addresses**: [list]
        
    - **Domains**: [list]
        

---

**4. Analysis**

- **TTPs (MITRE ATT&CK Mapping)**:
    
    - [T####] Technique Name — Description
        
    - [T####] Technique Name — Description
        
- **Risk Justification**:
    
    - Why this is a **True Positive** and potential impact if not contained.
        

---

**5. Immediate Actions Taken**

- Quarantined email/file
- Isolated host
- Blocked IP/domain in firewall/EDR

---

**6. Escalation Note**

> This alert is **[Severity]** and requires L2/L3 investigation due to [reason: confirmed malware, C2 traffic, AD enumeration, privilege escalation, etc.].  
> Recommend immediate containment and forensic review.

---

**7. Appendices (Optional)**

- Screenshots of alert
    
- Email header dump
    
- VirusTotal / Hybrid Analysis links
    
- Process tree diagram
    

---

💡 **Tips for Fast Use**

- Keep a **pre-filled MITRE ATT&CK cheat sheet** handy so you can copy/paste TTP codes.
    
- Save a “common IOCs” list so you don’t retype domains/IPs every time.
    
- If you have repeat phishing or malware alerts, create **short canned L1 notes** to drop in quickly.
    

---