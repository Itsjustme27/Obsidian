![Zeek signatures task image.](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/a6fb1153dfbd0a96dbf8f593027a9452.png)

**Zeek Signatures**  

Zeek supports signatures to have rules and event correlations to find noteworthy activities on the network. Zeek signatures use low-level pattern matching and cover conditions similar to Snort rules. Unlike Snort rules, Zeek rules are not the primary event detection point. Zeek has a scripting language and can chain multiple events to find an event of interest. We focus on the signatures in this task, and then we will focus on Zeek scripting in the following tasks.  

  

Zeek signatures are composed of three logical paths; signature id, conditions and action. The signature breakdown is shown in the table below;

  

|   |   |
|---|---|
|**Signature id**|**Unique** signature name.|
|**Conditions**|**Header:** Filtering the packet headers for specific source and destination addresses, protocol and port numbers.<br><br>**<br><br>**Content:** Filtering the packet payload for specific value/pattern.<br><br>**|
|**Action**|**Default action:** Create the "signatures.log" file in case of a signature match.<br><br>**Additional action:** Trigger a Zeek script.|

Now let's dig more into the Zeek signatures. The below table provides the most common conditions and filters for the Zeek signatures.

  

|   |   |
|---|---|
|Condition Field|Available Filters|
|Header|src-ip: Source IP.<br><br>dst-ip: Destination IP.<br><br>src-port: Source port.<br><br>dst-port: Destination port.<br><br>ip-proto: Target protocol. Supported protocols; TCP, UDP, ICMP, ICMP6, IP, IP6|
|Content|**payload:** Packet payload.  <br>**http-request:** Decoded HTTP requests.  <br>**http-request-header:** Client-side HTTP headers.  <br>**http-request-body:** Client-side HTTP request bodys.  <br>**http-reply-header:** Server-side HTTP headers.  <br>**http-reply-body:** Server-side HTTP request bodys.  <br>**ftp:** Command line input of FTP sessions.|
|**Context**|**same-ip:** Filtering the source and destination addresses for duplication.|
|Action|**event:** Signature match message.|
|**Comparison  <br>Operators**|**==**, **!=**, **<**, **<=**, **>**, **>=**|
|**NOTE!**|Filters accept string, numeric and regex values.|

Run Zeek with signature file

           `ubuntu@ubuntu$ zeek -C -r sample.pcap -s sample.sig`
        

  

|   |
|---|
|Zeek signatures use the ".sig" extension.|
|**-C:** Ignore checksum errors.<br><br> **-r:** Read pcap file.<br><br>**-s:** Use signature file.|

  

Example | Cleartext Submission of Password  

Let's create a simple signature to detect HTTP cleartext passwords.

**View Signature**           
        

Remember, Zeek signatures support regex. Regex ".*" matches any character zero or more times. The rule will match when a "password" phrase is detected in the packet payload. Once the match occurs, Zeek will generate an alert and create additional log files (signatures.log and notice.log).  

  

Signature Usage and Log Analysis

           `ubuntu@ubuntu$ zeek -C -r http.pcap -s http-password.sig  ubuntu@ubuntu$ ls clear-logs.sh  conn.log  files.log  http-password.sig  http.log  http.pcap  notice.log  packet_filter.log  signatures.log  ubuntu@ubuntu$ cat notice.log  | zeek-cut id.orig_h id.resp_h msg  10.10.57.178	44.228.249.3	10.10.57.178: Cleartext Password Found! 10.10.57.178	44.228.249.3	10.10.57.178: Cleartext Password Found!  ubuntu@ubuntu$ cat signatures.log | zeek-cut src_addr dest_addr sig_id event_msg  10.10.57.178		http-password	10.10.57.178: Cleartext Password Found! 10.10.57.178		http-password	10.10.57.178: Cleartext Password Found!`
        

  

As shown in the above terminal output, the signatures.log and notice.log provide basic details and the signature message. Both of the logs also have the application banner field. So it is possible to know where the signature match occurs. Let's look at the application banner!  

  

