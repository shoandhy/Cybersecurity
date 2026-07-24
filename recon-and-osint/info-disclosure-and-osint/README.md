# Information Disclosure & Basic OSINT

## Overview

This document covers the foundational concepts of Information Disclosure, Sensitive Data Exposure, and Open Source Intelligence (OSINT). It outlines the difference between active and passive reconnaissance and provides a comprehensive toolbox of industry-standard utilities used to map targets and identify vulnerabilities before an attack even begins.

## Primary Bullet Points

- **Data Failures:** Information Disclosure is accidentally leaving the door cracked open; Sensitive Data Exposure is failing to lock the safe.
- **Reconnaissance:** The process of gathering as much data as possible about a target. It is divided into Active (interacting directly) and Passive (using third parties) techniques.
- **Active Tooling:** Tools like Nmap, Nuclei, and GoBuster interact directly with the target, leaving digital footprints in logs.
- **Passive Tooling:** Tools like Shodan, GAU, and Sublist3r gather historical or indexed data without touching the target's current infrastructure.
- **Command Line is King:** While graphical tools exist, the CLI (Command Prompt/Terminal) is preferred for recon because it is faster, scriptable, and uses fewer resources.

## Learning Objectives

- Differentiate between Information Disclosure and Sensitive Data Exposure.
- Understand the critical distinction between Active and Passive reconnaissance.
- Learn how to use industry-standard tools for network, directory, and domain enumeration.
- Grasp the basics of OSINT and the vast sources of public information available.

## Background

Before a penetration tester attempts to exploit a system, they must understand it. This phase, called Reconnaissance or Information Gathering, is often the longest part of an engagement. Attackers look for misconfigurations (like Directory Listing), exposed secrets (like API keys in code), or historical data (like old subdomains that still resolve). Defenders must understand these techniques to ensure they are not leaking unnecessary data to the public internet.

## Key Concepts

### 1. Information Disclosure vs. Sensitive Data Exposure
**General Explanation:** 
- **Information Disclosure:** When a system accidentally reveals information that could be used by an attacker (e.g., verbose error messages, directory listing, debug info). It doesn't necessarily expose user data, but it gives the attacker a map of the system.
- **Sensitive Data Exposure:** A failure to protect confidential data (e.g., storing passwords in plaintext, transmitting credit card numbers over unencrypted HTTP). 
**Baby Talk Explanation:** 
- **Information Disclosure:** You accidentally leave a blueprint of your house's security system on the sidewalk. A robber finds it and knows exactly where the cameras are.
- **Sensitive Data Exposure:** You leave the actual safe full of money wide open on your front porch.

### 2. Active vs. Passive Reconnaissance
**General Explanation:** 
- **Active Recon:** Directly interacting with the target system (e.g., scanning ports, fuzzing directories). This will trigger alarms and leave logs on the target's servers.
- **Passive Recon:** Gathering information from third-party sources without touching the target (e.g., searching public databases, reading DNS records). 
**Baby Talk Explanation:** 
- **Active:** Walking up to the house and rattling the doorknobs to see if they are locked.
- **Passive:** Sitting in a car across the street, watching the house with binoculars, and checking public city records to see who owns it.

### 3. Search Engine Mechanics (Crawling & Indexing)
**General Explanation:** Search engines operate by using automated bots (spiders/crawlers) to browse the web (Crawling), analyze the content (Parsing), store it in a massive database (Indexing), and use algorithms to rank the results based on user queries.
**Baby Talk Explanation:** Imagine a librarian who reads every single book in the world, writes down a summary of each book on an index card, and puts them in a giant filing cabinet. When you ask for a book about "hacking," they instantly look through their filing cabinet (index) rather than re-reading every book.

## Practical Exercises & Tool Usage

*Note: The commands below are structural examples. Always ensure you have authorization before scanning any target.*

### The Command Prompt (CLI) in Recon
Security professionals prefer the Command Prompt/Terminal over Graphical User Interfaces (GUIs) because CLI tools consume less memory, can be automated via scripts (Bash/Python), and provide raw, parseable output.

### 1. Active Reconnaissance Tools

#### Network & Port Scanning
- **Nmap (Network Mapper):** The industry standard for network discovery. It sends packets to target IPs/ports and analyzes the responses.
  - *State Definitions:* `Open` (service is listening), `Filtered` (blocked by a firewall/restriction).
  - *Example Usage:* `nmap -sV example.com` (Note: Do not include `http://` when scanning domains).
