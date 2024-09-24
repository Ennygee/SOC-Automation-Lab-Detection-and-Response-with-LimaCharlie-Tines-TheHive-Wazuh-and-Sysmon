# SOC Automation Lab: Detection and Response with LimaCharlie, Tines, TheHive, Wazuh, and Sysmon

## Overview
This SOC automation lab integrates LimaCharlie (EDR), Tines (SOAR), TheHive (case management), Wazuh (security monitoring), and Sysmon to build a functional SOC environment. The lab focuses on detecting security events, generating telemetry, and automating incident responses while managing cases effectively.

## Objective
The goal of this project is to create a fully automated SOC environment that detects security threats using Wazuh and Sysmon, automates responses via Tines and LimaCharlie, and manages incidents through TheHive. The final step is to automate machine isolation using a user-confirmed decision flow through Tines, notifying stakeholders via Slack and email.

## Skills Learned
- Automating security workflows with Tines.
- Configuring endpoint detection with LimaCharlie and Sysmon.
- Integrating incident management using TheHive.
- Automating decision-based actions like machine isolation using SOAR.
- Monitoring security events using Wazuh.
- Real-time communication through Slack and Email notifications.

## Tools Used
- **LimaCharlie**: EDR tool for detecting and monitoring threats.
- **Tines**: SOAR platform for automating incident response workflows.
- **TheHive**: Case management system for tracking and managing security incidents.
- **Wazuh**: Security monitoring platform for ingesting logs and detecting security events.
- **Sysmon**: Advanced logging tool for Windows event monitoring.
- **Draw.io**: Used for designing workflows and playbooks.
- **Slack**: Real-time messaging platform for notifying SOC teams.
- **Email**: For sending email notifications.
- **SquareX**: Temporary email generator for secure email use.

## Steps and Screenshots

### Step 1: Designing the Playbook Workflow
Use Draw.io to create a workflow that integrates LimaCharlie, Tines, Wazuh, and TheHive. The workflow includes detection, notifications, and automated responses such as machine isolation.

**Ref 1: Workflow Design in Draw.io**  
![Workflow Design](path/to/screenshot1.png)

*Explanation*: A visual diagram showing the complete SOC workflow integration, including detection, response, and case management.

---

### Step 2: Configuring TheHive
Set up Cassandra and Elasticsearch for TheHive to manage and query data. Ensure that TheHive's public IP is correctly configured, and enable Cortex and MISP for cyber threat intelligence enrichment.

**Ref 2: TheHive Configuration**  
![TheHive Configuration](path/to/screenshot2.png)

*Explanation*: Screenshot showing the configuration of Cassandra and Elasticsearch for TheHive.

---

### Step 3: Configuring Wazuh
Log into the Wazuh dashboard and configure the server’s public IP. Set up a Windows agent for monitoring endpoint telemetry. Generate the agent command, run it via PowerShell on the Windows machine, and verify agent connectivity in the Wazuh dashboard.

**Ref 3: Wazuh Agent Setup**  
![Wazuh Agent Setup](path/to/screenshot3.png)

*Explanation*: Screenshot of the Wazuh agent installation on a Windows machine and verifying connectivity in the Wazuh dashboard.

---

### Step 4: Setting up Sysmon and Generating Telemetry
Install Sysmon on the Windows 10 machine and configure it to log key events such as process creation (event ID 1). Update Wazuh's configuration file to ingest Sysmon logs by specifying the correct event log channel.

**Ref 4: Sysmon Configuration**  
![Sysmon Configuration](path/to/screenshot4.png)

*Explanation*: Screenshot showing the configuration of Sysmon on the Windows machine and the Wazuh config file update.

---

### Step 5: Testing with Mimikatz
Disable Windows Defender to avoid interference and download Mimikatz. Execute Mimikatz from the Windows machine using PowerShell to generate telemetry for analysis in Wazuh.

**Ref 5: Mimikatz Execution**  
![Mimikatz Execution](path/to/screenshot5.png)

*Explanation*: Screenshot showing Mimikatz being run on the Windows machine, generating security events for telemetry collection.

---

### Step 6: Monitoring Sysmon Events in Wazuh
Query the Wazuh dashboard to find Sysmon events related to Mimikatz activity. If necessary, modify the ossec.conf file to enable full logging of Sysmon events.

**Ref 6: Sysmon Logs in Wazuh**  
![Sysmon Logs](path/to/screenshot6.png)

*Explanation*: Screenshot showing Sysmon events related to Mimikatz in the Wazuh dashboard.

---

### Step 7: Creating a Custom Alert for Mimikatz in Wazuh
Write a custom detection rule in Wazuh to trigger alerts for Mimikatz activity by identifying the original file name. Set the alert severity to 15 (the highest) and test by renaming the Mimikatz executable.

**Ref 7: Custom Alert Creation**  
![Custom Alert Creation](path/to/screenshot7.png)

*Explanation*: Screenshot of the custom rule in Wazuh that triggers an alert for Mimikatz activity, even after renaming the executable.

---

### Step 8: Integration of Tines with Slack and Email
Configure Tines to send an alert to Slack and Email when a detection occurs. Use SquareX to generate a secure email address for testing. Both notifications include key details like computer name, IP address, and detection time.

**Ref 8: Notification Setup**  
![Tines Notification](path/to/screenshot8.png)

*Explanation*: Screenshot showing the Slack and email notification setup in Tines, complete with detection details.

---

### Step 9: User Prompt for Machine Isolation
Set up a user decision prompt in Tines to ask whether to isolate the compromised machine. Based on the user’s response, either initiate machine isolation or send a Slack message advising further investigation.

**Ref 9: User Decision Prompt**  
![User Decision Prompt](path/to/screenshot9.png)

*Explanation*: Screenshot showing the decision-making interface in Tines with options for machine isolation.

---

### Step 10: Machine Isolation with LimaCharlie
If the user selects "yes," LimaCharlie isolates the machine by disconnecting it from the network. Tines retrieves the isolation status and sends a confirmation message to Slack.

**Ref 10: Machine Isolation in LimaCharlie**  
![Machine Isolation](path/to/screenshot10.png)

*Explanation*: Screenshot showing LimaCharlie’s API request to isolate the machine, and the confirmation message in Slack.

---

## Challenges and Solutions
- **Slack and Email Integration**: Establishing the necessary credentials and permissions to link Tines with Slack and Email.
- **Machine Isolation**: Configuring LimaCharlie to correctly isolate machines based on user input, and testing the isolation process.

---

## Results
- Successfully automated machine isolation using LimaCharlie and Tines, based on real-time decisions.
- Integrated Slack and Email for immediate notifications of security events.
- Created a decision-based workflow that enabled SOC analysts to approve machine isolation.

---

## Learning Outcomes
- Developed proficiency in building SOC automation workflows using Tines and LimaCharlie.
- Gained hands-on experience with automated incident response based on detection data.
- Improved skills in configuring and integrating multiple SOC tools for seamless security operations.

---

## Next Steps
- Further automate the incident management process in TheHive by creating more detailed playbooks.
- Expand the integration with Slack for more advanced alerts and monitoring.
- Experiment with additional detection rules and telemetry to identify more sophisticated attacks.

