## Kill Chain Summary
1. Valid IAM credentials were used to enumerate resources (ListBuckets)
2. Network telemetry confirms external connectivity to cloud resources
3. S3 GetObject confirms successful data access

## Business Impact
Unauthorized access to cloud storage may result in:
- Data leakage
- Regulatory impact (GDPR)
- Loss of customer trust

## Defensive Recommendations
- Enforce least privilege IAM policies
- Enable CloudTrail Data Events for all sensitive buckets
- Create alerts for unusual GetObject activity
- Rotate compromised credentials

## Logging Is Not Enabled by Default
Critical telemetry such as S3 data access events is not collected unless
explicitly configured. Without enabling CloudTrail Data Events, real data exfiltration would remain invisible.

## Cloud Attacks Look Like Legitimate Activity
All observed attack actions used valid AWS APIs. No malware or exploits were required, highlighting how cloud attacks often blend into normal activity.

## Context Is Essential for Detection
Individual events such as ListBuckets or GetObject are not inherently malicious. Detection requires contextual correlation, including identity, source IP, timing, and access patterns.

## Network Logs Have Limited Visibility
VPC Flow Logs provide useful network metadata but lack authentication or payload-level context. They must be combined with CloudTrail for effective investigation.

## Early Detection Reduces Impact
Detecting IAM enumeration early can prevent follow-on actions such as privilege escalation, persistence, and data exfiltration.
