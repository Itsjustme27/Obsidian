```shell

└─$ nmap -sT --top-ports 100 -T2 -oA mushroomnepal_basic mushroomnepal.com

Starting Nmap 7.95 ( https://nmap.org ) at 2025-10-15 09:43 EDT
Stats: 0:00:31 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 31.00% done; ETC: 09:45 (0:01:09 remaining)
Nmap scan report for mushroomnepal.com (216.198.79.1)
Host is up (0.067s latency).
Not shown: 98 filtered tcp ports (no-response)
PORT    STATE SERVICE
80/tcp  open  http
443/tcp open  https

Nmap done: 1 IP address (1 host up) scanned in 92.63 seconds

```
