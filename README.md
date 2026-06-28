# AWS Security Compliance Remediation

Hands-on remediation of real AWS security compliance findings — across S3, EBS, EC2 networking, VPC, and instance metadata. Each finding follows the same structure: the risk, what was found, what was done to fix it, and verification with evidence.

These findings mirror real compliance checks (modeled on the Drata framework) commonly required for SOC 2 and similar audits. All fixes were performed and documented in a personal AWS free-tier account.

## Findings

| # | Finding | Risk Area | Status |
|---|---------|-----------|--------|
| 1 | [S3 Block Public Access](./01-s3-block-public-access) | Data exposure | Remediated |
| 2 | [EBS Encryption by Default](./02-ebs-encryption) | Encryption at rest | Remediated |
| 3 | [Security Group — SSH Open to Internet](./03-security-groups) | Network access control | Remediated |
| 4 | [VPC Flow Logs](./04-vpc-flow-logs) | Network visibility / audit trail | Remediated |
| 5 | [IMDSv2 Enforcement](./05-imdsv2-enforcement) | SSRF / credential exposure | Remediated |

## Approach

For each finding, the documentation follows a consistent format:

- **Risk** — why the misconfiguration matters
- **What I Found** — the specific issue identified
- **What I Did** — the exact steps taken to remediate it
- **Verification** — how the fix was confirmed, with screenshot evidence

## Tools & Services Covered

`Amazon S3` · `Amazon EBS` · `Amazon EC2` · `Amazon VPC` · `IAM` · `CloudWatch Logs`

## Why This Repo Exists

Compliance remediation is a core part of day-to-day cloud security work — closing findings from tools like Drata, AWS Security Hub, or similar audit frameworks. This repo demonstrates that process end-to-end: identifying a misconfiguration, understanding its risk, applying the fix through the AWS Console, and verifying the result.
