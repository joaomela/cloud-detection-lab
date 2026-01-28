## 1. VPC Design

- **CIDR Block:** `192.168.0.0/16` for the VPC
    
- **Subnet Strategy:**
    
    - **Public subnets:** connected to the Internet via an Internet Gateway; used for resources that must be accessible externally (e.g., public-facing apps).
        
    - **Private subnets:** no direct internet access; can reach the internet only through NAT if required.
        
- **Rationale:** This separation minimizes the attack surface and reduces blast radius in case of compromise.
    

---

## 2. Network Security

- **Security Groups (SGs):** primary line of defense; control inbound/outbound access to EC2 instances and other resources.
    
- **Network ACLs (NACLs):** secondary defense; applied at the subnet level for extra segmentation and logging.
    
- **Protected Assets:** EC2, S3 (through VPC endpoints or IAM policies), internal subnets.
    
- **Common Misconfigurations:**
    
    - Overly permissive SGs or NACLs → unnecessary exposure
        
    - Overly restrictive SGs → breaks legitimate traffic
        
- **Detection Impact:**
    
    - Misconfigured SGs can be exploited by attackers
        
    - Overly permissive NACLs can generate noise in detection systems
        

---

## 3. Compute Placement

- **Public EC2 Instances:**
    
    - Must be reachable from the Internet (e.g., web servers, bastion hosts).
        
- **Private EC2 Instances:**
    
    - Not directly accessible externally (e.g., databases, internal services).
        
- **Rationale:** Minimizes exposure of critical assets while allowing controlled access for operational needs.
    

---

## 4. IAM Design

- **Users:** persistent human identities; credentials are fixed and must be protected. Common target for credential leaks.
    
- **Roles:** temporary identities assumed by instances or services (e.g., EC2, Lambda). Can be abused if misconfigured.
    
- **Least Privilege Principle:**
    
    - Assign only the minimum permissions required to perform a task.
        
    - Reduces risk of privilege escalation and limits potential damage in case of compromise.
        

---

## 5. S3 Design

- **Sensitive Bucket:** example `company-data` bucket is a potential exfiltration target.
    
- **Threat Scenario:** compromised IAM credentials or role abuse can lead to unauthorized data copying.
    
- **Logging:** CloudTrail logging is enabled to capture read/write access, object-level operations, and API activity.
    
- **Rationale:** Logging allows detection, investigation, and response to malicious activity.