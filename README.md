
# 🛡️ Project: Microsoft Sentinel SIEM Integration with AWS & CrowdStrike

## 📘 Scenario
A fast-growing tech startup is expanding its cloud infrastructure and endpoint security. They use **AWS** for cloud services and **CrowdStrike Falcon** for endpoint detection and response (EDR). To centralize security monitoring and improve threat detection, they want to integrate these data sources into **Microsoft Sentinel**, their chosen SIEM platform.

You are hired as a **SIEM Integration Expert** to:
- Connect AWS GuardDuty and CloudWatch to Sentinel.
- Ingest CrowdStrike Falcon logs.
- Normalize and validate log data.
- Create high-fidelity detection rules and dashboards.
- Recommend best practices for ongoing monitoring.

## 🎯 Objectives
1. Establish secure and reliable data ingestion from AWS and CrowdStrike into Microsoft Sentinel.
2. Normalize and validate logs to ensure consistent schema and usable data.
3. Develop detection rules using KQL to identify suspicious activity.
4. Build dashboards for visibility into cloud and endpoint threats.
5. Document and recommend best practices for SIEM maintenance.

## 🧰 Prerequisites
### Technical Skills
- Familiarity with Microsoft Sentinel, Azure Monitor, and Log Analytics
- Experience with AWS services (GuardDuty, CloudWatch)
- Understanding of CrowdStrike Falcon API/Data Replicator
- Proficiency in KQL (Kusto Query Language)
- Basic scripting knowledge (PowerShell, Python, or Azure Functions)

### Accounts & Access
- Azure subscription with permissions to create Sentinel resources
- AWS account with GuardDuty and CloudWatch enabled
- CrowdStrike Falcon API credentials (client ID and secret)

### Architecture Diagram
<img width="1024" height="1024" alt="Designer" src="https://github.com/user-attachments/assets/0b365b08-4d3a-4491-8531-3c09c1361afd" />

## 🧠 Key Concepts Explained
- **SIEM**: Security Information and Event Management platform for centralized log analysis.
- **Microsoft Sentinel**: Cloud-native SIEM on Azure using Log Analytics and KQL.
- **AWS GuardDuty**: Threat detection service for AWS environments.
- **AWS CloudWatch**: Monitoring service for AWS resources and applications.
- **CrowdStrike Falcon**: Endpoint detection and response platform.
- **KQL**: Query language used in Azure Monitor and Sentinel.

## 🧪 Step-by-Step Implementation
### 🔹 Phase 1: Microsoft Sentinel Setup
1. Create a Log Analytics Workspace.
2. Enable Microsoft Sentinel.
3. Configure retention policies and access controls.

### 🔹 Phase 2: AWS GuardDuty Integration
1. Enable GuardDuty in AWS.
2. Use Sentinel AWS Connector.
3. Create IAM Role with trust policy for Azure.
4. Configure connector and validate ingestion.
5. Sample KQL:
```kql
AWSGuardDutyFindings_CL
| summarize count() by Severity, Region
```

### 🔹 Phase 3: AWS CloudWatch Integration
1. Identify CloudWatch log groups.
2. Stream logs to Kinesis Firehose or S3.
3. Use Azure Logic Apps or Event Hub to ingest logs.
4. Normalize logs using custom parsers.
```kql
CloudWatchLogs_CL
| extend SourceIP = extract("src=(\d+\.\d+\.\d+\.\d+)", 1, RawData)
```

### 🔹 Phase 4: CrowdStrike Falcon Integration
1. Create API client in Falcon Console.
2. Use Azure Function or Logstash to pull logs.
3. Push logs to Sentinel via HTTP Data Collector API.
4. Validate ingestion:
```kql
CrowdStrikeDetections_CL
| summarize count() by Tactic, Technique
```

### 🔹 Phase 5: Detection Engineering
1. Create Analytics Rules in Sentinel.
2. Tune rules to reduce noise.
```kql
| where AccountName !in ("admin", "service_account")
```
3. Map entities for incident correlation.

### 🔹 Phase 6: Dashboards & Visualization
1. Import or build Workbooks.
2. Visualize:
   - Top GuardDuty findings
   - CrowdStrike detections by severity
   - CloudWatch anomalies

### 🔹 Phase 7: Maintenance & Best Practices
1. Set up connector health alerts.
2. Implement alert suppression and incident grouping.
3. Document integration steps and update monthly.

## 📦 Final Deliverables
| Item | Description |
|------|-------------|
| ✅ AWS GuardDuty Connector | Fully configured and validated |
| ✅ AWS CloudWatch Logs | Ingested and normalized |
| ✅ CrowdStrike Falcon Logs | Ingested via API |
| ✅ Detection Rules | 5+ tuned KQL rules |
| ✅ Dashboards | 2+ custom workbooks |
| ✅ Documentation | Setup guide, tuning notes, maintenance checklist |

## 🔗 Useful Links
- [Microsoft Sentinel Documentation](https://learn.microsoft.com/en-us/azure/sentinel/)
- [AWS GuardDuty Documentation](https://docs.aws.amazon.com/guardduty/latest/ug/what-is-guardduty.html)
- [AWS CloudWatch Documentation](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)
- [CrowdStrike Falcon API Docs](https://www.crowdstrike.com/resources/community-tools/falconpy/)
- [KQL Language Reference](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/)
