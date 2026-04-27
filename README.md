**Azure SIEM Honeypot Lab**

Overview

Deployed a cloud-based honeypot in Microsoft Azure to capture and analyze real-world attack traffic using Microsoft Defender and KQL.

**Technologies**

Microsoft Azure

Microsoft Defender (SIEM)

Log Analytics Workspace

KQL (Kusto Query Language)

Windows Event Logs


**1. Initial Setup**
Created resource group, virtual network, and VM.

![Resource Group](screenshots/initial-setup/1-creating-resource-group.jpg)

![Virtual Network](screenshots/initial-setup/2-creating-virtual-network.jpg)

![VNet in Resource Group](screenshots/initial-setup/3-virtual-network-inside-RG.jpg)

![Virtual Machine Creation](screenshots/initial-setup/4-creating-virtual-machine.jpg)

![Verification](screenshots/initial-setup/5-verification.jpg)



**2. Network Security Group (NSG)**

Configured inbound rules to allow traffic for honeypot behavior.

![Selecting NSG](screenshots/creating-network-security-group/1.%20Selecting%20NSG.jpg)

![Opening NSG](screenshots/creating-network-security-group/2.%20Opening%20up%20NSG%20to%20the%20Public.jpg)

![Inbound Rule](screenshots/creating-network-security-group/3.%20Creating%20new%20Inbound%20Security%20Rule.jpg)

![Rule Parameters](screenshots/creating-network-security-group/4.%20Setting%20Rule%20Parameters.jpg)

![New Rule](screenshots/creating-network-security-group/5.%20New%20Security%20Rule.jpg)




**3. Disable Windows Firewall**

Disabled firewall to increase visibility of inbound attacks.

![Retrieve IP](screenshots/disabling-windows-fw-on-vm/1.%20Retrieving%20IP%20Address.jpg)

![RDP](screenshots/disabling-windows-fw-on-vm/2.%20RDP%20into%20VM.jpg)

![Disable Firewall](screenshots/disabling-windows-fw-on-vm/3.%20Disabling%20Firewall.jpg)

![Ping](screenshots/disabling-windows-fw-on-vm/4.%20Pinging%20VM.jpg)

![Checking Logs](screenshots/disabling-windows-fw-on-vm/5.%20Checking%20for%20Failed%20Login%20Attempts.jpg)

![Failed Login](screenshots/disabling-windows-fw-on-vm/6.%20Failed%20Login%20Attempt.jpg)


**4. Log Collection & SIEM (Sentinel)**

Forwarded Windows Security logs to Log Analytics and connected Microsoft Defender.

![Create LAW](screenshots/creating-log-repository/1.%20Creating%20LAW.jpg)

![Create SIEM](screenshots/creating-log-repository/2.%20Creating%20SIEM.jpg)

![Attach LAW](screenshots/creating-log-repository/3.%20Attaching%20LAW%20to%20SIEM.jpg)

![Architecture](screenshots/creating-log-repository/4.%20Current%20Architecture.jpg)

![Connect VM](screenshots/creating-log-repository/5.%20Connecting%20VM%20to%20Log%20Repository%20via%20Windows%20Security%20Events%20AMA.jpg)

![AMA Extension](screenshots/creating-log-repository/6.%20AMA%20Connector%20Added%20to%20VM%20Extension.jpg)


**5. KQL Queries**

Queried failed login attempts (Event ID 4625):

SecurityEvent
| where EventID == 4625
| summarize FailureCount = count() by IpAddress
| order by FailureCount desc


**6. Attack Map (GeoIP Enrichment)**

Mapped attacker IPs to geographic locations.



**Results**

Captured real failed login attempts

Identified attacker IPs and locations

Visualized global attack patterns

Observed over 6,000+ failed login attempts within 18 hours



**Skills Demonstrated**

SIEM configuration and log analysis

Threat detection and investigation

KQL querying

Azure cloud security

