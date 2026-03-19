# Endpoint Security Notes

![Status](https://img.shields.io/badge/Status-Active-brightgreen)
![Focus](https://img.shields.io/badge/Focus-SOC%20Analyst-blue)
![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Linux-lightgrey)

## Overview

A living reference document built from hands-on endpoint investigation using Process Explorer on a clean Windows host. Used to develop SOC analyst baseline knowledge for endpoint triage, IOC identification, and incident response across multiple platforms.

This repository is actively maintained and updated as new techniques, tools, and findings are discovered through practical investigation and study.

---

## Purpose

The goal of this repository is to document foundational endpoint security knowledge from a SOC analyst perspective — not copied from courses, but built from direct hands-on investigation. It serves as both a personal reference during endpoint triage and a demonstration of analytical thinking applied to real systems.

---

## Contents

| Document | Description |
|----------|-------------|
| [Windows Process Baseline](./windows-process-baseline.md) | Legitimate Windows processes, their expected locations, parent processes, and red flags — built from Process Explorer investigation on a clean host machine |
| [LOLBins Reference](./lolbins-reference.md) | Living Off the Land Binaries — legitimate Windows tools commonly abused by attackers, with detection tips for each |

---

## Methodology

Each document in this repository is built using the following approach:

- **Hands-on investigation** - findings come from direct observations using tools like Sysinternals Process Explorer on a clean Windows environment
- **Baseline first** - normal behaviour is documented before suspicious behaviour, because you cannot identify anomalies without knowing what normal looks like
- **Detection focused** - every entry includes not just what something is, but how it would appear as an IOC during endpoint triage
- **Continuously updated** - this is a living document, updated as new findings emerge through study and practical lab work

---

## Tools Used

| Tool | Purpose |
|------|---------|
| Sysinternals Process Explorer | Process investigation and baseline building |
| Sysinternals Process Monitor | Real-time file, registry, and process activity monitoring |
| Windows Task Manager | Quick process reference |
| LetsDefend EDR Labs | Practical endpoint triage and IOC identification |
| VirusTotal | Hash and URL reputation checking |

---

## Related Repositories

| Repository | Description |
|------------|-------------|
| [letsdefend-soc-investigations](../letsdefend-soc-investigations) | SOC alert investigation writeups from LetsDefend |
| [portswigger-web-security-labs](../portswigger-web-security-labs) | Web attack analysis and detection from PortSwigger |
| [comptia-securityplus-labs](../comptia-securityplus-labs) | Applied defensive security labs from CompTIA Security+ |

---

## Certifications & Study Context

This repository supports active study and professional development in the following areas:

- ✅ CompTIA Security+ - Certified
- 🔄 CompTIA Network+ - In Progress
- 🔄 LetsDefend SOC Analyst Learning Path - In Progress
- 🔄 PortSwigger Web Security Academy - In Progress

---

## Author

**[Sindi Msubo]**
Cybersecurity Analyst student actively building SOC fundamentals through hands-on endpoint investigation, LetsDefend alert triage, and PortSwigger web security labs |
[LinkedIn](https://linkedin.com/in/sindiswa-msubo-1b908716a/) | [GitHub](https://github.com/Sindi298)

---

*This repository is part of a broader cybersecurity portfolio built to demonstrate practical, hands-on security knowledge for SOC analyst and defensive security roles.*
