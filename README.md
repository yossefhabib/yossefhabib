# Hey, I'm Yossef Habib 👋

<a href="https://www.linkedin.com/in/yossef-habib/"><img src="https://img.shields.io/badge/-LinkedIn-0072b1?&style=for-the-badge&logo=linkedin&logoColor=white" /></a>
<a href="https://github.com/yossefhabib?tab=repositories"><img src="https://img.shields.io/badge/-Lab_Write--ups-181717?&style=for-the-badge&logo=GitHub&logoColor=white" /></a>
<a href="https://www.credly.com/badges/619c3266-d0ba-463d-bc1c-29e3f5884f19/public_url"><img src="https://img.shields.io/badge/-Security%2B-C8202F?&style=for-the-badge&logo=CompTIA&logoColor=white" /></a>

**InfoSec intern at a regional government agency** · BS in Cybersecurity · CompTIA Security+

Day to day I work alert triage, incident response, and endpoint policy on the InfoSec team of a regional government agency. During my free time I build and break **JuiceBox**, a home detection lab with Active Directory, a SIEM, an attacker VM and its own firewall, so I can run real ATT&CK techniques and see exactly what the telemetry looks like.

---

## 🛡️ What I Do

- **SOC operations:** Cortex XDR alert triage, XSOAR phishing investigations, and incident response in a CJIS-compliant environment co-managed with Palo Alto Unit 42
- **Endpoint control:** Primary ThreatLocker administrator for my organization (application allowlisting, policy management)
- **Detection engineering (homelab):** Simulating MITRE ATT&CK techniques and building Splunk detections from Sysmon and Windows Security logs
- **Network segmentation:** Lab traffic isolated from my home network behind a dedicated OPNsense firewall, with Hyper-V port ACLs as a second layer
- **Automation:** A self-hosted, local-AI video pipeline built with n8n, Ollama and Claude Code

---

## 🧪 Homelab: JuiceBox

A Hyper-V detection lab on a Ryzen 7 7800X3D / 32 GB / RTX 5070 host, supported by an always-on Linux server and a repurposed laptop running OPNsense.

```mermaid
flowchart TB
    Internet((Internet)) --> Router[Home router]
    Router --> Host[JuiceBox host<br/>Hyper-V · GPU worker]
    Router --> Mini[MiniJuiceBox<br/>Ubuntu · n8n · Kasm]
    Router --> FW[OPNsense firewall<br/>repurposed laptop]
    FW -->|lab internet only<br/>home network blocked| EXT[Lab_external switch<br/>dedicated NIC, host not attached]

    subgraph Lab VMs on JuiceBox
        DC[Windows Server 2022<br/>AD DS · DNS · Sysmon · UF]
        W11[Windows 11 target<br/>Sysmon · UF · Atomic Red Team]
        KALI[Kali Linux<br/>attacker]
        SPL[Ubuntu 24.04<br/>Splunk Enterprise]
    end

    EXT --- DC & W11 & KALI & SPL
    KALI == attacks over isolated<br/>Lab_internal switch ==> W11
    DC -. logs .-> SPL
    W11 -. logs .-> SPL
```

**What's in it**
- **Active Directory domain** on Windows Server 2022 with a domain-joined Windows 11 endpoint
- **Telemetry:** Sysmon (Olaf Hartong config) + Splunk Universal Forwarder → Splunk Enterprise
- **Attack simulation:** Kali Linux and Atomic Red Team; first exercise is RDP brute force (**T1110**)
- **Two networks per VM:** an internal-only switch for attack traffic and logs, and an external switch that reaches the internet *only* through OPNsense
- **Segmentation:** OPNsense blocks the lab from the household network, Hyper-V extended port ACLs back it up, and the host blocks all inbound traffic from the lab
- **Host hardening:** least-privilege service accounts, firewall rules scoped to a single source host, versioned firewall-state backups, Smart App Control enforcing

**Currently working on**
- [ ] Getting Splunk back to a clean license state, then the first SPL detection + SOC dashboard for T1110
- [ ] Shipping OPNsense firewall logs into Splunk
- [ ] Next: SOAR/EDR layer (Wazuh + Shuffle or LimaCharlie + Tines)

---

## 🤖 Side Project: JuiceBot, a Local AI Content Pipeline

A self-hosted pipeline that turns each day's top cybersecurity story into a narrated, animated YouTube Short, running on my own hardware with local models.

