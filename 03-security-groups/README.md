# Finding 3: Security Group — SSH Open to the Entire Internet

## Risk

A security group acts as a firewall for EC2 instances. When SSH (port 22) is open to `0.0.0.0/0` ("Anywhere-IPv4"), it means any IP address on the internet can attempt to connect to the instance. This is one of the most commonly exploited misconfigurations in the cloud — exposed SSH ports are constantly targeted by automated brute-force login attempts. Restricting access to known IP ranges is a standard requirement across compliance frameworks, including the one used in this audit (Drata).

## What I Found

The security group `demo-unrestricted-sg` had an inbound rule allowing **SSH (port 22)** from **Source: 0.0.0.0/0** — meaning the entire internet had network-level access to attempt an SSH connection to any instance using this security group.

## What I Did

1. Navigated to **EC2 → Network & Security → Security Groups**
2. Opened the security group `demo-unrestricted-sg`
3. Clicked **Edit inbound rules**
4. Changed the **Source** for the SSH rule from `Anywhere-IPv4 (0.0.0.0/0)` to **My IP**, which restricts the rule to a single known IP address
5. Saved the updated rule

## Verification

The inbound rules table now shows the SSH rule with **Source: [specific IP]/32** instead of `0.0.0.0/0`, confirming that only one trusted IP address can attempt SSH access — not the entire internet.

## Evidence

- `before-security-group-ssh-open.png` — SSH open to 0.0.0.0/0 (entire internet)
- `after-security-group-restricted.png` — SSH restricted to a single trusted IP (/32)
