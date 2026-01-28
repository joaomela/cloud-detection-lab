# VPC Flow Log Detections


---


# Detection 2: Suspicious Outbound Network Activity from EC2


**Attack Scenario:**
EC2 Compromise


**MITRE ATT&CK Mapping:**
-  Tactic: Command and Control
-  Technique: Application Layer Protocol


**Log Source:**
VPC Flow Logs


**Detection Logic:**
Detects EC2 instances initiating outbound connections to unusual external IP addresses or uncommon ports within a short time window.


**Why This Is Suspicious:**
Compromised instances often establish outbound connections to attacker-controlled infrastructure.

**False Positive Considerations:**
-  Legitimate software updates
-  Third-party integrations

**Severity:**
Medium to High