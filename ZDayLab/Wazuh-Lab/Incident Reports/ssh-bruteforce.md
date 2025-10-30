# SSH Brute Force Detection Report

**Date/Time:** 2025-09-04 16:00

**Target Host:** ubuntu-server

**Source IP:** 192.168.1.15

**Username:** itsjustme

**Number of Attempts:** 25

**Wazuh Rule Fired:** 5710 - SSH Brute Force Attempt

**Alert Level:** 5 (Medium)

**Mitigation:**  
- Block source IP  
- Enforce strong passwords  
- Enable fail2ban or Wazuh active response


```json
{
  "_index": "wazuh-alerts-4.x-2025.09.04",
  "_id": "DomoFZkBJz1-ugdaVOG3",
  "_version": 1,
  "_score": null,
  "_source": {
    "predecoder": {
      "hostname": "ubuntu-server",
      "program_name": "sshd",
      "timestamp": "Sep 04 16:56:06"
    },
    "input": {
      "type": "log"
    },
    "agent": {
      "ip": "192.168.1.4",
      "name": "ubuntu-server",
      "id": "001"
    },
    "previous_output": "Sep 04 16:56:05 ubuntu-server sshd[113772]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=192.168.1.15  user=itsjustme\nSep 04 16:56:05 ubuntu-server sshd[113768]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=192.168.1.15  user=itsjustme\nSep 04 16:56:05 ubuntu-server sshd[113775]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=192.168.1.15  user=itsjustme\nSep 04 16:56:05 ubuntu-server sshd[113763]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=192.168.1.15  user=itsjustme\nSep 04 16:56:05 ubuntu-server sshd[113762]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=192.168.1.15  user=itsjustme\nSep 04 16:56:05 ubuntu-server sshd[113770]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=192.168.1.15  user=itsjustme\nSep 04 16:56:05 ubuntu-server sshd[113764]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=192.168.1.15  user=itsjustme",
    "data": {
      "uid": "0",
      "srcip": "192.168.1.15",
      "euid": "0",
      "dstuser": "itsjustme",
      "tty": "ssh"
    },
    "manager": {
      "name": "kali"
    },
    "rule": {
      "mail": false,
      "level": 10,
      "pci_dss": [
        "10.2.4",
        "10.2.5",
        "11.4"
      ],
      "hipaa": [
        "164.312.b"
      ],
      "tsc": [
        "CC6.1",
        "CC6.8",
        "CC7.2",
        "CC7.3"
      ],
      "description": "PAM: Multiple failed logins in a small period of time.",
      "groups": [
        "pam",
        "syslog",
        "authentication_failures"
      ],
      "nist_800_53": [
        "AU.14",
        "AC.7",
        "SI.4"
      ],
      "frequency": 8,
      "gdpr": [
        "IV_35.7.d",
        "IV_32.2"
      ],
      "firedtimes": 1,
      "id": "5551",
      "gpg13": [
        "7.8"
      ]
    },
    "location": "journald",
    "decoder": {
      "name": "pam"
    },
    "id": "1757004967.184720",
    "full_log": "Sep 04 16:56:06 ubuntu-server sshd[113786]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=192.168.1.15  user=itsjustme",
    "timestamp": "2025-09-04T12:56:07.348-0400"
  },
  "fields": {
    "timestamp": [
      "2025-09-04T16:56:07.348Z"
    ]
  },
  "highlight": {
    "data.tty": [
      "@opensearch-dashboards-highlighted-field@ssh@/opensearch-dashboards-highlighted-field@"
    ],
    "manager.name": [
      "@opensearch-dashboards-highlighted-field@kali@/opensearch-dashboards-highlighted-field@"
    ],
    "full_log": [
      "Sep 04 16:56:06 ubuntu-server sshd[113786]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=@opensearch-dashboards-highlighted-field@ssh@/opensearch-dashboards-highlighted-field@ ruser= rhost=192.168.1.15  user=itsjustme"
    ]
  },
  "sort": [
    1757004967348
  ]
}

```
