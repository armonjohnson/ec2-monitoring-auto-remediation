**EC2 Proactive Monitoring & Auto-Remediation on AWS**


**B — Background**

Modern cloud environments require continuous monitoring, rapid detection, and automated remediation to maintain reliability and security.

Manually logging into servers after an issue occurs does not scale and increases recovery time. This project was built to simulate a real-world AWS production environment where infrastructure issues are detected and handled automatically using native AWS services.

The focus of this project is not application code, but infrastructure observability, automation, and incident response.

**U — Understanding the Problem**

This project addresses common operational challenges faced by Cloud Support and DevOps engineers:

How do you detect EC2 performance issues early?

How do you automatically respond to high CPU usage?

How do you remediate issues without SSH access?

How do you validate alarms actually fire?

How do you surface security findings in real time?

The goal was to build an event-driven monitoring and auto-remediation workflow using AWS-managed services.

**I — Implementation**
1️⃣ EC2 Environment

Two EC2 instances were launched to simulate separate environments:

Dev-Server

Prod-Server

Both instances are running and actively monitored in the us-east-1 region.

What this proves

Multiple environments (not a single test instance)

Realistic Dev / Prod separation

Instance-level monitoring enabled

Mirrors real production architecture

2️⃣ **CloudWatch CPU Alarm Configuration**

A CloudWatch alarm was configured on the Dev EC2 instance with the following settings:

Metric: CPUUtilization

Namespace: AWS/EC2

Statistic: Average

Period: 1 minute

Threshold: ≥ 85%

Evaluation: 1 datapoint

What this proves

Proper metric selection

Realistic alert thresholds

Fast detection configuration

Manual alarm setup (not default)

3️⃣ **Alarm Triggered — High CPU Detected**

The CloudWatch alarm successfully transitioned to the IN ALARM state after CPU usage exceeded the threshold.

What this proves

CPU was intentionally stressed

Alarm logic works end-to-end

Monitoring was validated, not assumed

This is real operational data

4️⃣ **Automated Remediation with AWS Lambda**

When the alarm fired:

CloudWatch published the alarm to SNS

SNS triggered a Lambda function

Lambda parsed the alarm payload

EC2 Instance ID was extracted

Remediation logic executed automatically

The Lambda function (Python) handles:

SNS event parsing

CloudWatch alarm formats

EC2 dimension extraction

Debug logging for traceability

What this proves

Event-driven automation knowledge

Real alarm payload handling

Production-style remediation logic

No manual SSH intervention required

5️⃣ **Security Detection with Amazon GuardDuty**

Amazon GuardDuty detected outbound port scanning activity from the EC2 instance.

Finding details

Type: Recon:EC2/Portscan

Severity: Medium

Region: us-east-1

What this proves

Security monitoring enabled

Findings are real, not simulated

Awareness of infrastructure security risks

Alignment with SOC / cloud security workflows

L — **Learning & Outcomes
Skills Demonstrated**

✅ EC2 monitoring with CloudWatch

✅ Alarm-based alerting

✅ SNS-driven automation

✅ Lambda auto-remediation

✅ Parsing CloudWatch alarm payloads

✅ IAM-aware automation

✅ Security visibility with GuardDuty

Key Takeaways

Monitoring alone is not enough

Alarms must be tested, not just configured

Automation reduces recovery time

Performance and security are connected

AWS-native tools can fully automate response workflows

Why This Project Matters

This project demonstrates real production cloud engineering practices, not just configuration.

It directly aligns with roles such as:

Cloud Support Engineer

DevOps Engineer

AWS Solutions Architect

It proves hands-on experience with monitoring, automation, remediation, and security detection in AWS.

Author

Armon Johnson
Cloud / DevOps Engineer in Progress ☁️🚀

⭐ If you found this project useful, feel free to star the repository!
