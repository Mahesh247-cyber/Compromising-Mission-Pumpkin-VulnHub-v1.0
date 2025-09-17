# Compromising VulnHub Machine – Mission-Pumpkin v1.0: PumpkinFestival

This repository contains my **Ethical Hacking Major Project (Elewayte)** on compromising the VulnHub machine **Mission-Pumpkin v1.0: PumpkinFestival**.  
It includes the methodology, findings, and recommendations from the penetration test.

---

## Table of Contents
- [Confidentiality Statement](#confidentiality-statement)
- [Disclaimer](#disclaimer)
- [Project Overview](#project-overview)
- [Scope](#scope)
- [Methodology](#methodology)
- [Tools Used](#tools-used)
- [Executive Summary](#executive-summary)
- [Vulnerability Summary](#vulnerability-summary)
- [Technical Findings & Techniques](#technical-findings--techniques)
- [Recommendations](#recommendations)
- [Appendix: Tokens & Ticket](#appendix-tokens--ticket)

---

## Confidentiality Statement
This report is prepared for educational purposes as part of the Ethical Hacking Major Project (Elewayte).  
It contains sensitive information about vulnerabilities and exploitation techniques for a virtual machine designed for practice.  
Distribution or use outside of this context is not recommended without proper authorization.

---

## Disclaimer
This assessment was conducted in a **controlled, virtual environment** using a VulnHub machine intended for ethical hacking training.  
Activities were performed on authorized systems with no impact on real infrastructure.

---

## Project Overview
- **Machine:** Mission-Pumpkin v1.0: PumpkinFestival (VulnHub)  
- **Goal:** Gain root access, collect 10 PumpkinTokens, and retrieve the PumpkinFestival_Ticket.  
- **Environment:** VirtualBox/VMware with Kali Linux as the attacker VM.  
- **URL:** [https://www.vulnhub.com/entry/mission-pumpkin-v10-pumpkinfestival,329/](https://www.vulnhub.com/entry/mission-pumpkin-v10-pumpkinfestival,329/)

---

## Scope
- **In Scope:** Target VM’s IP and all open ports/services.  
- **Exclusions:** No DoS, social engineering, or host system modifications.  
- **Assumptions:** Bridged or host-only networking for reachability.

---

## Methodology
Based on **OWASP Testing Guide** and **PTES**:

1. Reconnaissance  
2. Scanning  
3. Enumeration  
4. Exploitation  
5. Privilege Escalation  
6. Post-Exploitation (collect PumpkinTokens and the final ticket)

---

## Tools Used
- Nmap, Hydra, WPScan, DirBuster  
- FTP Client, SSH  
- CyberChef (decoding)  
- tar, bunzip2, zip/gzip utilities  

---

## Executive Summary
The Mission-Pumpkin v1.0 machine was successfully compromised:

- Initial access via **anonymous FTP** and web enumeration.  
- User-level SSH access obtained after decoding credentials.  
- Privilege escalation through **sudo misconfiguration** allowed arbitrary scripts to be run as root.  
- All **10 PumpkinTokens** collected and the **PumpkinFestival_Ticket** retrieved.

Key weaknesses:
- Weak/reversible passwords  
- Information leaks in web sources  
- Overly permissive sudo rules  

---

## Vulnerability Summary

| Description                                       | Count | Severity   |
|---------------------------------------------------|-------|-----------|
| Privilege escalation via sudo misconfiguration    | 2     | Critical   |
| Weak password brute-forcing / SSH key exposure    | 3     | High       |
| Information disclosure (tokens in source code)    | 4     | Moderate   |
| Anonymous FTP access                              | 1     | Low        |

---

## Technical Findings & Techniques
Highlights of the attack path (see full write-up in the repo):

- **Recon:** `nmap -p- -A <target-ip>`  
- **Enumeration:** FTP anonymous access, HTTP source code, WordPress users, hidden directories.  
- **Exploitation:** WordPress login (admin & morse), brute-forcing FTP for harry, nested archive extraction for jack’s SSH key.  
- **Privilege Escalation:** Exploited sudo wildcard to run a custom script as root.  
- **Post-Exploitation:** Retrieved the PumpkinFestival_Ticket as root.

---

## Recommendations
- Use strong passwords and disable anonymous FTP.  
- Secure and harden WordPress (update plugins, hide sensitive files).  
- Fix sudoers misconfigurations to restrict wildcards.  
- Regularly patch and audit services for leaks.  

---

## Appendix: Tokens & Ticket
Collected **PumpkinTokens** and **PumpkinFestival_Ticket** during exploitation:

| Location/Description      | Token # | Value (truncated) |
|---------------------------|---------|-------------------|
| FTP /secret/token.txt     | 1       | 2d6dbbae84…       |
| HTTP page source          | 2       | 45d9ee7239…       |
| WordPress pumpkins.local  | 3–7     | …                 |
| Harry’s FTP token         | 8       | ba9fa9abf2…       |
| Nested data.txt           | 9       | …                 |
| /home/jack/token executable | 10    | 8d66ef0055…       |

---

## 📧 Contact
Prepared by **Mahesh (CSE – Cyber Security)**  
For questions: *(Kairamkondamaheshh@gmail.com)*  

---
