# Finding 5: IMDSv2 Not Enforced

## Risk

EC2's Instance Metadata Service (IMDS) allows an instance to retrieve information about itself, including temporary IAM credentials. The original version, IMDSv1, is vulnerable to Server-Side Request Forgery (SSRF) attacks — if an attacker can trick an application running on the instance into making an internal request, they may be able to retrieve the instance's IAM credentials without direct access to the operating system. IMDSv2 closes this gap by requiring a session token (obtained via a PUT request) before any metadata can be read, blocking that attack path entirely. This is a well-known, high-severity finding in cloud security — it was the root cause of a major real-world breach in 2019 — and is a standard check in compliance frameworks including the one used in this audit (Drata).

## What I Found

The EC2 instance `i-028585a2cc20a8c2a` had its **IMDSv2** setting configured as **Optional**, meaning both the older, vulnerable IMDSv1 and the more secure IMDSv2 were accepted — leaving the SSRF attack path open.

## What I Did

1. Selected the instance → **Actions → Instance settings → Modify instance metadata options**
2. Changed **IMDSv2** from **Optional** to **Required**
3. Saved the change

## Verification

The instance metadata options now show **IMDSv2: Required**, confirming that only session-token-based requests (IMDSv2) are accepted, and the legacy IMDSv1 method is no longer usable on this instance.

## Evidence

- `before-imdsv2-optional.png` — IMDSv2 set to Optional
- `after-imdsv2-required.png` — IMDSv2 set to Required
