<h1>Run Secure Environment for 24 Hours and Capture Analytics</h1>

- <b>All map queries actually returned no results due to no instances of malicious activity for the 24-hour period after hardening</b>

## Metrics After Hardening / Security Controls

- <b>The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:</b>
- <b>Start Time 2024-10-02 19:22:57</b>
- <b>Stop Time	2024-10-03 19:22:57</b>

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 407
| Syslog                   | 3
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 48

![image](https://github.com/user-attachments/assets/d9f23233-f3e3-4982-a4c9-db84fbd00c2a)

- <b>SecurityEvent (Windows Event Logs)</b>

```
SecurityEvent
| where TimeGenerated >= ago(24h)
| count
```
![image](https://github.com/user-attachments/assets/d694e069-fa55-46b8-b0f6-1a96ab8612c6)

- <b>Syslog (Linux Event Logs)</b>
```
Syslog
| where TimeGenerated >= ago(24h)
| count
```

![image](https://github.com/user-attachments/assets/593ce507-94d9-46af-b38c-8cc1d000c5c4)

- <b>SecurityAlert (Microsoft Defender for Cloud)</b>
```
SecurityAlert
| where DisplayName !startswith "CUSTOM" and DisplayName !startswith "TEST"
| where TimeGenerated >= ago(24h)
| count
```
![image](https://github.com/user-attachments/assets/9ceae795-282d-4e7d-b18a-0c4ba08e17ad)

- <b>SecurityIncident (Incidents created by Sentinel)</b>
```
SecurityIncident
| where TimeGenerated >= ago(24h)
| count
```
![image](https://github.com/user-attachments/assets/5d931897-f5f9-4ef4-b2db-01a806d6d135)

- <b>AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)</b>
```
AzureNetworkAnalytics_CL 
| where FlowType_s == "MaliciousFlow" and AllowedInFlows_d > 0
| where TimeGenerated >= ago(24h)
| count
```
![image](https://github.com/user-attachments/assets/6f5474ff-c51a-46b6-97f8-142c72c358d7)
