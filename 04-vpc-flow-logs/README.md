# Finding 4: VPC Flow Logs Not Enabled

## Risk

VPC Flow Logs capture metadata about network traffic flowing in and out of a VPC — including source/destination IP, ports, and whether the traffic was accepted or rejected. Without flow logs enabled, there is no visibility into network activity. In the event of a security incident — such as unusual outbound traffic, a port scan, or a compromised instance communicating with an unexpected destination — there would be no record to investigate. Flow logs are a baseline requirement across most compliance frameworks, including the one used in this audit (Drata), because they provide the network-level audit trail needed for incident response.

## What I Found

The VPC `vpc-09c0ef19050979f22` had no flow logs configured, meaning no record of network traffic in or out of the VPC was being captured.

## What I Did

1. Navigated to **VPC → Your VPCs**, selected the VPC, and opened the **Flow logs** tab
2. Clicked **Create flow log**
3. Set **Filter** to **All** (captures both accepted and rejected traffic, which gives the most complete picture for security review)
4. Set **Destination** to **Send to CloudWatch Logs**
5. Created a new destination log group: `vpc/flowlogs-demo`
6. Selected **Create and use a new service role**, allowing AWS to automatically generate an IAM role with the correct permissions to publish logs to CloudWatch
7. Created the flow log

## Verification

The Flow Logs tab now shows one flow log with **State: Active**,  **Destination Type: cloud-watch-logs**, and **Traffic Type: All**, confirming network traffic for this VPC is now being logged and available for review in CloudWatch.

## Evidence

- `before-vpc-flow-log-empty.png` — no flow logs configured
- `after-vpc-flow-log-active.png` — flow log created and Active
