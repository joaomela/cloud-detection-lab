

## IAM Credential Abuse
IAM enumeration was successfully simulated using an IAM user via AWS CloudShell.
CloudTrail management events such as ListBuckets were observed in the correct region,
confirming telemetry availability for detection validation.


### MITRE Mapping
-  Tactic: Credential Access / Discovery
-  Technique: Valid Accounts
-  Data Source: AWS Access
-  Telemetry: CloudTrail Logs

### Detection
Trigger an alert when AWS enumeration API calls (e.g., ListBuckets, ListUsers, ListRoles) are executed by an IAM principal under one or more of the following conditions:
- Originating from an unknown or external IP address
- Occurring outside normal business hours
- Performed by a user or role that does not typically perform administrative actions
- Followed by additional discovery or privilege-related API calls within a short time window

Initial enumeration events should be treated as early warning signals and prioritized for investigation when combined with subsequent privilege escalation or data access activity.


###  Limitations
CloudTrail logs only capture AWS API activity and do not provide insight into the intent behind the actions.
Read-only enumeration events such as ListBuckets or ListUsers may be part of legitimate administrative workflows.

Without contextual enrichment such as baseline user behavior, known source IPs, or time-of-day analysis, these events alone are insufficient to confirm malicious activity.
Additional correlation with other API calls (e.g., GetObject, CreateUser, AttachRolePolicy) is required to assess attack progression.


### Log Example 
```
{
  "eventVersion": "1.0",
  "userIdentity": {
    "type": "IAMUser",
    "principalId": "AIDA...",
    "arn": "arn:aws:iam::123456789012:user/MyUser",
    "accountId": "123456789012",
    "accessKeyId": "ASIA...",
    "userName": "MyUser"
  },
  "eventTime": "2026-01-21T10:30:00Z",
  "eventSource": "s3.amazonaws.com",
  "eventName": "ListBuckets",
  "awsRegion": "us-east-1",
  "sourceIPAddress": "203.0.113.42",
  "userAgent": "aws-cli/2.15.28 Python/3.11.6 Linux/5.15.0-105-generic",
  "requestParameters": {}, // Empty for ListBuckets as no specific bucket is targeted
  "responseElements": {
    "Buckets": [ // Array of buckets found
      {
        "Name": "my-first-bucket-123",
        "CreationDate": "2023-01-15T12:00:00Z"
      },
      {
        "Name": "my-second-bucket-456",
        "CreationDate": "2024-05-20T09:00:00Z"
      }
    ],
    "Owner": {
      "DisplayName": "my-user-name",
      "ID": "123456789012"
    }
  },
  "requestID": "...",
  "eventID": "...",
  "readOnly": true, // Indicates a read operation
  "eventType": "AwsApiCall", // Type of event recorded
  "recipientAccountID": "123456789012"
}
```
### Analysis
CloudTrail logs show the use of valid IAM credentials to perform management API calls such as ListBuckets.
These actions are commonly associated with initial account reconnaissance following credential compromise.

While the API calls themselves are legitimate, their execution outside of normal administrative workflows may indicate malicious intent.
Attackers typically use enumeration techniques to understand the available resources and identify high-value targets such as S3 buckets, IAM users, and roles.

If not detected early, this activity may lead to privilege escalation, persistence through the creation of new IAM users or access keys, and eventual data exfiltration.

