# Introduction to Cyber Security

## Overview

This module introduces the two primary pillars of cybersecurity: Offensive Security (attacking systems to find weaknesses) and Defensive Security (protecting and monitoring systems against attacks). It also provides a high-level overview of potential career paths within the industry.

## Learning Objectives

- Understand the difference between offensive and defensive security.
- Learn the attacker's mindset regarding content discovery and hidden website paths.
- Understand how to monitor, detect, and block ongoing attacks using defensive concepts.
- Identify basic cybersecurity career roles (SOC Analyst, Security Engineer, Penetration Tester).

## Background

Before diving into technical tools, it is crucial to understand the "why" behind cybersecurity. Systems are built to function, but functionality often overlooks security. Cybersecurity exists to protect the Confidentiality, Integrity, and Availability (CIA Triad) of data. To protect systems effectively, defenders must understand how attackers operate. Therefore, learning offensive basics is a fundamental requirement for becoming a good defender.

## Key Concepts

### 1. Offensive Security

**General Explanation:** Offensive security involves proactively simulating attacks against a system to identify vulnerabilities before malicious actors do. It requires thinking like an attacker—mapping the target's attack surface, discovering hidden endpoints, and exploiting weaknesses to prove a system is insecure.

**Baby Talk Explanation:** Imagine you are the owner of a bank. Instead of waiting for a real robber to come and steal your money, you hire a "good robber" to try and break into your bank. The good robber tells you exactly which window was unlocked so you can fix it before the real bad guys find it.

### 2. Defensive Security

**General Explanation:** Defensive security is the process of protecting systems, networks, and data from unauthorized access and attacks. It focuses on three main areas: Prevention (configuring firewalls, patching systems), Detection (monitoring logs and alerts), and Response (investigating incidents and blocking malicious IP addresses).

**Baby Talk Explanation:** You are the security guard sitting in the control room looking at TV screens (monitoring). When you see someone sneaking around the back door (detection), you run over and lock the door so they can't get in (response).

### 3. Tool Spotlight: Directory Brute-forcing (e.g., `dirb`)

**General Explanation:** Directory brute-forcing is a technique used for content discovery. Tools like `dirb` send HTTP requests to a web server using a wordlist (a text file containing thousands of common words). If the server responds with a 200 OK status, the tool knows that hidden directory or file exists. 

**Baby Talk Explanation:** Imagine a massive apartment building with no directory. A robot knocks on every single door—Door 1, Door 2, Door "Admin", Door "Secret"—and writes down a list of every door where someone actually answers.

### 4. Career Paths

- **SOC Analyst (Blue Team):** Monitors networks, investigates alerts, and responds to ongoing attacks.
- **Security Engineer:** Builds and maintains secure infrastructure and detection systems (like Intrusion Detection Systems - IDS).
- **Penetration Tester (Red Team):** Ethically hacks systems and software to find and report vulnerabilities.

## Practical Exercises

_Note: In compliance with TryHackMe's Terms of Service, specific lab details, commands, and answers are omitted._

- **Offensive Simulation:** Applied the attacker mindset to a simulated web environment. Practiced using directory brute-forcing concepts to discover hidden web endpoints that were not visibly linked on the target's main page.
- **Defensive Simulation:** Reviewed a simulated security monitoring dashboard. Practiced reading alerts to identify ongoing malicious activity, tracing the attacker's actions, and understanding the process of applying firewall rules to block malicious IP addresses.

## Challenges Encountered

### Challenge: Understanding Directory Brute-forcing Tools

- **The Issue:** The learning material introduced the concept of directory brute-forcing but did not fully explain the mechanics, pros, and cons of running these tools against real websites.
- **Root Cause:** The module was designed to show a quick result rather than teach the underlying mechanics of web scraping.
- **Resolution (Mentor Note):** These tools guess directory names using a dictionary (wordlist).
    - **Pros:** Fast, automates finding hidden admin panels or backup files.
    - **Cons/Risks:** It generates a massive amount of web traffic (noise). On real websites, this will immediately trigger security alarms (like an IDS/IPS) and get your IP banned.
- **Alternative Solutions:** In real engagements, penetration testers use tools like `ffuf` or `gobuster` which are faster and offer more filtering options, but the core concept remains the same.

## Lessons Learned

- Offensive and Defensive security are two sides of the same coin; defenders must understand attacker techniques.
- Content discovery is a critical first step in web application testing because hidden pages often contain sensitive functionality.
- Defensive security is not just about building walls; it requires active monitoring and incident response.

## Best Practices

- **Authorization First:** Never run scanning tools or attempt to block IPs on a system you do not own or have explicit permission to test.
- **Log Everything:** In defensive security, logs are your best friend. An alert is useless if you don't have logs to investigate what the attacker did before the alert triggered.
- **Principle of Least Privilege:** Firewalls should be configured to deny all traffic by default, only allowing explicitly necessary IPs and ports.

## Common Mistakes

- **Running scanners blindly:** Beginners often run directory brute-forcers on real websites without realizing it is illegal and highly noisy.
- **Assuming "Offensive" means "Bad":** Offensive security is highly structured, legal, and relies heavily on documentation. It is not about malicious destruction.
- **Blocking IPs permanently:** In defensive security, blocking a single IP is a temporary fix. Attackers use VPNs and botnets; they will change IPs. You must also patch the vulnerability they were trying to exploit.

## Further Reading

- [TryHackMe - Pre Security Path](https://tryhackme.com/path/outline/presecurity)
- [OWASP - Content Discovery](https://owasp.org/www-community/attacks/Brute_force_attack)
- [MITRE ATT&CK Framework](https://attack.mitre.org/)