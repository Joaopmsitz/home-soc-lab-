# Home SOC Lab

A virtualized Security Operations Center (SOC) lab built from scratch using VirtualBox to simulate a small enterprise environment and practice security monitoring, threat detection, incident investigation, and response.

The lab is initially inspired by the **Building a SOC Lab at Home** learning path from LetsDefend, but is independently expanded and customized to develop practical Blue Team and SOC skills.

> **Status:** 🟡 In Progress

---

## 🎯 Objectives

The main goal of this project is to build a realistic, isolated security environment to practice the complete SOC workflow:

Attack → Telemetry → Detection → Alert → Investigation → MITRE ATT&CK Mapping → Response → Incident Documentation

Skills developed in this lab:

- Security Monitoring
- Threat Detection & Detection Engineering
- Incident Response
- Active Directory Security
- Windows & Network Security
- Log Analysis & Endpoint Telemetry
- Threat Hunting
- MITRE ATT&CK

---

## 🏗️ Architecture

```text
                        Internet
                            │
                       pfSense (FW)
                            │
              ┌─────────────┴─────────────┐
           GREEN                        ORANGE
        (internal LAN)                  (DMZ)
              │                            │
       ┌──────┴──────┐                     │
     DC01          WIN01                Linux01
   (AD/DNS)       (Client)                (DMZ)
              │
          Sysmon / CrowdSec
              │
          Wazuh (SIEM)
              │
     Detection & Investigation

The architecture evolves as new systems, security controls, and attack scenarios are introduced.

The lab is designed as an isolated virtual environment, allowing controlled security events and attack scenarios to be generated without affecting external systems.

Full network design, subnets, and architectural decisions: docs/00-architecture.md

🧰 Technology Stack
Category	Technology
Virtualization	VirtualBox
Firewall / Network Security	pfSense
Identity & Directory Services	Active Directory
Endpoint	Windows 10/11 Pro
Endpoint Telemetry	Sysmon
Security Engine	CrowdSec
SIEM	Wazuh
Attack Simulation	Kali Linux / other controlled tools
Detection Framework	MITRE ATT&CK
🖥️ Lab Environment
Hostname	Role	Network	IP
SOC-pfSense	Firewall / Router	WAN / GREEN / ORANGE	.1
DC01	Domain Controller / DNS	GREEN	192.168.10.10
WIN01	Domain Workstation	GREEN	192.168.10.20
Linux01	DMZ Host	ORANGE	192.168.20.x
SIEM01	Wazuh SIEM	GREEN	TBD
ATTACKER01	Attack Simulation	TBD	TBD
📁 Repository Structure
home-soc-lab/
│
├── README.md
├── CHECKPOINTS.md
│
├── docs/
│   ├── 00-architecture.md
│   ├── 01-pfsense.md
│   ├── 02-active-directory.md
│   ├── 03-windows-workstation.md
│   ├── 04-sysmon.md
│   ├── 05-crowdsec.md
│   ├── 06-siem-wazuh.md
│   └── 07-attack-detection-response.md
│
├── configs/
│   ├── sysmon/
│   ├── crowdsec/
│   └── wazuh/
│
├── detections/
│   ├── mitre-attack-mapping.md
│   └── incident-reports/
│
├── screenshots/
│
└── scripts/
🚧 Roadmap
Phase	Focus	Status
1	Network Infrastructure (pfSense, GREEN/ORANGE)	⬜
2	Active Directory (DC01, WIN01, domain join)	⬜
3	Security Telemetry (Sysmon, CrowdSec)	⬜
4	SIEM (Wazuh deployment & dashboards)	⬜
5	Attack Simulation (attacker VM, scenarios)	⬜
6	SOC Operations (investigation, MITRE mapping, incident reports)	⬜

Detailed criteria and sub-tasks for each phase: CHECKPOINTS.md

🔎 Detection & Investigation

Each attack scenario follows a SOC investigation workflow, from telemetry generation to incident documentation.

Results are tracked under:

detections/mitre-attack-mapping.md — techniques covered vs. detection rules created
detections/incident-reports/ — one report per investigated case
📚 References

This project uses official documentation and security learning resources as technical references, including:

LetsDefend
Microsoft documentation
Microsoft Sysinternals
MITRE ATT&CK
pfSense documentation
CrowdSec documentation
Wazuh documentation

The lab is independently implemented and documented, with configurations and scenarios adapted to the objectives of this project.

Additional resources and official download links are maintained in home-soc-lab-resources.

⚠️ Disclaimer

This project is intended exclusively for education, defensive security training, and authorized security testing.

All attack simulations are performed against systems intentionally deployed and controlled within this isolated laboratory environment.
