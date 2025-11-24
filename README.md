# 🔐 SOC Automation Project – Mimikatz Detection & Response

## 🎯 Objective

This project demonstrates the creation of a fully automated **Security Operations Center (SOC)** workflow using:

- **SIEM:** Wazuh  
- **SIRP:** TheHive  
- **SOAR:** Shuffle  

The goal was to automatically detect, enrich, and respond to a real-world attack scenario involving **Mimikatz execution** on a Windows 11 endpoint.

The project focused on:
- Generating attack telemetry  
- Detecting it using custom SIEM rules  
- Enriching alerts via threat intelligence  
- Automating incident creation in a SOC platform  

---

## 🧠 Skills Learned

- **SIEM Configuration & Log Ingestion:**  
  Configured Wazuh to ingest Windows + Sysmon telemetry.

- **Custom Detection Engineering:**  
  Created a custom Wazuh detection rule (**Rule ID: 100002**) targeting Mimikatz execution.

- **Incident Management (SIRP):**  
  Deployed and configured TheHive using Cassandra and Elasticsearch for alert processing.

- **SOAR Automation:**  
  Designed automated workflows in Shuffle to enrich alerts with VirusTotal and forward them into TheHive.

- **Cloud & Virtualization:**  
  Deployed Windows and Linux VMs with proper networking and firewall configurations.

- **API Integrations:**  
  Integrated Wazuh, Shuffle, VirusTotal, and TheHive using webhooks and API keys.

---

## 🛠️ Tools & Technologies Used

### Virtualization & Infrastructure
- VirtualBox (Windows 11 VM)
- Ubuntu Cloud Servers

### Detection & Telemetry
- Wazuh Manager & Agent  
- Sysmon (System Monitor)

### SOC & Automation
- TheHive (SIRP)  
- Shuffle (SOAR Engine)

### Threat Intelligence
- VirusTotal API

### Back-End Services
- Apache Cassandra  
- Elasticsearch  

---

## 🧪 Project Steps & Evidence

### 🔹 Step 1: Virtual Environment Setup

**Goal:** Establish the test environment and baseline telemetry.

| Ref | Description |
|----|-------------|
| Ref 1 | Installed VirtualBox (v7.1 for stability) |
| Ref 2 | Created Windows 11 VM (8GB RAM, 80GB HDD) |
| Ref 3 | Deployed two Ubuntu cloud servers (Wazuh & TheHive) |
| Ref 4 | Installed Sysmon with Olaf Sysmon Config |
| Ref 5 | Created VM snapshot after Sysmon setup |

---

### 🔹 Step 2: Wazuh & TheHive Deployment

**Goal:** Install and configure SIEM and Case Management systems.

| Ref | Description |
|----|-------------|
| Ref 6 | Installed Wazuh Manager |
| Ref 7 | Installed Java, Cassandra, Elasticsearch |
| Ref 8 | Configured databases to bind to public IP |
| Ref 9 | Opened Port 9000 on TheHive server (UFW rule) |
| Ref 10 | Successful login to TheHive interface |
| Ref 11 | Deployed Wazuh Agent on Windows 11 |
| Ref 12 | Opened Ports 1514 & 1515 for agent communication |
| Ref 13 | Verified active agent in Wazuh |

---

### 🔹 Step 3: Custom Detection & Attack Simulation

**Goal:** Detect Mimikatz execution using custom logic.

| Ref | Description |
|----|-------------|
| Ref 14 | Modified `ossec.conf` to ingest Sysmon logs |
| Ref 15 | Verified Sysmon logs in Wazuh dashboard |
| Ref 16 | Executed Mimikatz on Windows VM |
| Ref 17 | Created Wazuh custom rule (`Rule ID: 100002`) |
| Ref 18 | Verified successful detection alert |

---

### 🔹 Step 4: SOAR Automation with Shuffle

**Goal:** Automate SOC response using workflow orchestration.

| Ref | Description |
|----|-------------|
| Ref 19 | Created a new Shuffle workflow |
| Ref 20 | Integrated Wazuh alerts with Shuffle webhook |
| Ref 21 | Extracted file hash using Regex |
| Ref 22 | Enriched hash using VirusTotal API |
| Ref 23 | Generated API key for TheHive |
| Ref 24 | Configured TheHive alert creation |
| Ref 25 | Verified automatic alert creation in TheHive |

---

## ✅ Final Result

After execution of Mimikatz on the endpoint:

✔️ Wazuh detected the attack using the custom rule  
✔️ Shuffle extracted and enriched the hash  
✔️ VirusTotal provided threat intelligence  
✔️ TheHive automatically created a SOC alert  

This confirmed a successful **end-to-end SOC automation pipeline**.

---

## 🚀 Outcome

This project demonstrates a real-world SOC workflow that combines:

- Detection Engineering  
- SIEM Event Handling  
- SOAR Automation  
- Threat Intelligence Enrichment  
- Incident Response  

It reflects how modern SOCs automate detection and response to reduce human effort and response time.

---

