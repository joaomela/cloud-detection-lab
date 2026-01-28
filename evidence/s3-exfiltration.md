## S3 Data Exfiltration

An S3 data access event was observed where an IAM user performed a GetObject operation against an S3 bucket.

The CloudTrail Data Event confirms that an object was successfully downloaded, with outbound bytes transferred to an external IP address.

This activity represents a confirmed data access action and, if unauthorized, may indicate data exfiltration following credential compromise.

### MITRE Mapping
- Tactic: Exfiltration
- Technique: Exfiltration Over Cloud Storage (T1537)
- Data Source: AWS S3
- Telemetry: CloudTrail Data Events

### Detection
Alert on S3 GetObject events when:
- Performed by IAM users or roles not normally accessing the bucket
- Source IP is external or unusual
- High volume or repeated GetObject requests in a short time window
- Performed after ListBuckets/ListObjects
- Used by recently created user
- Used in unusual hour

### Limitations
CloudTrail Data Events confirm that an object was accessed but do not provide visibility into the sensitivity of the data or whether the download was authorized.

Without user behavior baselines or data classification, it is not possible to determine intent solely from a single GetObject event.

Additional context such as IAM role purpose, access patterns, and data classification would be required to reduce false positives.