```mermaid
flowchart LR
    N8N[n8n<br/>MiniJuiceBox] -->|Wake-on-LAN, 5 AM| GPU[JuiceBox GPU]
    GPU --> LLM[Ollama<br/>script]
    LLM --> TTS[Local TTS<br/>narration]
    TTS --> R[ComfyUI + FFmpeg NVENC<br/>visuals · render · Whisper captions]
    R --> TG[Telegram<br/>approve / reject]
    TG -->|approved| YT[YouTube]
```

- **Runs unattended:** n8n cold-boots the GPU box with Wake-on-LAN every morning; services start with nobody logged in
- **Human in the loop:** nothing publishes until I approve it from my phone
- **Built like production:** each service runs under its own non-admin account, LAN ports are scoped to the orchestrator only, and remote access goes through a Cloudflare Tunnel + Zero Trust with no ports forwarded
- **Built with Claude Code** as my coding agent, with a written boundary between what it owns (pipeline code and docs) and what I own (lab architecture)

---

## 📜 Certifications

<a href="https://www.credly.com/badges/619c3266-d0ba-463d-bc1c-29e3f5884f19/public_url"><img src="https://img.shields.io/badge/-Security%2B-C8202F?&style=for-the-badge&logo=CompTIA&logoColor=white" /></a>

- **CompTIA Security+ (SY0-701)** · February 2026
- **BS, Cybersecurity** · Metropolitan State University · May 2026

---

## 🧰 Tools

### SIEM, Detection & Response
<div>
  <img src="https://img.shields.io/badge/-Splunk-000000?&style=for-the-badge&logo=Splunk&logoColor=white" />
  <img src="https://img.shields.io/badge/-Sysmon-0078D6?&style=for-the-badge&logo=Windows&logoColor=white" />
  <img src="https://img.shields.io/badge/-Cortex%20XDR%20%2F%20XSOAR-F04E23?&style=for-the-badge&logo=paloaltonetworks&logoColor=white" />
  <img src="https://img.shields.io/badge/-ThreatLocker-1D3C6E?&style=for-the-badge&logoColor=white" />
  <img src="https://img.shields.io/badge/-MITRE%20ATT%26CK-C0392B?&style=for-the-badge&logoColor=white" />
  <img src="https://img.shields.io/badge/-Atomic%20Red%20Team-B22222?&style=for-the-badge&logoColor=white" />
</div>

### Network & Firewall
<div>
  <img src="https://img.shields.io/badge/-OPNsense-D94F00?&style=for-the-badge&logo=opnsense&logoColor=white" />
  <img src="https://img.shields.io/badge/-Strata-F04E23?&style=for-the-badge&logo=paloaltonetworks&logoColor=white" />
  <img src="https://img.shields.io/badge/-Prisma%20Access%20Browser-F04E23?&style=for-the-badge&logo=paloaltonetworks&logoColor=white" />
  <img src="https://img.shields.io/badge/-Cloudflare%20Zero%20Trust-F38020?&style=for-the-badge&logo=cloudflare&logoColor=white" />
  <img src="https://img.shields.io/badge/-Wireshark-1679A7?&style=for-the-badge&logo=Wireshark&logoColor=white" />
  <img src="https://img.shields.io/badge/-Nmap-4682B4?&style=for-the-badge&logo=Nmap&logoColor=white" />
</div>

### Virtualization & Infrastructure
<div>
  <img src="https://img.shields.io/badge/Hyper--V-0078D6?style=for-the-badge&logo=windows&logoColor=white" />
  <img src="https://img.shields.io/badge/-VMware-607078?&style=for-the-badge&logo=VMware&logoColor=white" />
  <img src="https://img.shields.io/badge/-Active%20Directory-0078D6?&style=for-the-badge&logo=Windows&logoColor=white" />
  <img src="https://img.shields.io/badge/-Docker-2496ED?&style=for-the-badge&logo=docker&logoColor=white" />
  <img src="https://img.shields.io/badge/-Kasm%20Workspaces-2980B9?&style=for-the-badge&logoColor=white" />
</div>

### Automation & AI
<div>
  <img src="https://img.shields.io/badge/-Claude%20Code-D97757?&style=for-the-badge&logo=claude&logoColor=white" />
  <img src="https://img.shields.io/badge/-n8n-EA4B71?&style=for-the-badge&logo=n8n&logoColor=white" />
  <img src="https://img.shields.io/badge/-Ollama-000000?&style=for-the-badge&logo=ollama&logoColor=white" />
  <img src="https://img.shields.io/badge/-ComfyUI-222222?&style=for-the-badge&logoColor=white" />
  <img src="https://img.shields.io/badge/-FFmpeg-007808?&style=for-the-badge&logo=ffmpeg&logoColor=white" />
  <img src="https://img.shields.io/badge/-Python-3776AB?&style=for-the-badge&logo=python&logoColor=white" />
