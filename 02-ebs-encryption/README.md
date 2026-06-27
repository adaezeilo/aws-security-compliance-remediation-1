# Finding 2: EBS Encryption by Default Not Enabled

## Risk

EBS volumes are the storage disks attached to EC2 instances. If encryption isn't enabled by default, any data written to those disks — including application data, logs, or database files — is stored unencrypted. If a volume or snapshot is ever exposed (shared by mistake, or accessed by someone who shouldn't have access), the data is readable in plain form. Encryption at rest is a baseline control required by most compliance frameworks (SOC 2, HIPAA, and the standard used in this audit — Drata).

## What I Found

In the account's EC2 Settings → Data protection and security, **"Always encrypt new EBS volumes"** was set to **Disabled**. This meant any new EBS volume or snapshot copy created in the account would not be encrypted by default.

## What I Did

1. Navigated to **EC2 → Settings → Data protection and security**
2. Located the **EBS encryption** section
3. Clicked **Manage**
4. Enabled **"Always encrypt new EBS volumes"**
5. Left the default encryption key as the AWS managed key `alias/aws/ebs`
6. Saved the change

## Verification

The EBS encryption section now shows **"Always encrypt new EBS volumes": Enabled** ✅. Any new EBS volume or snapshot copy created in this account/region going forward will be encrypted automatically, without relying on individual developers to remember to turn it on.

## Evidence

- `before-ebs-encryption.png` — showing "Disabled"
- `after-ebs-encryption.png` — showing "Enabled"
