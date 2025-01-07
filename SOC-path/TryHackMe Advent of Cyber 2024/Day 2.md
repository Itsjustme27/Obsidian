
The Story

![Task banner for day 2.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5dbea226085ab6182a2ee0f7/room-content/5dbea226085ab6182a2ee0f7-1730369227263.png)

It’s the most wonderful time of the year again, and it’s also the most stressful day for Wareville’s Security Operations Center (SOC) team. Despite the overwhelming alerts generated by the new and noisy rules deployed, Wareville’s SOC analysts have been processing them nonstop to ensure the safety of the town.

However, the SOC analysts are now burning out of all the workload needed before Christmas. Numerous open cases are still pending, and similar alerts are still firing repeatedly, making them think of the possibility of false positives out of all this mess.

Now, help the awesome Wareville’s SOC team analyse the alerts to determine whether the rumour is true—that Mayor Malware is instigating chaos within the town.

## True Positives or False Positives?

In a SOC, events from different devices are sent to the SIEM, which is the single source of truth where all the information and events are aggregated. Certain rules (Detection Engineering rules) are defined to identify malicious or suspicious activity from these events. If an event or set of events fulfils the conditions of a rule, it triggers an alert. 

1) A SOC analyst then analyses the alert to identify if the alert is a True Positive (TP) or a False Positive (FP). An alert is considered a TP if it contains actual malicious activity. 
 
2) On the flip side, if the alert triggers because of an activity that is not actually malicious, it is considered an FP. This might seem very simple in theory, but practically, separating TPs from FPs can be a tedious job. It can sometimes become very confusing to differentiate between an attacker and a system administrator.

![Identifying true vs. false positives.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5dbea226085ab6182a2ee0f7/room-content/5dbea226085ab6182a2ee0f7-1730369255180.png)


**Using the SOC Superpower**

The SOC has a superpower. When they are unsure whether an activity is performed by a malicious actor or a legitimate user, they can just confirm with the user. This privilege is not available to the attacker. A SOC analyst, on the other hand, can just send an email or call the relevant person to get confirmation of a certain activity. In mature organisations, any changes that might trigger an alert in the SOC often require Change Requests to be created and approved through the IT change management process. Depending on the process, the SOC team can ask the users to share Change Request details for confirmation. Surely, if it is a legitimate and approved activity, it must have an approved Change Request.

**Context**

While it might seem like using the SOC superpower makes things super easy, that is not always the case. There are cases which can act as Kryptonite to the SOC superpower:

- If an organisation doesn't have a change request process in place.
- The performed activity was outside the scope of the change request or was different from that of the approved change request.
- The activity triggered an alert, such as copying files to a certain location, uploading a file to some website, or a failed login to a system. 
- An insider threat performed an activity they are not authorised to perform, whether intentionally or unintentionally.
- A user performed a malicious activity via social engineering from a threat actor.

In such scenarios, it is very important for the SOC analyst to understand the context of the activity and make a judgement call based on their analysis skills and security knowledge. While doing so, the analyst can look at the past behaviour of the user or the prevalence of a certain event or artefact throughout the organisation or a certain department. For example, if a certain user from the network team is using Wireshark, there is a chance that other users from the same team also use Wireshark. However, Wireshark seen on a machine belonging to someone from HR or finance should rightfully raise some eyebrows.

**Correlation**

When building the context, the analyst must correlate different events to make a story or a timeline. Correlation entails using the past and future events to recreate a timeline of events. When performing correlation, it is important to note down certain important artefacts that can then be used to connect the dots. These important artefacts can include IP addresses, machine names, user names, hashes, file paths, etc.

Correlation requires a lot of hypothesis creation and ensuring that the evidence supports that hypothesis. A hypothesis can be something like the user downloaded malware from a spoofed domain. The evidence to support this can be proxy logs that support the hypothesis that a website was visited, the website used a spoofed domain name, and a certain file was downloaded from that website. Now, let's say, we want to identify whether the malware executed through some vulnerability in an application or a user intentionally executed the malware. To see that, we might look at the parent process of the malware and the command line parameters used to execute the said malware. If the parent process is Windows Explorer, we can assume the user executed the malware intentionally (or they might have been tricked into executing it via social engineering), but if the parent process is a web browser or a word processor, we can assume that the malware was not intentionally executed, but it was executed because of a vulnerability in the said application.

## Is this a TP or an FP?

