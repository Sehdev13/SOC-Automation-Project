#  SOC Automation Project – Mimikatz Detection & Response

##  Objective

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



##  Skills Learned

- **SIEM Configuration & Log Ingestion:**  
  Configured Wazuh to ingest Windows + Sysmon telemetry.

- **Custom Detection Engineering:**  
  Created a custom Wazuh detection rule (**Rule ID: 100002**) targeting Mimikatz execution.

- **Incident Management (SIRP):**  
  Deployed and configured TheHive using Cassandra and Elasticsearch for alert processing.

- **SOAR Automation:**  
  Designed automated workflows in Shuffle to enrich alerts with VirusTotal and forward them into TheHive.

- **API Integrations:**  
  Integrated Wazuh, Shuffle, VirusTotal, and TheHive using webhooks and API keys.



##  Tools & Technologies Used

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



##  Project Steps & Evidence


###  Step 1: Virtual Environment Setup

1. Installed **VirtualBox v7.1** for stable virtualization.

2. Created a **Windows 11 VM**:
   - 8 GB RAM  
   - 80 GB Storage  
   - Endpoint system for generating security telemetry.

3. Deployed two **Ubuntu cloud servers**:
   - Server 1: Wazuh Manager  
   - Server 2: TheHive Server  

4. Installed **Sysmon** on Windows using the Olaf configuration file.

5. Took a clean system **snapshot** after Sysmon installation.



###  Step 2: Wazuh & TheHive Deployment

1. Installed **Wazuh Manager** using the official quick-start script.

2. Installed required TheHive dependencies:
   - Java  
   - Apache Cassandra  
   - Elasticsearch  

3. Updated Cassandra and Elasticsearch configs:
   - Modified `listen_address`
   - Modified `rpc_address`
   - Modified `network.host`
   - Set all to server public IP instead of localhost.

4. Opened TheHive port:
   ```bash
   ufw allow 9000

5. Successfully logged into TheHive web UI.

6. Deployed Wazuh Agent on Windows 11.

7. Opened Wazuh Manager ports:
   ```bash
   ufw allow 1514
   ufw allow 1515

8. Verified Windows 11 agent appeared as Active in Wazuh dashboard.



 ### Step 3: Custom Detection & Attack Simulation
 
1. Modified ossec.conf on Windows agent to ingest:
   ```bash 
   Microsoft-Windows-Sysmon/Operational
   
2. Verified Sysmon logs were ingested successfully inside the Wazuh dashboard.

3. Executed Mimikatz on Windows 11 VM.

4. Created a custom Wazuh detection rule (local_rules.xml):
   ```xml
   <rule id="100002" level="15">
   <if_group>sysmon_event1</if_group>
   <field name="win.eventdata.originalFileName">mimikatz.exe</field>
   <description>Mimikatz Execution Detected</description>
   </rule>

5. Confirmed alert generation in Wazuh after attack execution.


### Step 4: SOAR Automation using Shuffle

1 Created a new workflow in **Shuffle** and generated a Webhook URL.

2 Configured **Wazuh** to send alerts with **Rule ID: 100002** to Shuffle.

3 Built a **Regex extraction tool** inside Shuffle:

  - Extracts the **SHA-256 hash** from Wazuh alert data.
    
4 Integrated **VirusTotal API** for automated threat intelligence enrichment.

5 Generated an **API key in TheHive** for the automation service account.

6 Connected **Shuffle with TheHive API**.

7 Enabled automatic alert creation in TheHive using enriched data.



##  Final Result

https://github.com/user-attachments/assets/1445fbae-4f92-449b-9217-ec0b848c3e89


After execution of Mimikatz on the endpoint:

- Wazuh detected the attack using the custom rule  
- Shuffle extracted and enriched the hash  
- VirusTotal provided threat intelligence  
- TheHive automatically created a SOC alert  

This confirmed a successful **end-to-end SOC automation pipeline**.


##  Outcome

This project demonstrates a real-world SOC workflow that combines:

- Detection Engineering  
- SIEM Event Handling  
- SOAR Automation  
- Threat Intelligence Enrichment  
- Incident Response  

It reflects how modern SOCs automate detection and response to reduce human effort and response time.



