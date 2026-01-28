
# S3 Detections


---


## Detection 3: Abnormal S3 Object Download Activity


**Attack Scenario:**
S3 Data Exfiltration


**MITRE ATT&CK Mapping:**
-  Tactic: Exfiltration
-  Technique: Exfiltration Over Web Service


**Log Source:**
CloudTrail (S3 Data Events) / S3 Access Logs


**Detection Logic:**
Detects a high volume of GetObject request or large data transfers from a single identity or source IP in a short period of time.


**Why This Is Suspicious:**
Mass downloads are uncommon in normal S3 usage patterns and often indicate data exfiltration.


**False Positive Considerations:**
-  Backup jobs
-  Data analytics workflows


**Severity:**
High