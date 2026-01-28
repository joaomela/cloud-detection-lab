# Logging Sources
This document describes the AWS telemetry used in this lab, what each source provides, and its limitations.


---


## CloudTrail

**Description:**
Logs all AWS API activity performed by users, roles, and services.

**Used For:**
 -  IAM credential abuse
 -  Resource enumeration
 -  Configuration changes
 -  S3 object-level access


**Detection Value**
Primary source for detecting identity and API abuse n AWS.


**Limitations:**
 -  No visibility into network payloads
 -  No insight into OS-level activity inside EC2 instances


---


## VPC Flow Logs


**Description:**
Captures metadata about network traffic flowing in and out of network interfaces.


**Used For:**
 -  Port scanning detection
 -  Suspicious outbound connections
 -  Unusual traffic patterns


**Detection Value:**
Provides network-level visibility that complements CloudTrail

**Limitations:**
-  No packet payloads
-  No application-layer context


---


## S3 Access Logs


**Description:**
Records requests made to S3 buckets and objects.


**Used For:**
-  Data exfiltration detection
-  Abnormal object access behavior


**Detection Value:**
Critical for identifying suspicious data access patterns.


**Limitations:**
-  Log delivery delay
-  Less real-time than CloudTrail data events


---



## GuardDuty


**Description:**
AWS-managed threat detection service analyzing multiple telemetry sources.


**Used For:**
-  Baseline alerting
-  Comparison with custom detections


**Detection Value:**
Provides fast, managed threat intelligence-based findings.


**Limitations:**
-  Limited customization
-  Should not replace custom detection logic

