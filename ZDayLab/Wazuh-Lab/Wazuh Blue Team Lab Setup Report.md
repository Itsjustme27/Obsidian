## **1. Lab Objective**

- Build a functional, hands-on blue team SIEM environment to monitor, detect, and respond to security events in real time.

- Learn real SOC workflows, incident detection, troubleshooting, and endpoint log centralization.


## **2. Core Technologies & Architecture**

- **SIEM Platform:** Wazuh (Docker-based, version 4.x)
s
- **Deployment Method:** Official single-node Docker Compose stack
    
    - _Wazuh manager_ (event analysis, agent enrollment, rule engine)
        
    - _Wazuh indexer_ (OpenSearch, event storage & search)
        
    - _Wazuh dashboard_ (Web UI, visualization & correlation)
        
- **Host OS:** Kali Linux
    
- **Monitored Endpoint(s):** Ubuntu Server (VM, for agent testing)
    

## **3. Major Accomplishments**

## **A. Building and Running Wazuh in Docker**

- Pulled and launched the full Wazuh stack using Docker Compose on your host.
    
- Ensured all essential containers (manager, indexer, dashboard) are persistent and restartable.
    
- Learned that logs, configs, and history are saved using Docker named volumes—even after shutdown/restart.
    

## **B. Access & Security of the SIEM**

- Successfully accessed the Wazuh dashboard via browser, verified with local and LAN IPs.
    
- Learned about network interfaces, host IPs, and Docker bridges to ensure proper access.
    
- Configured for secure, local-only monitoring (with options for expansion).
    

## **C. Monitoring a Real Endpoint**

- Deployed a fresh Ubuntu Server VM for agent installation.
    
- Troubleshooted and fixed networking/firewall issues (including UFW rules, IPv4 connectivity, and package manager locks).
    
- Removed the unnecessary manager role from the Ubuntu Server, ensuring it acts as an agent only.
    
- Enrolled the agent using the Wazuh dashboard’s guided instructions with secure enrollment keys.
    

## **D. Validating Lab Functionality**

- Confirmed the agent was reporting—with "Active" status in the dashboard.
    
- Simulated and detected test incidents (e.g., failed SSH logins, sudo attempts).
    
- Used dashboard filters/searches (like “ssh”) to investigate security events just like a real SOC analyst.
    

## **E. Troubleshooting & Blue Team Learning**

- Dealt with common problems:
    
    - Package conflicts
        
    - dpkg/apt inconsistent states
        
    - Network timeouts and IPv6 issues
        
    - Apt/dpkg lock errors
        
- Learned Linux troubleshooting best practices (process kills, forced removals, manual config).
    

## **F. Expansion and Next Steps**

- Explored adding more types of monitored endpoints (Windows, macOS, network appliances, cloud VMs).
    
- Discussed how to securely extend monitoring to remote agents (across networks or over the internet) for even bigger/practical labs.
    

## **4. Practical Skills Gained**

- Dockerized SIEM stack setup and management
    
- System/network troubleshooting (firewalls, IPs, package management)
    
- SIEM agent deployment & enrollment
    
- Real-world event detection and validation
    
- Dashboard usage for log review/incident analysis
    
- Security monitoring principles for both hosts and networks
    

## **5. Next Level Ideas (Optional)**

- Add more diverse endpoints (Windows agents, network devices, cloud VMs)
    
- Create and test custom alert rules or integrations (email, Slack)
    
- Simulate different kinds of attacks (port scans, privilege abuse) and tune detection/alerts
    

## **Conclusion**

You have successfully:

- Built a working SIEM on your own hardware
    
- Centralized logs from real and virtual endpoints
    
- Detected and verified real security events
    
- Overcome troubleshooting hurdles—a true blue team experience!


