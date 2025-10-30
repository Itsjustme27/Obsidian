## Room Type :

> **_Free Room  
> _**_Anyone can deploy virtual machines in the room (without being subscribed)!_

## Task 1 : Introduction

This module is a basic intro to this room :

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*s5LR5EAzxjhlIhZxAVQ0aQ.png)

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*zMkMg0SPkoZGuCcm96F2sw.png)

## Task 2 : The Incident Response Documentation Universe

> **Task 2 Question : Can multiple use cases trigger a single playbook? y/n**

Yes, multiple use cases can trigger a single playbook.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*VZNGUzol6MEctaR_dHH62w.png)

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*1jKhKVA4JSlM6Hlc-HB6Hg.png)

## Task 3 : IR Process and Playbooks: Preparation

> **Task 3 — Question : What stage of the IR process can be translated into prerequisites for the playbooks?**

The **Preparation** stage of the Incident Response (IR) process can be translated into prerequisites for playbooks. This stage involves defining policies, processes, and tools that must be in place before an incident occurs. It ensures that the team is ready to respond effectively

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*R1ceW3S9DOBRp-UBLKhJhA.png)

> Task 3 is now Complete !

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*CcCdEsMXarqIgXe2zSMLfQ.png)

## Task 4 : IR Process and Playbooks: Detection and Analysis

> **Task 4 Question : What steps should we follow if the incident is a False Positive?**

If an incident is identified as a false positive, These steps should be followed :

**Document the False Positive**: Record all relevant details of the alert, including why it was deemed a false positive, to maintain a clear audit trail.  
**Analyze the Root Cause**: Investigate why the alert was triggered and determine whether it was due to a misconfiguration, incorrect detection logic, or unusual but benign activity.  
**Update Detection Logic**: If necessary, adjust or fine-tune detection rules or thresholds to reduce similar false positives in the future.  
**Communicate with the Team**: Notify relevant team members or stakeholders that the alert was a false positive and explain the actions taken.  
**and in the end →**

**Close the Incident**: Properly mark the incident as resolved and close the ticket in the incident tracking system, categorizing it as a false positive.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*-5KGAG_RknXve6pfAjRHQA.png)

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*yf2aCiEYDrcbwil_lrMgoQ.png)

## Task 5 : IR Process and Playbooks: Containment, Eradication, and Recovery

> **Task 5 — Question : To recover systems affected by an incident, which configuration should we bring them back to?**

To recover systems affected by an incident, they should be brought back to their **last known good configuration**. This is the system state before the incident occurred, where the system was functioning normally without any compromise or corruption.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*PU9H6vYA-TXjduZyHkBIFg.png)

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*h7J5lTJg3K8WR12xxA09uQ.png)

## Task 6 : IR Process and Playbooks: Post-Incident Activity

> **Task 6 Question : What is the last stage of the IR process?**

The last stage of the Incident Response (IR) process is typically referred to as **Post-Incident Activity**

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*uMibtvTzdTk-gs5dog_SHg.png)

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*GP57z3eUKH7OGSFiRxwigw.png)

## Task 7 : Putting It Into Practice

This module requires to start the VM

Once you start the machine , the details are shared to you :

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*5L9ytDjpVqkjvXjEGg7h4A.png)

Note the ip address for you would be different

> **After following the link asked in the module we get a login page**

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*CtlaFxSiPk1jLK9itXeUjQ.png)

> **The user credentials are being shared →**

elastic : elastic 

> **After successfully login in , we see a dashboard →**

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*Aazti_BaojNG3696RmPIVw.png)

> **Task 7 — Question 1 : What is the name of the process that initiated this communication?**

Let’s check the information provided to us →

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*dCQFUoKeTScOUt_EysoykQ.png)

> **The hint for Question 1 :**

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*qnr1K0qp_PGd_BlaETJaOw.png)

Hint for Task 7 Question 1 is given

we have a search string to check the destination ip address along with date

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*2TyYwqlYFtjY1W2VzJc1OA.gif)

We see the Process name with the date and ip filters →

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*V1c7J8BKuosouel0WXKiyw.png)

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*nv6cqx0svgl_JG5HReraOQ.png)

> **Task 7 — Question 2 : Is this process malicious, as per VirusTotal? y/n**

we can find the VirusTotal website from google →

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*bTMTlQ0SV_4TWXseA2zajA.png)

There are three ways to check — with File , URL and by Searching

> **We can find a URL from the elastic search**

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*-4lqatXLln33QXfKZYDfwA.png)

> **URL That we found →**

http://schemas.microsoft.com/win/2004/08/events/event

> **Now let’s use the URL above and search on VirusTotal →**

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*4AcDIYLspLcMp397U5b9zA.png)

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*Z2YCh1b0RYEXTQDYQRYg2Q.png)

> **The URL is clean and free from being Malicious**
> 
> **Task 7 Question 3 : What is the name of the parent process of this process?**

by Adding filter , we see the paent process name entry value

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*ta3A-78fA4-16n1IGmpCow.png)

> **By selecting the parent_process_name the first value is our answer**

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*hzr9zrYk8gpi3dr6rOyugw.png)

> **Task 7 — Question 4 : This process’s parent was launched by another process, which is a notorious ransomware. Which ransomware is that?**

Let’s ask our Friend google —

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*cfBRYFBcybcpG8gIyKpfCw.png)

You can also use the Chart set to — Bar Vertical Stacked and get the same result from the filter option .

> **Task 7 — Question 5 : Which playbook should be followed to respond to this incident?**

malware playbook

> **Task 7 — Question 6 : Is this incident an FP (False Positive) or a TP (True Positive)?**

TP

> **Task 7 Question 7 : In case the incident is a TP, what will be the next step in the IR process?**

Containment

### Task 7 is now Complete !

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*hExzQbVjs14qjlVJvQNEkg.png)

## Task 8 : Conclusion

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*RKdOF9ToNuHOvO0icsJeEQ.png)

> We have successfully completed the room !