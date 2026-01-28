# Sigma Overview

This project focuses on defining detection logic for common AWS cloud attack patterns using a SIEM-agnostic approach.

The detections described are based on real CloudTrail and VPC Flow Logs generated during the lab and are designed to be portable across different security monitoring platforms.

## Detection Scope
The following attack behaviors were covered:
- IAM enumeration using valid credentials
- Suspicious network activity targeting EC2 instances
- Unauthorized S3 object access

## Example Detection Use Cases
- Multiple List* API calls by non-administrative IAM users
- Repeated inbound SSH connections from external IPs
- S3 GetObject operations from unusual source IPs or identities

## Future Sigma Implementation
Each detection can be translated into Sigma rules by:
- Mapping CloudTrail fields to Sigma log source definitions
- Defining selection criteria based on eventName and userIdentity
- Applying thresholds to reduce false positives

This approach enables consistent cloud detections across SIEM platforms such as Splunk, Elastic, Sentinel, or Chronicle.


### Sigma Rule Example

detection:
	selection:
		eventName: GetObject
		 userIdentity.type: IAMUser
	 filter:
		sourceIPAddress:
			-  "192.168.0.0/16"
	 condition: selection and not filter