- **Nuclei:** A fast, template-based vulnerability scanner. It uses YAML templates to check for specific known vulnerabilities (CVEs) and misconfigurations.
  - *Template Source:* [nuclei-templates](https://github.com/projectdiscovery/nuclei-templates)
  - *Example Usage:* `nuclei -u <URL_TARGET> -t <PATH_FILE_YAML>`
- **Naabu:** A fast port scanner optimized for reliability. It sends SYN/CONNECT/UDP probes directly to target IPs to enumerate open ports.
  - *Example Usage:* `naabu -host <ip/domain>`

#### Directory Fuzzing
*Finding hidden directories often leads to Information Disclosure via misconfigured Directory Listing.*
- **dirsearch:** A Python tool used to brute-force web servers and discover hidden files and directories.
  - *Example Usage:* `dirsearch.py -u <URL> -e <extensions>` (e.g., `-e php,txt,bak`)
- **FFUF (Fuzz Faster U Fool):** An extremely fast web fuzzer written in Go. Used for discovering directories, virtual hosts, and parameter values.
- **GoBuster:** A high-performance directory/file, DNS, and virtual host brute-forcing tool.

### 2. Passive Reconnaissance Tools

> **Important Note:** Passive tools can quickly become Active. If you use `Shodan` to find an IP, and then click the IP to visit the web page, you have transitioned from Passive to Active recon.

#### URL & History Scanning
- **GAU (GetAllUrls):** Fetches known URLs from third-party sources like AlienVault OTX, Wayback Machine, Common Crawl, and URLScan. It reveals historical endpoints that might still exist on the server.
- **Wayback Machine:** A digital archive of the web. It stores snapshots of websites over time, allowing you to see deleted pages or old vulnerabilities.

#### Device & IoT Lookup
- **Shodan:** Often called the "search engine for the Internet of Things (IoT)." It scans the internet for connected devices (CCTV, servers, routers) and indexes their banners and open ports.
- **Censys:** Similar to Shodan, it provides detailed information about internet-connected hosts and their certificates.
- **Google Dorking:** Using advanced Google search operators to find sensitive data exposed on the web.
  - *Database:* The [Google Hacking Database (GHDB)](https://www.exploit-db.com/google-hacking-database) contains lists of dorks like `inurl:`, `filetype:`, `intitle:`.

#### Domain and Sub-domain Enumeration
- **whois:** Queries databases to retrieve registration information about internet domains (owner, contact, name servers).
- **Sublist3r & Subfinder:** Tools that enumerate subdomains (e.g., `dev.example.com`, `mail.example.com`) using search engines and public datasets.
- **DNSDumpster:** A free online research tool that maps out a domain's DNS infrastructure visually.

## Challenges Encountered

### Challenge: Transitioning from Passive to Active Unintentionally
- **The Issue:** During OSINT gathering, it is easy to accidentally interact with the target, turning a passive scan into an active one.
- **Root Cause:** Clicking links in search results, resolving subdomains directly in the browser, or using tools that perform DNS resolution against the target's own servers.
- **Resolution (Mentor Note):** When performing passive recon, use a VPN or a burner virtual machine. If you find an interesting subdomain using `Subfinder`, do not immediately navigate to it in your browser. Record the data, and only interact with it when you are ready to begin the Active phase of your engagement.

## Lessons Learned

- Information Disclosure provides the blueprint; Sensitive Data Exposure provides the loot. Both must be mitigated.
- The distinction between Active and Passive recon is critical for legal and operational security reasons.
- The Command Line Interface is essential for efficient, automatable reconnaissance.
- There is no single "magic" OSINT tool. Professionals rely on a framework of different tools (like [OSINT Framework](https://osintframework.com/)) depending on the specific intelligence requirement.

## Best Practices

- **Scope Verification:** Always double-check your target IP addresses and domains. Running `nmap` against the wrong IP can have legal consequences.
- **Use Wordlists Wisely:** Directory fuzzing is only as good as your wordlist. Use standard lists like `SecLists` for comprehensive coverage.
- **Limit Noise:** Active scanning is noisy. Defenders will see it. Ensure your client or employer is aware of the scanning timeframe.

## Common Mistakes

- **Including Protocols in Nmap:** Beginners often run `nmap http://example.com`. Nmap expects a hostname or IP, not a URL. This will cause the scan to fail.
- **Assuming Passive Means Invisible:** While you aren't touching the target, your searches on Shodan or GAU are logged by those third-party services.
- **Ignoring Historical Data:** Deleting a vulnerable page from your live website does not mean it's gone. Wayback Machine and search engine caches might still hold the sensitive data.

## Further Reading

- [OSINT Framework](https://osintframework.com/) (Interactive diagram of OSINT tools)
- [Google Hacking Database (GHDB)](https://www.exploit-db.com/google-hacking-database)
- [Nmap Official Documentation](https://nmap.org/book/man.html)
- [ProjectDiscovery Tools (Nuclei, Naabu, Subfinder)](https://github.com/projectdiscovery)

## Summary

Information gathering is the foundation of both offensive and defensive cybersecurity. By understanding how data is leaked (Information Disclosure) and how attackers map infrastructure using Active and Passive tools, security professionals can better secure their environments. Mastery of CLI tools like Nmap, Nuclei, and GoBuster, combined with an understanding of OSINT frameworks, equips a professional to find vulnerabilities before malicious actors do.