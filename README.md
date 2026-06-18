
# 🔐 Azure Sentinel Threat Monitoring & Detection Lab

## 📌 Project Overview

This project demonstrates the deployment of a cloud-based Security Operations Centre (SOC) using **Microsoft Azure** and **Microsoft Sentinel**.

The lab simulates a real-world security monitoring environment capable of:
- Collecting and analysing security logs
- Detecting malicious activity (e.g., brute-force attacks)
- Investigating incidents
- Visualising security insights using dashboards and workbooks

---

## 🏗️ Architecture & Implementation Workflow

The following diagram illustrates the end-to-end data flow and implementation workflow of the lab:

![Architecture Diagram](images/architecture-diagram.png)

### 🔄 Workflow Summary
---

## 🎯 Project Objectives

- Deploy an Azure Virtual Machine  
- Configure Log Analytics Workspace  
- Integrate Microsoft Sentinel  
- Collect Windows Security Events  
- Monitor RDP and SSH activity  
- Detect brute-force attacks  
- Perform threat hunting using KQL  
- Create analytics rules for automated detection  
- Investigate security incidents  
- Build dashboards and visualisations  

---

## 🧰 Technologies Used

| Technology | Purpose |
|----------|--------|
| Azure Virtual Machine | Target system for attack simulation |
| Log Analytics Workspace | Centralised log collection |
| Microsoft Sentinel | SIEM platform |
| Azure Monitor Agent | Telemetry/data collection |
| KQL (Kusto Query Language) | Threat hunting & analysis |
| Workbooks | Data visualisation |
| Analytics Rules | Detection & alerting |

---

## ⚙️ Lab Implementation

### ✅ Step 1 – Azure VM Deployment

- Deployed a **Windows Server VM** exposed to the internet  
- Enabled:
  - RDP (Port 3389)
  - SSH (Port 22)

**Purpose:**
- Simulate real-world attack surface  
- Attract brute-force login attempts  

📷 `images/azure-vm.png`

---

### ✅ Step 2 – Log Analytics Workspace

- Created a centralised **Log Analytics Workspace**
- Collected:
  - SecurityEvent logs  
  - Authentication logs  
  - System telemetry  

📷 `images/log-analytics-workspace.png`

---

### ✅ Step 3 – Microsoft Sentinel Setup

- Connected Sentinel to the workspace  
- Enabled:
  - Threat detection  
  - Threat hunting  
  - Incident management  

📷 `images/sentinel-setup.png`

---

### ✅ Step 4 – Data Collection Configuration

- Configured **Azure Monitor Agent (AMA)**  
- Collected:
  - Failed login attempts  
  - Successful logins  
  - Authentication events  

📷 `images/data-collection.png`

---

## 🔍 Threat Hunting (KQL)

### 🔸 Failed Login Detection
```kql
SecurityEvent
| where EventID == 4625
| summarize Count = count() by IpAddress
| order by Count desc

✅ Identifies brute-force attempts

🔸 Successful Login Detection
KQLSecurityEvent| where EventID == 4624Show more lines
✅ Tracks successful authentications

🔸 Top Attacking IPs
KQLSecurityEvent| where EventID == 4625| summarize Attempts = count() by IpAddress| order by Attempts descShow more lines
✅ Highlights suspicious source IPs

🚨 Detection Rules
🔹 RDP Brute Force Detection

Multiple failed login attempts
Same IP within short timeframe

📷 images/rdp-alert-rule.png

🔹 SSH Brute Force Detection

Repeated login failures
High-frequency attempts from same source

📷 images/ssh-alert-rule.png

🧪 Incident Investigation
During monitoring, multiple suspicious activities were observed:
🔍 Observed Activity

RDP brute-force attempts
SSH login attempts
Password spraying attacks
Internet-wide scanning behaviour

🛠️ Investigation Tools

Microsoft Sentinel Incidents
SecurityEvent logs
KQL queries

📷 images/incidents/

📊 Dashboard & Visualisation
A Sentinel Workbook was created to visualise:

Failed logons
Successful logons
Top attacking IPs
Authentication trends
Incident counts

📷 images/workbook-dashboard.png

📌 Key Findings

Public-facing systems are scanned almost immediately
RDP and SSH are primary attack targets
Microsoft Sentinel provides centralised visibility
KQL enables rapid threat investigation
Analytics rules automate detection effectively


🧠 Skills Demonstrated

Cloud Security Monitoring
SIEM Deployment (Microsoft Sentinel)
Threat Hunting & Detection Engineering
Incident Investigation
KQL Query Development
Azure Administration
Security Analytics
SOC Operations


🚀 Future Improvements

Integrate Threat Intelligence feeds
Automate response using Playbooks (SOAR)
Deploy honeypots for advanced attack simulation
Implement UEBA (User Entity Behaviour Analytics)
Integrate Microsoft Defender for Endpoint


📁 Repository Structure
Azure-Sentinel-Threat-Monitoring-Lab/
│
├── images/
│   ├── architecture-diagram.png
│   ├── azure-vm.png
│   ├── log-analytics-workspace.png
│   ├── sentinel-setup.png
│   ├── data-collection.png
│   ├── rdp-alert-rule.png
│   ├── ssh-alert-rule.png
│   ├── workbook-dashboard.png
│   └── incidents/
│
├── kql/
│   ├── failed-logons.kql
│   ├── successful-logons.kql
│   └── bruteforce-detection.kql
│
└── README.md


🔗 Project Value
This project demonstrates the practical implementation of a cloud-native SIEM solution, covering:

End-to-end log ingestion
Real-time threat detection
Incident management workflows
Security data visualisation


⭐ Author
Simon Yusuf Enoch
