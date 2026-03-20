# VulnVision 360

## Continuous Compliance & Threat Exposure Engine

---

# Project Overview

**VulnVision 360** is a cybersecurity lab project that simulates a real-world vulnerability management and compliance monitoring system.

The project demonstrates how organizations can continuously monitor their infrastructure, identify vulnerabilities, enforce security compliance, and remediate risks.

The environment simulates an enterprise scenario where legacy systems remain unpatched, increasing the organization's attack surface.

---

# Tools & Technologies

| Tool             | Purpose                           |
| ---------------- | --------------------------------- |
| Nmap             | Network discovery and enumeration |
| OpenVAS (GVM)    | Vulnerability scanning            |
| OpenSCAP         | Compliance auditing               |
| Bash / Ansible   | Automation & remediation          |
| Kali Linux       | Security testing platform         |
| Ubuntu Server    | Asset discovery & enumeration     |
| Metasploitable 2 | Vulnerability scanning target     |

---

# Lab Environment

| Machine          | Role                             | IP Address    |
| ---------------- | -------------------------------- | ------------- |
| Kali Linux       | Vulnerability Scanner            | 192.168.198.4 |
| Ubuntu Server    | Discovery Target                 | 192.168.198.3 |
| Metasploitable 2 | Vulnerable Target (OpenVAS Scan) | 192.168.198.7 |

Network Range: 192.168.198.0/24

> Note: Ubuntu Server was used for asset discovery and enumeration.
> Metasploitable 2 (intentionally vulnerable machine) was used specifically for vulnerability scanning using OpenVAS to generate meaningful security findings.

---

Network Range:

192.168.198.0/24

# Week 1 – Discovery & Setup

## Objective

To identify all active systems within the network and build a complete asset inventory.

---

## Network Discovery (Nmap)

Network discovery was performed using Nmap to identify all live hosts within the internal network.

Command used:

```bash
sudo nmap -sn 192.168.198.0/24

```
### Result

The scan successfully discovered the target Ubuntu machine and the Kali scanning system.

![](screenshots/active_host.png)


## Service & Port Enumeration

After identifying live hosts, a deeper aggrassive scan was performed to determine open ports, running services, and OS information.

Command used:

```bash
sudo nmap -A -T4 192.168.198.3
```

This scan enables:

* OS detection
* Service version detection
* Script scanning
* Traceroute

### Result

The scan revealed several open services including SSH (23) and HTTP(80) running on the target system.

![](screenshots/port_enum.png)

---

# OpenVAS Installation & Setup

The vulnerability scanning platform **OpenVAS (Greenbone Vulnerability Manager)** was installed on Kali Linux.

Commands used:

```bash
sudo gvm-setup
sudo gvm-start
```

After installation, the web interface was accessed using:

```
https://127.0.0.1:9392
```

The dashboard confirms that the vulnerability scanner is properly installed and operational.

![](screenshots/openvas_dash.png)

---

## Asset Inventory

| Host             | IP Address    | OS    | Open Ports       | Services                      |
| ---------------- | ------------- | ----- | ---------------- | ----------------------------- |
| Kali Linux       | 192.168.198.4 | Linux | 22               | SSH                           |
| Ubuntu Server    | 192.168.198.3 | Linux | 22,80            | SSH, HTTP                     |
| Metasploitable 2 | 192.168.198.7 | Linux | 21,22,23,80,3306 | FTP, SSH, Telnet, HTTP, MySQL |

---

## Week 1 Gate Check

✔ Network discovery completed
✔ Service enumeration completed
✔ OpenVAS installed and configured
✔ Asset inventory created

---

# Week 2 – Vulnerability Assessment

## Objective

To identify, analyze and prioritize vulnerabilities in the target system using OpenVAS. This phase simulates both external and internal attacker perspectives to evaluate the security posture of the environment.


### Target Information

Target Machine: Metasploitable 2

IP Address: 192.168.198.7

Scanner: OpenVAS (GVM)

Scan Type: Full and Fast

## Scan Execution

A vulnerability scan was performed using OpenVAS against the **Metasploitable 2** system.

<p align="center">
<img src="screenshots/openvas_scan_running.png" width="800">
</p>

---

## Scan Results Overview

The scan identified multiple vulnerabilities, including several **Critical (CVSS 10.0)** issues.

<p align="center">
<img src="screenshots/openvas_results.png" width="800">
</p>

---

## Critical Vulnerability Analysis

### Apache Tomcat Default Credentials

* **Severity:** Critical
* **CVSS Score:** 10.0

Default credentials allow attackers to gain administrative access.

**Impact:**

* Full system compromise
* Remote code execution

**Remediation:**

* Change default credentials
* Restrict admin access

---

### rlogin Passwordless Login

* **Severity:** Critical
* **CVSS Score:** 10.0

Allows remote login without authentication.

**Impact:**

* Unauthorized system access

**Remediation:**

* Disable rlogin
* Use SSH


## Vulnerability Details

<p align="center">
<img src="screenshots/openvas_cve_details.png" width="800">
</p>

---

## Week 2 Gate Check

✔ Identified Critical vulnerabilities (CVSS ≥ 9.0)
✔ Analyzed vulnerability impact
✔ Documented remediation steps

---

# Project Progress

Week 1 – Discovery & Setup ✔ Completed
Week 2 – Vulnerability Assessment ✔ Completed
Week 3 – Compliance Automation ⏳ In Progress
Week 4 – Remediation & Reporting ⏳ Pending

---

# Next Phase – Week 3

The next stage focuses on compliance auditing using OpenSCAP and CIS Benchmarks.

Planned tasks:

* Perform compliance scan using CIS profiles
* Identify configuration weaknesses
* Generate structured HTML report

