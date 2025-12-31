
# What are logs?


- Logs are the digital evidence or "receipts" of historical activity, or events of the past activity.
- It is used to record an adversary's actions.

# Types, Format, and Standards of logs


## Types of Common/General Logs:

- **Application Logs:** Messages about specific applications, including status, errors, warnings, etc.

- **Audit Logs:** Activities related to operational procedures crucial for regulatory compliance.

- **Security Logs:** Security events such as logins, permissions changes, firewall activity, etc.

- **Server Logs:** Various logs a server generates, including system, event, error, and access logs.

- **System Logs:** Kernel activities, system errors, boot sequences, and hardware status.

- **Network Logs:** Network traffic, connections, and other network-related events.

- **Database Logs:** Activities within a database system, such as queries and updates.

- **Web Server Logs:** Requests processed by a web server, including URLs, response codes, etc.


## Log Formats:

- **Structured Logs:** Follows a strict format, easy for analysis. Examples are CSV, JSON, W3C Extended Log Format, and XML.

![[Pasted image 20251231145906.png]]


- **Unstructured Logs:** Free-text logs, rich but harder to parse. Examples include NCSA Common and Combined Log Formats.

![[Pasted image 20251231150105.png]]


- **Semi-Structured Logs:** Combination of Structured and Unstructured Logs. Example: Syslog and Windows Event Log.


![[Pasted image 20251231150331.png]]


# Specific Logs

1. **Firewall Logs:**

	- What to allow, and what not to allow.

	- **5-tuple format, the minimum set of instructions a firewall must identify:**
		- Source IP
		- Destination IP
		- Source Port
		- Destination Port
		- Protocol (TCP/UDP)

	- Types of Firewall Logs (FortiGate Logs):

| Type    | Description                                                                                                             | Subtype                                                                                                                                                                                                                                                                                                                                                                                              |
| ------- | ----------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| traffic | Records traffic flow information, such as an HTTP/HTTPS request and its response, if any.                               | - forward<br>    <br>- http-transaction<br>    <br>- local<br>    <br>- multicast<br>    <br>- sniffer<br>    <br>- ztna                                                                                                                                                                                                                                                                             |
| event   | Records system and administrative events, such as downloading a backup copy of the configuration, or daemon activities. | - cifs-auth-fail<br>    <br>- connector<br>    <br>- endpoint<br>    <br>- fortiextender<br>    <br>- ha<br>    <br>- rest-api<br>    <br>- router<br>    <br>- sdwan<br>    <br>- security-rating<br>    <br>- switch-controller<br>    <br>- system<br>    <br>- telemetry<br>    <br>- user<br>    <br>- vpn<br>    <br>- wanopt<br>    <br>- web-svc<br>    <br>- webproxy<br>    <br>- wireless |
| UTM     | Records UTM events                                                                                                      | - virus<br>- webfilter<br>- ips<br>etc.                                                                                                                                                                                                                                                                                                                                                              |



![[Pasted image 20251231111015.png]]



2. **Active Directory (AD):**

	- In a Windows Domain, the credentials stored in a centralized repository is called Active Directory.
	- The critical server in charge of running the Active Directory is called Domain Controller.
	- It uses Kerberos for secure authentication.
	- It uses LDAP (Lightweight Directory Access Protocol) for querying and managing directory information.

	![[Pasted image 20251231123424.png]]


## Kerberos Authentication process

-  **Authentication server request**:
	
	The client requests sends an authentication request to the Kerberos KDC AS. The initial authentication request is sent as plaintext because no senstitive information is included in the request. The AS verifies that the client is in the KDC database and retrieves the initiating client's private key.

-  **Authentication server response:** 
	
	The Authentication server looks for client's username in the KDC database. If the server doesn't find the username, the auth process is stopped otherwise it sends the client a ticket-granting ticket(TGT) and a session-key.

- **Service ticket request:**
	
	Once authenticated by the AS, the client asks for a service ticket from the TGS. This request must be accompanied by the TGT sent by the KDC AS.

- **Service ticket response:**
	
	If the TGS can authenticate the client, it sends credentials and a ticket to access the requested service. This transmission is encrypted with a session key specific to the user and service being accessed.


- **Application Server request:**
	
	The client sends a request to access the application server. This request includes the service ticket received in step 4. If the application server can authenticate this request, the client can access the server.


- **Application Server response:**
	
	In cases where the client requests the application server to authenticate itself, this response is required. The client has already authenticated itself, and the application server response includes Kerberos authentication of the server.


- Types of AD Logs:

	- **Security Log:** Tracks authentication/authorization, successful/failed logins, account lockouts, policy changes, and permission changes (Event IDs 4624 , 4625 for logins).
	
	- **System Log:** Records OS-level events, driver issues, hardware failures, and service starts/stops.
	
	- **Application Log:** Events from installed software like Exchange, IIS, or other custom apps.
	
	- **Directory Service Log:** Specific to AD, logging domain controller operations, replication issues, schema changes, and directory object modifications.
	
	- **DNS Server Log:** Monitors DNS queries, responses, and zone transfers, essential for name resolution issues.


- **Log Levels in AD:**
	
	- 0 (None): Only alerts critical errors
	- 1 (Minimal): High-level tasks
	- 3 (Extensive): Detailed steps for tasks
	- 5 (Internal): All events, including debug logs.


