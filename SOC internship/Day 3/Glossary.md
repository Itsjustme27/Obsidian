
# Firewall

- **NGFW**: Next Generation Firewall 


- **NGFW vs Traditional Firewall:**

| NGFW (Next Generation Firewall)                                                         | Traditional Firewall                                                                                                           |
| --------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| Deep packet inspection, malware detection and intrusion prevention.                     | Packet filtering based on IP, port, and protocol                                                                               |
| Operates across layer 3 to 7                                                            | Operates at Layer 3 (Network Layer)                                                                                            |
| Advanced Threat Detection, IDS/IPS (Snort, Suricata), malware detection and sandboxing. | Basic & limited threat detection (Only known threats).                                                                         |
| Examples: Fortigate, Palo Alto, Cloudfare (Magic Firewall)                              | Examples: Packet Filtering Firewall like iptables, Proxy firewalls like Reverse Proxies, Transparent Proxies, Forward Proxies. |

- UTM : Unified Threat Management, refers to its ability to combine multiple security functions (like Firewall, IPS, Antivirus, Web Filtering, Anti-spam) into a single appliance (FortiGate device) and platform (FortiOS) for simplified, comprehensive protection.


# AD

- Several groups are created by default in a domain that can be used to grant specific privileges to users. As an example, here are some of the most important groups in a domain:


| **Security Group** | **Description**                                                                                                                                           |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Domain Admins      | Users of this group have administrative privileges over the entire domain. By default, they can administer any computer on the domain, including the DCs. |
| Server Operators   | Users in this group can administer Domain Controllers. They cannot change any administrative group memberships.                                           |
| Backup Operators   | Users in this group are allowed to access any file, ignoring their permissions. They are used to perform backups of data on computers.                    |
| Account Operators  | Users in this group can create or modify other accounts in the domain.                                                                                    |
| Domain Users       | Includes all existing user accounts in the domain.                                                                                                        |
| Domain Computers   | Includes all existing computers in the domain.                                                                                                            |
| Domain Controllers | Includes all existing DCs on the domain.                                                                                                                  |


- **KDC:** Key Distribution Center

#  Proxy:

- **Forward Proxy:** Sits in front of clients, masking their IP for internet access (e.g., for company filtering, user privacy).

- **Reverse Proxy**: Sits in front of servers, handling incoming requests, load balancing, and security for backend systems.


![[Pasted image 20251231162834.png]]



# WAF

Web Application Firewall, is a security tool that filters, monitors, and blocks malicious HTTP/S traffic to protect web applications from attacks like SQL injection, Cross-Site Scripting (XSS), and bots by acting as a shield between users and the server, operating at the application layer (Layer 7) to enforce security rules and safeguard data.


### Types of WAF:

- **Cloud-based WAF:** Hosted in the cloud, protecting cloud applications
- **Network-based WAF:** Hardware appliances placed in front of servers
- **Host-based WAF:** Installed directly on application servers.