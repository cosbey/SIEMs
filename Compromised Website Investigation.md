

# Compromised Website Investigation

Investigating a compromised website involves collecting various artifacts to understand the scope of the breach, identify the attacker, and determine the method of compromise. 

1. **The first step is to identify the 5 W's of the incident.**

	a. Who were the victims, attackers of the compromise? *Servers, People, etc....*
	b. What happened? *Compromised, breach?*
	c. When did it happen? *Date and time*
	d. Where did it happen? *Server, host machines, Email?*
	e. Why did it happen? *To be determined..*

Gather as much evidence as possible. This will be used to investigate our system log in our environment. 

2. **Identify the sourcetype available in our SIEM (Splunk). 
- IDS
- UTM
- FIREWALL
- HTTP STREAM
- WINDOWS EVENT LOGS AND SYSMON
- SERVERS



To begin our investigation we need to search the SIEM with the artifacts we've collected earlier.

### EXAMPLE

Here are the typical artifacts you should retrieve:

### 1. **Web Server Logs**
   - **Access Logs**: These logs show who accessed the website, from which IP, and what resources they accessed. Look for unusual access patterns, such as requests from suspicious IP addresses, repeated access attempts, or requests to unusual endpoints.
   - **Error Logs**: These logs can provide insights into any errors encountered by the server, which might indicate attempted exploits or successful exploitation.
   - **Event Logs**: Logs of various events on the server, including user actions and system events.

### 2. **Application Logs**
   - **CMS Logs**: If you use a content management system (e.g., WordPress, Joomla), check its logs for login attempts, plugin installations, and other administrative actions.
   - **Custom Application Logs**: Logs specific to your application that might reveal unusual behavior or errors.

### 3. **Database Logs**
   - **Query Logs**: Logs of SQL queries executed, which can show if the attacker attempted or succeeded in SQL injection.
   - **Error Logs**: Logs that capture any errors encountered by the database server.

### 4. **Network Traffic Logs**
   - **Firewall Logs**: Logs showing inbound and outbound traffic. Look for unusual connections or repeated connection attempts.
   - **Intrusion Detection/Prevention System Logs**: Logs from IDS/IPS systems that might have detected suspicious traffic.

### 5. **System Logs**
   - **Authentication Logs**: Logs from the operating system or authentication services showing login attempts, especially failed ones or successful logins from unusual locations.
   - **Process Logs**: Logs showing running processes and any new processes that started, which might indicate the presence of malicious scripts or executables.

### 6. **File Integrity Monitoring Logs**
   - **File Change Logs**: Logs that capture changes to critical files (e.g., website files, configuration files). Look for unauthorized changes or additions, especially in directories where web content is stored.

### 7. **Web Application Firewall (WAF) Logs**
   - Logs from any WAF you have deployed, showing blocked or allowed requests that might indicate attack patterns such as SQL injection or cross-site scripting (XSS).

### 8. **User Activity Logs**
   - **Admin and User Activity Logs**: Logs of actions performed by administrators and regular users. Look for any unauthorized administrative actions or unusual user behavior.

### 9. **System Snapshots**
   - **Snapshots or Backups**: Recent snapshots or backups of the system state that can be compared to current state to identify unauthorized changes.

### 10. **Artifacts from Potentially Compromised Files**
   - **Malicious Scripts/Files**: Any new or modified files that seem out of place or are confirmed as malicious. This includes web shells, backdoors, or other scripts.
   - **Malicious Code in Existing Files**: Inserts or modifications in legitimate files, such as injected PHP or JavaScript code.

### 11. **Configuration Files**
   - **Web Server Configuration**: Files like `httpd.conf` or `nginx.conf` which might have been modified to aid the attacker.
   - **Application Configuration**: Configuration files of your application, which might have been altered to introduce vulnerabilities or gain persistent access.

### 12. **Forensic Data**
   - **Memory Dumps**: If you suspect the server is compromised, memory dumps can capture the state of the system, including any running malicious processes.
   - **Disk Images**: Full disk images can be useful for offline analysis and to preserve the state of the system for further investigation.

### Collecting and Analyzing Artifacts

1. **Establish a Timeline**:
   - Correlate timestamps across different logs to build a timeline of the attack. This helps in understanding the sequence of events.

2. **Identify Indicators of Compromise (IoCs)**:
   - Look for known IoCs such as specific IP addresses, file hashes, URLs, and domain names associated with the attack.

3. **Cross-Reference Logs**:
   - Use logs from different sources to corroborate findings and get a comprehensive view of the attack.

4. **Secure the Compromised Environment**:
   - Ensure the compromised system is isolated to prevent further damage and to preserve evidence.

By gathering and analyzing these artifacts, you can understand the nature of the compromise, identify the attack vectors, and develop a plan for remediation and prevention of future incidents.