# Home SOC Lab

A virtualized Security Operations Center (SOC) lab built from scratch using VirtualBox to simulate a small enterprise environment and practice security monitoring, threat detection, incident investigation, and response.

The lab is initially inspired by the **Building a SOC Lab at Home** learning path from LetsDefend, but is independently expanded and customized to develop practical Blue Team and SOC skills.

> **Status:** 🟡 In Progress

---

## 🎯 Objectives

The main goal of this project is to build a realistic and isolated security environment where the complete SOC workflow can be practiced:

**Attack → Telemetry → Detection → Alert → Investigation → MITRE ATT&CK Mapping → Response → Incident Documentation**

The lab focuses on developing practical skills in:

* Security Monitoring
* Threat Detection & Detection Engineering
* Incident Response
* Active Directory Security
* Windows & Network Security
* Log Analysis & Endpoint Telemetry
* Threat Hunting
* MITRE ATT&CK

---

## 🏗️ Architecture

The lab is designed as a segmented virtual enterprise environment using **pfSense** as the network security boundary.

```text
                              Internet
                                  │
                           VirtualBox NAT
                                  │
                           ┌─────────────┐
                           │  SOC-pfSense │
                           │ Firewall / FW│
                           └──────┬──────┘
                                  │
                 ┌────────────────┴────────────────┐
                 │                                 │
              GREEN                             ORANGE
          Internal LAN                            DMZ
                 │                                 │
        ┌────────┴────────┐                        │
        │                 │                        │
      DC01              WIN01                   Linux01
   AD / DNS           Workstation                DMZ Host
        │
        │
   Sysmon / CrowdSec
        │
        ▼
      Wazuh
       SIEM
        │
        ▼
 Detection & Investigation
        │
        ▼
 MITRE ATT&CK Mapping
        │
        ▼
 Response & Incident Report
```

The architecture will evolve as new systems, security controls, telemetry sources, and attack scenarios are introduced.

The lab is intentionally isolated from production environments, allowing controlled security events and attack simulations to be generated without affecting external systems.

For the complete network design, addressing scheme, segmentation, and architectural decisions, see [`docs/00-architecture.md`](docs/00-architecture.md).

---

## 🧰 Technology Stack

| Category                      | Technology                          |
| ----------------------------- | ----------------------------------- |
| Virtualization                | VirtualBox                          |
| Firewall / Network Security   | pfSense                             |
| Identity & Directory Services | Active Directory                    |
| Endpoint                      | Windows 10/11 Pro                   |
| Endpoint Telemetry            | Sysmon                              |
| Security Engine               | CrowdSec                            |
| SIEM                          | Wazuh                               |
| Attack Simulation             | Kali Linux / other controlled tools |
| Detection Framework           | MITRE ATT&CK                        |

---

## 🖥️ Lab Environment

| Hostname      | Role                    | Network              | IP Address      |
| ------------- | ----------------------- | -------------------- | --------------- |
| `SOC-pfSense` | Firewall / Router       | WAN / GREEN / ORANGE | `.1`            |
| `DC01`        | Domain Controller / DNS | GREEN                | `192.168.10.10` |
| `WIN01`       | Domain Workstation      | GREEN                | `192.168.10.20` |
| `Linux01`     | DMZ Host                | ORANGE               | `192.168.20.x`  |
| `SIEM01`      | Wazuh SIEM              | GREEN                | `TBD`           |
| `ATTACKER01`  | Attack Simulation       | TBD                  | `TBD`           |

### Network Segmentation

| Network | Purpose                     | Subnet            | Gateway        |
| ------- | --------------------------- | ----------------- | -------------- |
| WAN     | Internet connectivity       | VirtualBox NAT    | DHCP           |
| GREEN   | Internal enterprise network | `192.168.10.0/24` | `192.168.10.1` |
| ORANGE  | DMZ / exposed services      | `192.168.20.0/24` | `192.168.20.1` |

---

## 📁 Repository Structure

```text
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
```

### Repository Organization

* **`README.md`** — Project overview, architecture, technologies, and roadmap.
* **`CHECKPOINTS.md`** — Detailed implementation checklist and validation criteria.
* **`docs/`** — Technical documentation for each component of the lab.
* **`configs/`** — Configuration files used by security tools and services.
* **`detections/`** — Detection engineering, MITRE ATT&CK mapping, and incident reports.
* **`screenshots/`** — Visual evidence from the lab environment.
* **`scripts/`** — Automation and utility scripts.

---

## 🚧 Roadmap

The lab is being developed incrementally, with each phase validated before moving to the next.

| Phase | Focus                                                            | Status |
| ----- | ---------------------------------------------------------------- | ------ |
| 1     | Network Infrastructure — pfSense, GREEN/ORANGE                   | ⬜      |
| 2     | Active Directory — DC01, WIN01, domain join                      | ⬜      |
| 3     | Security Telemetry — Sysmon, CrowdSec                            | ⬜      |
| 4     | SIEM — Wazuh deployment & dashboards                             | ⬜      |
| 5     | Attack Simulation — attacker VM & scenarios                      | ⬜      |
| 6     | SOC Operations — investigation, MITRE mapping & incident reports | ⬜      |

Detailed criteria, tasks, and validation steps for each phase are documented in [`CHECKPOINTS.md`](CHECKPOINTS.md).

---

## 🔎 Detection & Investigation

Once the monitoring infrastructure is operational, attack scenarios will be executed against intentionally deployed lab systems.

Each scenario follows a structured SOC investigation workflow:

```text
Attack
  ↓
Telemetry Generation
  ↓
Detection
  ↓
Alert Triage
  ↓
Investigation
  ↓
MITRE ATT&CK Mapping
  ↓
Response
  ↓
Incident Documentation
```

Investigation results and detection coverage are tracked under:

* [`detections/mitre-attack-mapping.md`](detections/mitre-attack-mapping.md) — MITRE ATT&CK techniques covered and corresponding detection rules.
* [`detections/incident-reports/`](detections/incident-reports/) — Individual incident investigation reports.

The objective is not only to generate alerts, but to understand **why an alert was triggered, what happened on the endpoint or network, how the activity maps to an adversary technique, and how the incident should be handled by a SOC analyst.**

---

## 📚 References & Resources

This project uses official documentation and security learning resources as technical references, including:

* LetsDefend
* Microsoft Documentation
* Microsoft Sysinternals
* MITRE ATT&CK
* pfSense Documentation
* CrowdSec Documentation
* Wazuh Documentation

The lab is independently implemented and documented, with configurations and attack scenarios adapted to the objectives of this project.

Official download links, software sources, and other resources used to build the environment are maintained separately in:

**[`home-soc-lab-resources`](https://github.com/Joaopmsitz/home-soc-lab-resources)**

---

## ⚠️ Disclaimer

This project is intended exclusively for **education, defensive security training, and authorized security testing**.

All attack simulations are performed against systems intentionally deployed and controlled within this isolated laboratory environment.

No unauthorized systems or production environments are targeted.
