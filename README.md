# VulnVision 360

## Continuous Compliance & Threat Exposure Engine

### Project Overview

**VulnVision 360** is a cybersecurity project that demonstrates a continuous vulnerability management and compliance automation workflow. The project focuses on discovering network assets, identifying vulnerabilities, enforcing compliance standards, and validating remediation in a controlled lab environment.

The objective is to simulate a real-world enterprise scenario where legacy systems remain unpatched, increasing the organization's attack surface.

---

# Tools & Technologies

| Tool           | Purpose                                 |
| -------------- | --------------------------------------- |
| Nmap           | Network discovery and asset enumeration |
| OpenVAS (GVM)  | Vulnerability scanning                  |
| OpenSCAP       | Compliance auditing                     |
| Bash / Ansible | Automated remediation                   |
| Kali Linux     | Security testing platform               |
| Ubuntu Server  | Target system                           |

---

# Lab Environment

| Machine       | Role                  | IP Address    |
| ------------- | --------------------- | ------------- |
| Kali Linux    | Vulnerability Scanner | 192.168.198.4 |
| Ubuntu Server | Target System         | 192.168.198.3 |

Network Range:

192.168.198.0/24

---

# Week 1 – Discovery & Setup

## Objective

The goal of Week 1 is to identify all active hosts within the internal network and build a complete asset inventory.

---

## Network Discovery

Network discovery was performed using **Nmap** to identify live hosts in the subnet.

Command used:

```
sudo nmap -sn 192.168.198.0/24
```

This scan identifies all reachable systems within the internal network.

---

## Service and Port Enumeration

A detailed scan was performed on the discovered Ubuntu server to identify open ports and running services.

Command used:

```
sudo nmap -A -T4 192.168.198.3
```

This command enables:

* OS detection
* Service version detection
* Script scanning
* Traceroute

---

## Asset Inventory

The following assets were identified during the network discovery phase.

| Host          | IP Address    | Operating System | Open Ports    | Services              |
| ------------- | ------------- | ---------------- | ------------- | --------------------- |
| Kali Linux    | 192.168.198.5 | Linux            | 22            | SSH                   |
| Ubuntu Server | 192.168.198.3 | Linux            | 21,22,80,3306 | FTP, SSH, HTTP, MySQL |

---

## Evidence

Screenshots and scan outputs are stored in the repository:

```
/scans
/screenshots
```

Example files:

* nmap_scan_results.txt
* network_discovery.png

---

# Week 1 Gate Check

The asset discovery phase successfully identified all active systems within the subnet.

Deliverables:

* Network discovery results
* Asset inventory documentation
* OpenVAS vulnerability scanner installed and ready

This completes **Week 1 – Discovery & Setup**.

---

# Next Phase

Week 2 will focus on **vulnerability assessment** using OpenVAS.

Tasks include:

* Running unauthenticated vulnerability scans
* Running authenticated scans using SSH credentials
* Identifying critical vulnerabilities (CVSS ≥ 9)
* Researching remediation steps
