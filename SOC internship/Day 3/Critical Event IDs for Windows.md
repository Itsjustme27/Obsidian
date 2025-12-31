

# Authentication and Logon events

| **Event ID** | **Description**                                                                                                |
| ------------ | -------------------------------------------------------------------------------------------------------------- |
| 4624         | User successfully logged on to a computer                                                                      |
| 4625         | Failed Logon                                                                                                   |
| 4648         | User successfully logged on to a computer using explicit credentials while already logged on as different user |
| 4672         | Special Privileges Assigned (Admin Logon, Potential Priv Esc)                                                  |
| 4740         | Account Lockout (Potential Bruteforce)                                                                         |
| 4768         | A Kerberos authentication ticket (TGT) was requested                                                           |
| 4769         | A Kerberos service ticket was requested                                                                        |

# Process & System Activity

| **Event ID**   | **Description**                                                     |
| -------------- | ------------------------------------------------------------------- |
| 4688           | New Process Creation                                                |
| 4689           | Process Terminal (Correlate with 4688)                              |
| 4698/4700/4701 | Scheduled Task Creation/Enable/Disable (Attacker Persistence)       |
| 4719           | System Audit Policy Changed                                         |
| 4794           | Directory Services Restore Mode Attempt (Critical for DSRM attacks) |

# Account and Group Management

| **Event ID** | **Description**                                  |
| ------------ | ------------------------------------------------ |
| 4720         | User Account Created                             |
| 4723         | Password Change Attempt                          |
| 4726         | User account deleted                             |
| 4732/4733    | Member Added/Removed from Local Group (Priv Esc) |

# Security And Integrity


| **Event ID** | **Description**                    |
| ------------ | ---------------------------------- |
| 1102         | Audit Log Cleared (Major red flag) |
| 4616         | System time changed                |
| 1116         | Antivirus Malware Detection        |

# System Stability


| **Event ID** | **Description**  |
| ------------ | ---------------- |
| 1001         | Server crash     |
| 7001/7000    | Service Failures |



