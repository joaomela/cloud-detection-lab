### Scenario 1: IAM Credential Abuse

**Goal:** Unauthorized access to sensitive AWS resources.

**Entry Point:** Compromised IAM user credentials used via AWS CLI.

**Expected Impact:** Data access and enumeration of cloud resources.

**MITRE ATT&CK Mapping:**
- Tactic: Credential Access
- Technique: Valid Accounts

**Detection Clues:** Multiple failed ConsoleLogin events in CloudTrail, unusual API calls.

---

### Scenario 2: EC2 Compromise

**Goal:** Gain control over a public-facing EC2 instance and expand access.

**Entry Point:** Brute-force or stolen SSH credentials on a public EC2 instance.

**Expected Impact:** Command execution, persistence, lateral movement, and potential IAM role abuse.

**MITRE ATT&CK Mapping:**
- Tactic: Initial Access
- Technique: Valid Accounts

**Detection Clues:** Multiple failed SSH attempts, abnormal outbound traffic in VPC Flow Logs, suspicious CloudTrail activity from the EC2 role.

---

### Scenario 3: S3 Data Exfiltration

**Goal:** Exfiltrate sensitive data stored in S3.

**Entry Point:** Abuse of compromised IAM user or EC2 role permissions.

**Expected Impact:** Theft of sensitive data and potential compliance violations.

**MITRE ATT&CK Mapping:**
- Tactic: Exfiltration
- Technique: Exfiltration Over Web Service

**Detection Clues:** Large or abnormal volume of GetObject events in CloudTrail and S3 Access Logs.
