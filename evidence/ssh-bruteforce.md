## EC2 Compromise
Multiple inbound connections to TCP port 22 were observed from an external IP address within a short time window.
Although authentication success cannot be confirmed via VPC Flow Logs, the pattern is consistent with SSH enumeration or brute-force activity.

### MITRE Mapping
-  Tactic: Initial Access
-  Technique: T1110 - Brute Force
-  Data Source: Network Traffic
-  Telemetry: VPC Flow Logs

### Detection
Alert when multiple inbound connections to port 22 from the same source IP occur within 5 minutes

### Limitations
VPC Flow Logs do not provide authentication context or command execution details.  
Additional host-based logs would be required to confirm compromise.

### Log Example 
2 338330xxxx eni-0a8350ddxxxxxxx 192.168.x.xxx x.x.x.x 52515 6 10 2049 1768999384 1768999414 ACCEPT OK

### Analysis
The VPC Flow Log entry indicates multiple inbound TCP connections to port 22 targeting an EC2 instance from an external IP address.
Port 22 is commonly used for SSH and is a frequent target for automated scanning and brute-force attempts.

The repeated connection attempts within a short time window suggest enumeration activity rather than normal administrative access.
While the log confirms that network access was allowed (ACCEPT), it does not provide visibility into authentication success.

If successful, such activity could lead to unauthorized access to the instance, enabling persistence, lateral movement, or credential harvesting through attached IAM roles.

Legitimate administrative SSH access should be rare and originate from known IP addresses.
