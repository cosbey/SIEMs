
# Investigating Suricata Logs in Splunk

To identify the IP address that performed a scan on a compromised website using Splunk and Suricata logs, you can follow these steps:

### 1. Access Suricata Logs in Splunk
First, ensure that your Suricata logs are properly indexed in Splunk. You can verify this by running a simple search to see if data from Suricata is available:

```spl
index=<your_suricata_index> sourcetype=suricata
```

Replace `<your_suricata_index>` with the actual index name where Suricata logs are stored.

### 2. Identify Relevant Suricata Events
Suricata logs network security events, which can include port scans, network anomalies, and potential threats. You need to identify events that indicate a scan. Common event types related to scans in Suricata include:

- `event_type=alert`
- `alert.signature` containing terms like "Scan" or "Reconnaissance"

### 3. Search for Scan Events
Construct a search query to find scan events. For example:

```spl
index=<your_suricata_index> sourcetype=suricata event_type=alert alert.signature=*Scan*
```

This query filters for alert events where the signature includes the term "Scan".

### 4. Extract Relevant Fields
From the resulting events, you need to extract fields such as the source IP (`src_ip`) and destination IP (`dest_ip`).

### 5. Identify the Source IP of the Scan
To identify the specific IP address that performed the scan, refine your search to include a time range around when the compromise was detected. For example:

```spl
index=<your_suricata_index> sourcetype=suricata event_type=alert alert.signature=*Scan* earliest=-24h
```

You can adjust the `earliest` time range based on your investigation needs.

### 6. Analyze and Visualize the Results
Use Splunk’s visualization tools to analyze the results. For instance, you can create a table of source IPs and the count of scan events associated with each:

```spl
index=<your_suricata_index> sourcetype=suricata event_type=alert alert.signature=*Scan* earliest=-24h
| stats count by src_ip
| sort - count
```

This query gives you a list of source IPs sorted by the number of scan events they generated.

### Example Query
Here’s a complete example query that combines these steps:

```spl
index=<your_suricata_index> sourcetype=suricata event_type=alert alert.signature=*Scan* earliest=-24h
| stats count by src_ip, dest_ip, alert.signature
| sort - count
```

This query provides a count of scan events grouped by source IP, destination IP, and the alert signature, sorted by the number of occurrences.

### Additional Steps
- **Review Top IPs**: Investigate the top source IPs further by looking at their activity patterns and checking for any additional suspicious behavior.
- **Correlate with Other Data Sources**: If you have other relevant data sources in Splunk (e.g., web server logs, firewall logs), correlate these with the Suricata logs to get a fuller picture of the incident.
- **Create Alerts**: Consider setting up real-time alerts in Splunk for future scan activities to catch potential threats early.

By following these steps, you should be able to identify the IP address that performed the scan on your compromised website. If you encounter any specific issues or need further assistance with the queries, feel free to ask!