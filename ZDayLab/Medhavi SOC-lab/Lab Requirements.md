
## SOC (Security Operation Center) Lab Hardware List (Priority-Based)

## Compulsory Hardware (Must-Have)
| Device                    | Qty   | Specs / Purpose                                                             |
| ------------------------- | ----- | --------------------------------------------------------------------------- |
| Ubuntu Server (Blue Team) | 1     | 16–32 GB RAM, 4–8 CPU cores, 1 TB SSD → Wazuh Manager + Indexer + Dashboard |
| Red Team / Attack VM Host | 1     | 16 GB RAM, 4 cores, 500 GB SSD → Kali Linux + Metasploitable / DVWA         |
| Workstation               | 1     | 8–16 GB RAM, 4 cores, 250 GB SSD → Monitor dashboards, run attacks, scripts |
| Managed Switch            | 1     | 8–16 ports, supports VLANs for Blue/Red separation                          |
| Cat6 or Cat5 Cables       | 10–15 | Connect servers & workstation                                               |
| UPS                       | 1     | 1–2 kVA for power backup                                                    |
| Monitor / Projector       | 1     | Dashboard visualization                                                     |

> These items are **essential** to get a fully functional solo SOC lab running.

---

## Optional Hardware (Nice-to-Have / Future Expansion)
| Device                     | Qty | Notes                                                         |
|----------------------------|-----|---------------------------------------------------------------|
| Router / Firewall          | 1   | For isolated network or controlled Internet access           |
| Wi-Fi AP                   | 1   | Optional, for wireless traffic exercises                     |
| External Storage           | 1   | Backup VM snapshots & logs                                    |
| IDS Server                 | 1   | Zeek / Suricata dedicated server for larger-scale monitoring |
| Rack                       | 1   | Organize servers if space allows                              |
| Network Tap / SPAN Port    | 1   | Advanced network traffic capture                               |
| Whiteboard / Digital Dashboard | 1 | Track lab exercises, incidents, and workflows               |

> Optional items are for **lab enhancement or scaling**. Start with the compulsory hardware, then add these later.
