I’ve recently compiled a list of generic AWS vulnerabilities & risks which could apply to any business.
They were pulled together based on a combination of some of the existing CIS benchmarking (see https://github.com/awslabs/aws-security-benchmark), some of the rules within Cloud Custodian (https://github.com/cloud-custodian/cloud-custodian) as well as some known areas of potential AWS weakness

They are a reasonable set of focus areas a business in the Cloud should focus on when trying to reduce cloud risk.





**IAM**
- IAM policy allows assume role permission across all services (assume/pass:*)
- Overly permissive IAM roles (wildcards)
- Overly permissive read access allows visibility to some customer data stores 
- Elasticsearch IAM policy allows internet traffic
- AWS IAM deprecated managed policies in use by User
- Access to modify security groups/ NACLs/ ENI's/ Route tables is not restricted in Prod
- Access to KMS is not restricted

**Security Groups**
- AWS Security Groups allow internet traffic to undesired ports
- Default Security Group does not restrict all traffic
- Security groups do not follow least privilege with regards to ports/ CIDR ranges
- Many groups allow RDP/SSH from any ip

**Root Account**
- MFA is not enabled on Root account
- Root account email is not on a distribution list

**MFA**
- Users do not have MFA activated for accounts

**Secrets / Keys (inc Access Key rotation)**
- Access keys are not rotated in line with industry standard best practice (90 days)
- KMS - default keys are used. 
- KMS - Keys are shared across services and functions where separate envelope keys should be used
- KMS - Access policies are too permissive. Too many services can call decrypt function for keys.

**Vulnerability Management**
- AMIs are not hardened
- No patching process for instances
- No vulnerability scanning on instances

**Compliance**
- Lack of visibility of current compliance status 
- No file integrity monitoring for PCI workloads
- No domain boundary program - lack of documentation around how PCI workloads are isolated (logically or otherwise)

**Encryption**
- AWS CloudFront origin protocol policy does not enforce HTTPS-only
- EBS volumes lack encryption
- S3 lack of encryption
- TLS is not enforced between ELB - EC2 
- RDS lack of encryption
- Redshift lack of encryption

**S3**
- AWS S3 Bucket has Global DELETE Permissions enabled via bucket policy
- AWS S3 Bucket has Global GET Permissions enabled via bucket policy
- S3 buckets are accessible to any authenticated user
- S3 buckets are accessible to public
- Log buckets are not sufficiently protected from PUT's (to protect against file over-ride/ deletes etc)
- Versioning is not enabled
- No bucket replication for high value workloads (minimal backups)

**Incident Response**
- Insufficient playbooks for AWS incident response
- Insufficient access to comms channels (e.g. Slack/JIRA/Trello/Email) for incidents 
- Lack of alerting for high risk events

**EBS**
- EBS snapshots are accessible to public
- No snapshot/ backup policy
- Large number of orphaned volumes with confidential data 

**WAF**
- CloudFront distributions lack a WAF
- WAF has inadequate policies
- WAF is not consistently in front of all incoming traffic
- WAF is not in blocking mode
- No logging/ alerting on WAF

**DDoS**
- Lack of consistent DDoS protection

**Logging**
- CloudTrail is not enabled on the account
- VPC Flow Logs are not enabled
- No sys logs from EC2
- No centralised logging
- Lack of S3 access logs
- Confidential/secrets/customer data often written to Cloudwatch during debugging

**Anti Virus**
- No AV for cloud windows instances

**Costs**
- Lack of alerting and reporting for cost control
- Incorrectly sized instances
