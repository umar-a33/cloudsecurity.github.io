---
layout: default
---

# Cloud Security Hub

A practical reference for securing cloud infrastructure — covering AWS, Azure, and GCP environments.

---

## Core Topics

### Identity & Access Management (IAM)

Misconfigured IAM is the leading cause of cloud breaches. Key principles:

- **Least privilege** — grant only the permissions required for the task
- **Avoid long-lived credentials** — use roles and temporary tokens (STS, Workload Identity)
- **Enforce MFA** — especially on root/admin accounts
- **Audit regularly** — use IAM Access Analyzer (AWS), IAM Recommender (GCP), or Access Reviews (Azure)

```bash
# AWS: find overly permissive policies attached to a user
aws iam list-attached-user-policies --user-name <username>
aws iam simulate-principal-policy --policy-source-arn <arn> --action-names "*"
```

---

### Network Security

- **Never expose management ports** (22, 3389) to `0.0.0.0/0`
- Use **VPC/VNet segmentation** — separate tiers (web, app, data) into distinct subnets
- Enable **VPC Flow Logs** / **NSG Flow Logs** for traffic visibility
- Use **private endpoints** for cloud services instead of public internet routes
- Apply **Web Application Firewalls (WAF)** in front of public-facing apps

---

### Data Protection

| Layer | Recommendation |
|:------|:---------------|
| At rest | Enable default encryption on all storage (S3, GCS, Azure Blob) |
| In transit | Enforce TLS 1.2+ everywhere; disable older protocols |
| Key management | Use managed KMS (AWS KMS, Cloud KMS, Azure Key Vault); rotate keys annually |
| Secrets | Never hardcode credentials — use Secrets Manager, Parameter Store, or Vault |

---

### Threat Detection & Monitoring

Enable native cloud threat detection services:

- **AWS** — GuardDuty, Security Hub, CloudTrail
- **GCP** — Security Command Center, Cloud Audit Logs
- **Azure** — Microsoft Defender for Cloud, Azure Monitor

Set up alerts for:
- Root/admin logins
- IAM policy changes
- S3/Blob public access changes
- Unusual API call volumes or new regions

---

### Secure Configuration (Hardening)

- Disable unused services and APIs
- Enable **CloudTrail / Audit Logs** in all regions
- Block public access at the account/org level for object storage
- Use **Organization Policies** (GCP) or **Service Control Policies** (AWS) to enforce guardrails org-wide
- Run periodic CIS Benchmark assessments

```bash
# AWS: check if S3 block public access is enabled at account level
aws s3control get-public-access-block --account-id <account-id>
```

---

## Quick Reference: Common Misconfigurations

| Misconfiguration | Risk | Fix |
|:-----------------|:-----|:----|
| Public S3 bucket | Data exposure | Enable Block Public Access |
| Unused IAM access keys | Account takeover | Rotate or delete keys > 90 days |
| Open security group (0.0.0.0/0) | Unauthorized access | Restrict to known CIDRs |
| No MFA on root account | Full account compromise | Enforce MFA immediately |
| Unencrypted EBS/disk | Data exposure | Enable encryption at rest |
| Logging disabled | No incident visibility | Enable CloudTrail/Audit Logs |

---

## Useful Tools

- [**Prowler**](https://github.com/prowler-cloud/prowler) — AWS/GCP/Azure security auditing CLI
- [**ScoutSuite**](https://github.com/nccgroup/ScoutSuite) — multi-cloud security auditing
- [**Trivy**](https://github.com/aquasecurity/trivy) — container and IaC vulnerability scanning
- [**Checkov**](https://github.com/bridgecrewio/checkov) — static analysis for Terraform, CloudFormation, Kubernetes

---

*Built for defenders. Contributions welcome.*
