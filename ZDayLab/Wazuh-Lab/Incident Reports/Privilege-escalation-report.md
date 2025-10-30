**1. Incident Summary**

- **Date/Time (UTC)**: 2025-09-10 07:10
    
- **Alert Type**: Privilege Escalation
    
- **Severity**: Medium
    
- **Host**: ubuntu-server
    
- **OS**: Ubuntu 24.10 (Oracular Oriole)
    
- **User Account**: attacker
    

---

**2. Description of Event**

> At 2025-09-10 07:10 UTC, the host **ubuntu-server** running **Ubuntu 24.10** executed the following suspicious activity:  
> **Commands / Actions**:
> 
> - `/usr/bin/bash -c 'echo "thanks" > /tmp/testfile'`
>     
> - `/usr/bin/bash -c 'echo "thanks" > /etc/passwd'`  
>     **Attachment / File**: No attachments  
>     **URLs (if any)**: None
>     
> 
> Source process chain: `sudo → bash`

---

**3. Technical Evidence**

- **SPF/DKIM/DMARC**: N/A (not email-related)
    
- **Malware Scan Results**: N/A
    
- **Indicators of Compromise (IOCs)**:
    
    - **IP Addresses**: 192.168.1.6
        
    - **Domains**: None
        

---

**4. Analysis**

- **TTPs (MITRE ATT&CK Mapping)**:
    
    - [T1078] Valid Accounts — User ‘attacker’ attempting unauthorized privilege escalation.
        
    - [T1548.002] Abuse Elevation Control Mechanism: Sudo — Attempts to use sudo without authorization.
        
- **Risk Justification**:
    
    - This is a **True Positive** alert indicating an unauthorized privilege escalation attempt. If successful, it could allow attackers full root control, risking system integrity and confidentiality.
        

---

**5. Immediate Actions Taken**

- Confirmed user ‘attacker’ is NOT in sudoers, blocking privilege escalation.
    
- Monitored and logged the unauthorized attempts via Wazuh alerting.
    
- Maintained system integrity with no successful privilege escalation.
    

---

**6. Escalation Note**

> This alert is **Medium** and requires L2/L3 investigation due to detected privilege escalation attempts by an unauthorized user.  
> Recommend immediate containment, review of user privileges, and forensic review of system access logs.

---

**7. Appendices (Optional)**

- Wazuh alert log snapshots for rule ID 5405 (Unauthorized user attempted to use sudo).
    
- Full command execution logs from `/var/log/journald`.