</div>

### Scripting & OS
<div>
  <img src="https://img.shields.io/badge/-PowerShell-5391FE?&style=for-the-badge&logo=PowerShell&logoColor=white" />
  <img src="https://img.shields.io/badge/-Bash-4EAA25?&style=for-the-badge&logo=gnubash&logoColor=white" />
  <img src="https://img.shields.io/badge/-Git-F05032?&style=for-the-badge&logo=git&logoColor=white" />
  <img src="https://img.shields.io/badge/-Windows_Server-0078D6?&style=for-the-badge&logo=Windows&logoColor=white" />
  <img src="https://img.shields.io/badge/-Linux-FCC624?&style=for-the-badge&logo=Linux&logoColor=black" />
  <img src="https://img.shields.io/badge/-Kali_Linux-557C94?&style=for-the-badge&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/-FreeBSD-AB2B28?&style=for-the-badge&logo=freebsd&logoColor=white" />
</div>

---

## 📂 Projects

### Completed

| Project | Description |
|---------|-------------|
| [JuiceBot: AI Content Creator Agent](https://github.com/yossefhabib/JuiceBot-AI) | A self-hosted AI pipeline that turns each day's top cybersecurity story into a narrated, animated YouTube Short using local models. Hardened with per-service accounts, LAN ports scoped to a single host, no forwarded ports, and a human approval gate from my phone. Built with Claude Code. |
| OPNsense Lab Firewall *(write-up coming)* | Turned an old gaming laptop into a dedicated OPNsense firewall that gives lab VMs internet access while blocking them from the home network. Includes a persistent fix for a flapping USB NIC on FreeBSD and a Hyper-V switch moved onto its own adapter. |
| [Mac Mini Ubuntu Kasm Server](https://github.com/yossefhabib/MiniJuiceBox) | Repurposed a T2 Intel Mac Mini into a 24/7 headless Ubuntu server running Kasm Workspaces and n8n, reachable from anywhere through Cloudflare Tunnel + Zero Trust with zero ports forwarded. |
| [Setting up Splunk](https://github.com/yossefhabib/Splunk) | Deployed Splunk on Ubuntu to centralize logs from Windows Server 2022 and Windows 11 via the Universal Forwarder, with Sysmon telemetry for threat detection and AD monitoring. |
| [Setting up Active Directory DS](https://github.com/yossefhabib/Initial-AD-setup-) | Built an Active Directory domain from scratch on Windows Server, joined a Windows 11 client, and created groups and users. |
| [Subnet Configuration & ICMP Validation](https://github.com/yossefhabib/Netconfig) | Built an isolated Hyper-V network with static IPv4 across Windows and Linux VMs, validated connectivity, and adjusted firewall rules as groundwork for AD and the SIEM. |
| [Hyper-V Kali Linux VM Setup](https://github.com/yossefhabib/HyperVSetUp) | Deployed an isolated Kali Linux VM on Hyper-V with network segmentation, resource tuning, and image integrity verification for AD attack simulation. |
| [Homelab Host Build](https://github.com/yossefhabib/HomelabWorkstationBuild) | Designed, assembled and validated the Windows 11 Pro workstation that hosts the multi-VM lab and the GPU workloads. |

### In Progress

| Project | Description |
|---------|-------------|
| T1110 Detection Lab | RDP brute force from Kali against the Windows 11 target, confirming 4625/4624 events land in Splunk, then the first SPL detection and a SOC dashboard. |
| Firewall Logs → SIEM | Forwarding OPNsense firewall logs into Splunk as a second detection data source. |

### Planned

| Project | Description |
|---------|-------------|
| SOAR Automation | Wazuh + Shuffle for automated incident-response playbooks |
| EDR Integration | LimaCharlie + Tines for endpoint detection and response |
| CSI Linux VM | OSINT and digital-forensics workstation inside the lab |
| Offline Knowledge Server | A local, offline reference library and AI assistant (Project NOMAD) |

---

📫 Open to conversations about SOC work, detection engineering, and homelabs. Reach me on [LinkedIn](https://www.linkedin.com/in/yossef-habib/).

