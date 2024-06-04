# Boss of the SOC Data Source Types

The source types for “Boss of the SOC” center around a few major types of tools that we use to collect data on hosts; primarily the following:

**Windows-TA**

- This is the default Windows-TA for Splunk and collects not only EventLog data but also registry information

**Sysmon-TA**

- This TA collects information generated from the Sysmon tool

**Fortinet Fortigate Add-on for Splunk**

- The scenario uses a Fortinet Fortigate devices as a “Next Generation Firewall” (NGFW). The Fortigate device in this scenario is configured to log network traffic crossing from internal to external, any alerts/blocks, layer 7 protection, and events that the Fortigate device logs

**Stream**

- Stream is Splunk’s wiredata collection/creation tool. It can capture a wide variety of traffic (including PCAPS and payloads!) on a network and turn them into wire metadata that is ingested into Splunk. The source type is broken out into all of the captured/detected protocols (`IE stream:dns, stream:http, etc`). In this exercise, we have turned on every possible option for Stream so that you can experience the full awesomeness of the tool

**IIS**

- Internet Information Services (IIS) is Microsoft’s default webserver on Windows Server Operating systems. It will show the access and utilization of websites hosted on Windows Web Servers

**Suricata**

- Suricata is a widely used open source IDS similar to Snort. It inspects packets traversing the network and creates alerts based on signatures. In this dataset, we are using a free signature pack provided by Emerging Threats