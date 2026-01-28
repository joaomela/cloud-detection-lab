
# CloudTrail Detections

This document describes detections based on AWS CloudTrail logs.


---


## Detection 1: Suspicious IAM API Enumeration


**Attack Scenario:**
IAM Credential Abuse


**MITRE ATT&CK Mapping:**
-  Tactic: Credential Access
-  Technique: Valid Accounts


**Log Source:**
AWS CloudTrail (Management Events)


**Detection Logic:**
Detects an unusual sequence of IAM and discovery-related API calls (ListUsers, ListRoles, ListBuckets) performed by a single identity within a short time window.


**Why This Is Suspicious:**
Legitimate users rarely enumerate multiple IAM and account-wide resources in rapid succession.


**False Positive Considerations:**
-  Cloud administrators performing audits
-  Automated inventory tools


**Severity:**
High