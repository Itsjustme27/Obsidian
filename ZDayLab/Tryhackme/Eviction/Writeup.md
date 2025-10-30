
# Eviction Room | TryHackMe

## Overview:

The Eviction Room is a beginner friendly room on TryHackMe that delves into the world of Advanced Persistent Threat (APT) groups and their tactics, techniques, and procedures. By exploring real-world scenarios and case studies, you’ve gained valuable insights into the cyber threat landscape.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:840/1*7TJFbgHLRGkw43qAZb0RjQ.png)

## APT28(G0007)

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:840/1*pj3l_gS505iy0nYtsyJPEQ.png)

## **_Answers for this room_**

**1).What is a technique used by the APT to both perform recon and gain initial access?**

Ans: Spearphishing Link

**2).Sunny identified that the APT might have moved forward from the recon phase. Which accounts might the APT compromise while developing resources?**

Ans: Email Accounts

**3).E-corp has found that the APT might have gained initial access using social engineering to make the user execute code for the threat actor. Sunny wants to identify if the APT was also successful in execution. What two techniques of user execution should Sunny look out for? (Answer format: <technique 1> and <technique 2>)**

Ans: Malicious File and Malicious Link

**4.)If the above technique was successful, which scripting interpreters should Sunny search for to identify successful execution? (Answer format: <technique 1> and <technique 2>)**

Ans: PowerShell and Windows Command Shell

**5).While looking at the scripting interpreters identified in Q4, Sunny found some obfuscated scripts that changed the registry. Assuming these changes are for maintaining persistence, which registry keys should Sunny observe to track these changes?**

Ans: Registry Run Keys

**6).Sunny identified that the APT executes system binaries to evade defences. Which system binary’s execution should Sunny scrutinize for proxy execution?**

Ans: Rundll32

**7).Sunny identified tcpdump on one of the compromised hosts. Assuming this was placed there by the threat actor, which technique might the APT be using here for discovery?**

Ans: Network Sniffing

**8).It looks like the APT achieved lateral movement by exploiting remote services. Which remote services should Sunny observe to identify APT activity traces?**

Ans: SMB/windows admin shares

**7).It looked like the primary goal of the APT was to steal intellectual property from E-corp’s information repositories. Which information repository can be the likely target of the APT?**

Ans: Sharepoint

**9).Although the APT had collected the data, it could not connect to the C2 for data exfiltration. To thwart any attempts to do that, what types of proxy might the APT use? (Answer format: <technique 1> and <technique 2>)**

Ans: External proxy and Multi-hop proxy