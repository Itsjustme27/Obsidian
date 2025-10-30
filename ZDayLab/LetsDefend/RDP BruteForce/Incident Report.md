
# Incident Report – RDP Brute Force Attack

## 1. Incident Summary
- **Date/Time (UTC):** 2024-03-07 23:44  
- **Alert Type:** Brute Force Attack (RDP)  
- **Severity:** Medium  
- **Host:** Matthew (172.16.17.148)  
- **OS:** Windows  
- **User Account:** Matthew  

---

## 2. Description of Event
At 2024-03-07 23:44 UTC, multiple failed RDP login attempts were detected on host `Matthew (172.16.17.148)` from external IP `218.92.0.56` targeting port 3389. The frequency of login attempts suggests a brute force attack pattern.

---

## 3. Technical Evidence
- Multiple failed login attempts in under one minute (Windows Security Event ID **4625**).  
- No successful login (Event ID **4624**) was observed.  
- Source IP `218.92.0.56` flagged as malicious by **8/95 vendors** in VirusTotal.  
- Target service: **Remote Desktop Protocol (RDP) – Port 3389**.

---

## 4. Risk Justification
The event matches brute force activity due to high-frequency login attempts on RDP (port 3389). External IP `218.92.0.56` is confirmed as malicious in VirusTotal. This validates the event as a **True Positive RDP brute force attack attempt**.

---

## 5. Scope Determination
- Attack attempts were limited to **host Matthew (172.16.17.148)**.  
- No evidence of attempts against other hosts or accounts within the same timeframe.  
- Current scope is **restricted to a single host and user account**.

---

## 6. Immediate Actions Taken
- Quarantined host `Matthew (172.16.17.148)` from the network.  
- Blocked malicious IP `218.92.0.56` at firewall/EDR.  
- Isolated host pending forensic review.  

---

## 7. Escalation Note
This alert is classified as **Medium severity** and requires **L2/L3 investigation** to confirm whether brute force attempts led to unauthorized access or privilege escalation.  

**Recommended next steps:**  
- Review Windows Security Event Logs (IDs 4624, 4625).  
- Investigate persistence mechanisms (scheduled tasks, services, registry).  
- Perform memory and disk forensic analysis.  
- Monitor for further activity from related IP ranges.