Log Analysis

           `ubuntu@ubuntu$ cat signatures.log | zeek-cut sub_msg POST /userinfo.php HTTP/1.1\x0d\x0aHost: testphp.vulnweb.com\x0d\x0aUser-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:98.0) Gecko/20100101 Firefox/...  ubuntu@ubuntu$ cat notice.log  | zeek-cut sub POST /userinfo.php HTTP/1.1\x0d\x0aHost: testphp.vulnweb.com\x0d\x0aUser-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:98.0) Gecko/20100101 Firefox/...`
        

We will demonstrate only one log file output to avoid duplication after this point. You can practice discovering the event of interest by analysing notice.log and signatures.log.

  

Example | FTP Brute-force

  

Let's create another rule to filter FTP traffic. This time, we will use the FTP content filter to investigate command-line inputs of the FTP traffic. The aim is to detect FTP "admin" login attempts. This basic signature will help us identify the admin login attempts and have an idea of possible admin account abuse or compromise events.

**View Signature**           
        

Let's run the Zeek with the signature and investigate the signatures.log and notice.log.  
  

FTP Signature

           `ubuntu@ubuntu$ zeek -C -r ftp.pcap -s ftp-admin.sig ubuntu@ubuntu$ cat signatures.log | zeek-cut src_addr dst_addr event_msg sub_msg | sort -r| uniq 10.234.125.254	10.121.70.151	10.234.125.254: FTP Admin Login Attempt!	USER administrator 10.234.125.254	10.121.70.151	10.234.125.254: FTP Admin Login Attempt!	USER admin` 
        

Our rule shows us that there are multiple logging attempts with account names containing the "admin" phrase. The output gives us great information to notice if there is a brute-force attempt for an admin account.

  

This signature can be considered a case signature. While it is accurate and works fine, we need global signatures to detect the "known threats/anomalies". We will need those case-based signatures for significant and sophistical anomalies like zero-days and insider attacks in the real-life environment. Having individual rules for each case will create dozens of logs and alerts and cause missing the real anomaly. The critical point is logging logically, not logging everything.

  

We can improve our signature by not limiting the focus only to an admin account. In that case, we need to know how the FTP protocol works and the default response codes. If you don't know these details, please refer to [RFC documentation](https://datatracker.ietf.org/doc/html/rfc765). 

  

**Let's optimise our rule and make it detect all possible FTP brute-force attempts.  
  
**

This signature will create logs for each event containing "FTP 530 response", which allows us to track the login failure events regardless of username. 

**View Signature**           
        

Zeek signature files can consist of multiple signatures. Therefore we can have one file for each protocol/situation/threat type. Let's demonstrate this feature in our global rule.

**View Signature**           
        

Let's merge both of the signatures in a single file. We will have two different signatures, and they will generate alerts according to match status. The result will show us how we benefit from this action. Again, we will need the "CLI Kung-Fu" skills to extract the event of interest.

  

This rule should show us two types of alerts and help us to correlate the events by having "FTP Username Input" and "FTP Brute-force Attempt" event messages. Let's investigate the logs. We're grepping the logs in range 1001-1004 to demonstrate that the first rule matches two different accounts (admin and administrator). 

  

FTP Signature

           `ubuntu@ubuntu$ zeek -C -r ftp.pcap -s ftp-admin.sig ubuntu@ubuntu$ cat notice.log | zeek-cut uid id.orig_h id.resp_h msg sub | sort -r| nl | uniq | sed -n '1001,1004p'   1001	CeMYiaHA6AkfhSnd	10.234.125.254	10.121.70.151	10.234.125.254: FTP Username Input Found!	USER admin   1002	CeMYiaHA6AkfhSnd	10.234.125.254	10.121.70.151	10.121.70.151: FTP Brute-force Attempt!	530 Login incorrect.   1003	CeDTDZ2erDNF5w7dyf	10.234.125.254	10.121.70.151	10.234.125.254: FTP Username Input Found!	USER administrator   1004	CeDTDZ2erDNF5w7dyf	10.234.125.254	10.121.70.151	10.121.70.151: FTP Brute-force Attempt!	530 Login incorrect.`
        

  

**Snort Rules in Zeek?**  

  

While Zeek was known as Bro, it supported Snort rules with a script called snort2bro, which converted Snort rules to Bro signatures. However, after the rebranding, workflows between the two platforms have changed. [The official Zeek document](https://docs.zeek.org/en/master/frameworks/signatures.html) mentions that the script is no longer supported and is not a part of the Zeek distribution.