Similar to every SOC, the analysts in the Wareville SOC also need to differentiate TPs from FPs. This becomes especially difficult for them near Christmas when the analysts face alert fatigue. High chances of misclassification of TPs into FPs and vice versa are present in such times. The analysts, therefore, appreciate any help they could get from us in this crucial time. To make matters worse, the office of the Mayor has sent the analysts an alert informing them of multiple encoded powershell commands run on their systems. Perhaps we can help with that.


## Write-up for Day 2: One man's false positive is another man's potpourri:

For Day 2 of Advent of Cyber 2024, I was tasked to analyze some logs.

1) First, I started the machine and, connect to the Elastic SIEM by visiting https://LAB_WEB_URL.p.thmlabs.com(https://lab_web_url.p.thmlabs.com/ ) your browser using the following credentials:

![TryHackMe Credentials](https://tryhackme-images.s3.amazonaws.com/user-uploads/5dbea226085ab6182a2ee0f7/room-content/0cbfa0d0f3a7f16cefa9fddd04b6de8d.png)

|              |                                   |
| ------------ | --------------------------------- |
| **URL**      | https://LAB_WEB_URL.p.thmlabs.com |
| **Username** | elastic                           |
| **Password** | elastic                           |

2) Once i logged in, I went to the hamburger icon and clicked on Discover tab.

	![Instructions to access the Discover console.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5dbea226085ab6182a2ee0f7/room-content/5dbea226085ab6182a2ee0f7-1730130654839.png)


3) According to the alert sent by the Mayor's office, the activity occurred on Dec 1st, 2024, between 09:00 and 09:30. So I filtered the logs from Dec 1st, 2024, 09:00 to 09:30 to make things easier. Note that we need to click the **Absolute** tab and set the exact time-frame we want to view. Lastly, click the **Update** button to apply the changes.

	![Instructions to configure the search timeframe.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5dbea226085ab6182a2ee0f7/room-content/5dbea226085ab6182a2ee0f7-1730130936812.png)

4) After hitting update i saw 21 hits/events in the mentioned time-frame.

	![[Pasted image 20241203090356.png]]

5) Then, I used some filters for some columns, since we are looking for events related to PowerShell, we would like to know the following details about the logs.

- The hostname where the command was run. We can use the `host.hostname` field as a column for that.
- The user who performed the activity. We can add the `user.name` field as a column for this information.
- We will add the `event.category` field to ensure we are looking at the correct event category.￼

- To know the actual commands run using PowerShell, we can add the `process.command_line` field.
- Finally, to know if the activity succeeded, we will add the `event.outcome` field.
	
	Once I added these fields as columns, we will see the results in a format like this.

	![View after adding the field columns.](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/61306d87a330ed00419e22e7-1728231315014.png)

7) It looked like someone ran the same encoded PowerShell command on multiple machines. Another thing to note here is that before each execution of the PowerShell command, we see an authentication event, which was successful.
	![[Pasted image 20241203091712.png]]

8) Now, since it's an Powershell command, someone must have run it, so to find the source of the IP we need to filter `source.ip` 

	![[Pasted image 20241203191025.png]]

9) After checking all the data through filtering, `user.name`  with  `service.admin` & `source.ip` with `10.0.11.11`

10) We can see the PowerShell command in the `process.command_line` field. 

	`C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -EncodedCommand SQBuAHMAdABhAGwAbAAtAFcAaQBuAGQAbwB3AHMAVQBwAGQAYQB0AGUAIAAtAEEAYwBjAGUAcAB0AEEAbABsACAALQBBAHUAdABvAFIAZQBiAG8AbwB0AA==`

11) Since it is a Base64 encoded command, McSkidy used two recipes, named `FromBase64` and `Decode text` from the left pane. Note that McSkidy configured the **Decode text** to **UTF-16LE (1200)** since it is the encoding used by PowerShell for Base64.

	![Applying recipes to decode the PowerShell command.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5dbea226085ab6182a2ee0f7/room-content/5dbea226085ab6182a2ee0f7-1730131884795.png)


I used the base64-decoder tool I coded via python to decode the Powershell command.


### Questions from the room

#### Answer the questions below

1) **What is the name of the account causing all the failed login attempts?**
	`service_admin`

2) **How many failed logon attempts were observed?**
	`6791`

3) **What is the IP address of Glitch?**
	`10.0.255.1`

4)  **When did Glitch successfully logon to ADM-01? Format: MMM D, YYYY HH:MM:SS.SSS**
	`Dec 1, 2024 08:54:39.000`

5) **What is the decoded command executed by Glitch to fix the systems of Wareville?**
	`Install-WindowsUpdate -AcceptAll -AutoReboot`


