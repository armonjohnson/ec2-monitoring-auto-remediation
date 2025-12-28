EC2 Proactive Monitoring & Auto-Remediation on AWS
BUILD Format Project README
B — Background

Modern cloud environments require continuous monitoring, rapid detection, and automated remediation to maintain reliability and security.

Manually logging into servers after an issue occurs does not scale and increases recovery time. This project was built to simulate a real-world AWS production environment where infrastructure issues are detected and handled automatically using native AWS services.

The focus is not application code, but infrastructure observability, automation, and incident response.

U — Understanding the Problem

This project addresses common operational challenges faced by Cloud Support and DevOps engineers:

How do you detect EC2 performance issues early?

How do you automatically respond to high CPU usage?

How do you remediate issues without SSH access?

How do you validate alarms actually fire?

How do you surface security findings in real time?

The goal was to build an event-driven monitoring and auto-remediation workflow using AWS-managed services.

I — Implementation
1️⃣ EC2 Environment

Two EC2 instances were launched to simulate separate environments:

Dev-Server

Prod-Server

Both instances are running and actively monitored in the us-east-1 region.

What your EC2 screenshot proves

Multiple environments exist (not a single test box)

Instances are running and reachable

Monitoring is applied at the instance level

This mirrors real Dev / Prod separation

2️⃣ CloudWatch CPU Alarm Configuration

A CloudWatch alarm was configured on the Dev EC2 instance using the following settings:

Metric: CPUUtilization

Namespace: AWS/EC2

Statistic: Average

Period: 1 minute

Threshold: ≥ 85%

Evaluation: 1 datapoint

What your CloudWatch alarm setup screenshot proves

You understand EC2 metrics

You selected realistic production thresholds

Short evaluation periods enable fast detection

Alarm configuration was done manually (not auto-generated)

3️⃣ Alarm Triggered — High CPU Detected

The CloudWatch alarm entered the IN ALARM state after CPU usage exceeded the defined threshold.

What the alarm graph screenshot proves

CPU was intentionally stressed

Alarm logic works end-to-end

Monitoring was validated, not assumed

This is real signal, not hypothetical configuration

4️⃣ Automated Remediation with AWS Lambda

When the alarm fired:

CloudWatch published the alarm to SNS

SNS triggered a Lambda function

Lambda parsed the SNS message

The EC2 Instance ID was extracted from alarm dimensions

Remediation logic executed automatically

The Lambda function was written in Python and includes logic to:

Handle CloudWatch alarm payloads

Parse EC2 Instance IDs

Support multiple metric dimension formats

Log events for debugging and traceability

What your Lambda code screenshot proves

You understand event-driven automation

You can parse CloudWatch + SNS payloads

You handled real-world alarm formats

This is operational automation, not a toy script

5️⃣ Security Detection with Amazon GuardDuty

Amazon GuardDuty detected outbound port scanning activity originating from the monitored EC2 instance.

Finding details:

Type: Recon:EC2/Portscan

Severity: Medium

Resource: EC2 instance

Region: us-east-1

What your GuardDuty screenshot proves

Security monitoring is enabled

Findings are real, not simulated

You understand that performance issues and security events are related

This reflects real SOC / cloud security workflows

L — Learning & Outcomes
Skills Demonstrated

✅ EC2 monitoring with CloudWatch

✅ Alarm-based alerting with real thresholds

✅ Event-driven automation using SNS + Lambda

✅ Parsing CloudWatch alarm payloads

✅ IAM-aware remediation logic

✅ Real-time security detection with GuardDuty

✅ Validation through triggered alarms and findings

Key Takeaways

Monitoring without automation is incomplete

Alarms must be tested, not just configured

Event-driven remediation reduces MTTR

Security findings are part of infrastructure reliability

AWS-native tools can fully automate incident response

Why This Project Matters

This project demonstrates real cloud engineering practices, not just configuration knowledge.

It aligns directly with responsibilities of:

Cloud Support Engineer

DevOps Engineer

AWS Solutions Architect

It proves hands-on experience with monitoring, automation, remediation, and security visibility in AWS.

Author

Armon Johnson
Cloud / DevOps Engineer in Progress ☁️🚀

⭐ If you found this project useful, feel free to star the repository.
