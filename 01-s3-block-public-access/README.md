
## Finding 1: S3 Bucket — Block Public Access Not Enabled
Risk
An S3 bucket without Block Public Access enabled can be exposed to the internet if a bucket policy or ACL is misconfigured even by accident. This is one of the most common causes of real-world data leaks, which is why it's a standard check in compliance frameworks like the one used in this audit (Drata).
What I Found
The bucket precious-demo-compliance-bucket was created with all four Block Public Access settings turned off, meaning public access through ACLs or bucket policies was possible if applied.

## What I Did

Navigated to the bucket → Permissions tab
Opened Block public access (bucket settings) → clicked Edit
Enabled Block all public access (which covers all 4 underlying settings: new ACLs, all ACLs, new bucket policies, and all bucket policies)
Saved and confirmed the change

## Verification
The Permissions tab now shows Block all public access: On, confirming the bucket and its objects can no longer be exposed publicly through ACLs or policies.

## Evidence:

before-block-public-access.png — settings unchecked during bucket creation

after-block-public-access.png — Block all public access showing "On"


