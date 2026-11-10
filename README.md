# PENETRATION TESTING REPORT
## FOOTPRINTING & NETWORK SCANNING PHASES

### W2-PM-FINAL | CYBERSECURITY | NETWORKWALKS

**Pentester Name:** Sanyam Maurya  
**Program:** Cybersecurity Internship – Networkwalks  
**Date:** 10 November 2026  
**Modules Completed:**
- W2-PM1 – Multiple Kali Linux Tools
- W2-PM5 – Zenmap Scanning

**Client / Target:**
1. Networkwalks – `networkwalks.com`
2. Personal Local LAN Network

**Permission Secured:** Yes, as stated in the practical scope.

**Phases Covered:**
- Phase 1: Reconnaissance & Footprinting
- Phase 2: Scanning & Network Discovery
- Phase 3–5: Not covered in this practical

---

# 1. Liability Disclaimer

The activities documented in this report were performed as part of my cybersecurity internship and practical learning exercises. Testing was limited to systems and devices within the authorized scope or personally owned infrastructure.

The information presented in this report is intended for educational and cybersecurity research purposes only. Unauthorized access, scanning, or testing of systems without appropriate permission may violate applicable laws and regulations.

The author and training organization are not responsible for misuse of the information contained in this report. All security testing activities must be conducted responsibly and within an approved scope.

# 2. Introduction

This report documents two practical modules completed during Week 02 of my Cybersecurity Internship at Networkwalks.

The first module, W2-PM1, focused on footprinting and reconnaissance of the `networkwalks.com` domain using multiple Kali Linux tools. The second module, W2-PM5, involved scanning my own local network using Zenmap.

These exercises demonstrate two important stages of a penetration testing engagement: gathering publicly available information about a target and identifying active hosts within a network.

All reconnaissance commands were executed in Kali Linux, while network scanning activities were performed on a Windows PC using Zenmap.

Each activity is documented with its objective, command, observed results, security relevance, and supporting evidence.

# 3. Tools Used

The following tools and utilities were used during the practical exercises.

| Tool | Purpose |
|---|---|
| Kali Linux | Operating system used for reconnaissance activities |
| WHOIS | Retrieves domain registration details, registration dates, and name servers |
| WhatWeb | Identifies website technologies, CMS, plugins, and server information |
| NSLookup | Resolves domain names into IP addresses using DNS |
| cURL (-I) | Retrieves and analyzes HTTP response headers |
| WAFW00F | Detects Web Application Firewall technology |
| DNSRecon | Enumerates DNS records such as NS, MX, SPF, TXT, and SRV |
| Zenmap (Nmap GUI) | Discovers live hosts and identifies network devices |
| Windows CMD | Identifies local IP configuration and network subnet |

# 4. Activities Performed

## 4.1 Footprinting & Reconnaissance

I performed reconnaissance against the `networkwalks.com` domain using six Kali Linux tools: WHOIS, WhatWeb, NSLookup, cURL, WAFW00F, and DNSRecon.

Each tool was used to collect a different category of publicly available information about the target.

### 4.1.1 WHOIS

WHOIS was used to retrieve publicly available domain registration information and identify the domain's name servers.

**Command Used:**

```bash
whois networkwalks.com
```

**Information Observed:**
- Domain registration information
- Registrar details
- Registration and expiry dates
- Name server information
- Publicly available registration contacts

**Security Relevance:**

Domain registration information helps identify ownership-related details and hosting infrastructure. Name server information can also provide useful context for further infrastructure reconnaissance.

**Evidence:** WHOIS command output screenshot.

### 4.1.2 WhatWeb

WhatWeb was used to identify and fingerprint the technologies used by the target website.

**Command Used:**

```bash
whatweb networkwalks.com
```

**Information Observed:**
- WordPress 7.1.4
- WP Download Manager 3.3.76
- Apache web server information
- Website technologies and other identifiable components

**Security Relevance:**

Technology fingerprinting helps identify the software components used by a website. Identified versions can be reviewed against available security advisories to determine whether further assessment is required.

**Evidence:** WhatWeb output screenshot.

### 4.1.3 NSLookup

NSLookup was used to resolve the target domain name into its corresponding IP address.

**Command Used:**

```bash
nslookup networkwalks.com
```

**Alternative Command:**

```bash
nslookup -vc networkwalks.com 8.8.8.8
```

**Information Observed:**

The domain resolved to the following IP address:

`192.232.216.135`

**Security Relevance:**

DNS resolution provides information about the network location of a domain and supports further infrastructure mapping and analysis.

**Evidence:** NSLookup output screenshot.

### 4.1.4 cURL

cURL was used with the `-I` option to inspect the HTTP response headers returned by the target website.

**Command Used:**

```bash
curl -I https://networkwalks.com
```

**Information Observed:**
- HTTP response headers
- Server-related information
- Caching-related information
- WordPress REST API endpoint visibility: `/wp-json/`

**Security Relevance:**

HTTP response headers may reveal technical information about the web server and application environment. This information can help security professionals understand the technologies and interfaces exposed by a web application.

**Evidence:** cURL response header screenshot.

### 4.1.5 WAFW00F

WAFW00F was used to identify whether a Web Application Firewall was protecting the target website.

**Command Used:**

```bash
wafw00f networkwalks.com
```

**Information Observed:**

The output identified:

**ModSecurity (SpiderLabs)**

**Security Relevance:**

Identifying a Web Application Firewall helps security testers understand the protective technologies deployed in front of a web application and consider them during an authorized security assessment.

**Evidence:** WAFW00F output screenshot.

### 4.1.6 DNSRecon

DNSRecon was used to enumerate DNS records and collect information about the target's DNS infrastructure.

**Command Used:**

```bash
dnsrecon -d networkwalks.com
```

**Information Observed:**
- Name server records
- Mail server records
- SPF and TXT records
- Service-related DNS records
- DNS infrastructure information

The practical notes also recorded BIND 9.16.23 as DNS software information.

**Security Relevance:**

DNS enumeration helps security professionals understand domain services, mail infrastructure, and associated network components. This information contributes to a broader view of the target's external footprint.

**Evidence:** DNSRecon output screenshot.

---

## 4.2 Network Scanning with Zenmap

For the second activity, I used Zenmap to perform network discovery on my own local network.

The main objectives were to identify the local IP address and subnet, discover active hosts, review their IP and MAC addresses, and understand the network topology.

### 4.2.1 Local Network Identification

I first used the Windows Command Prompt to identify the local IP address and subnet configuration.

**Command Used:**

```cmd
ipconfig
```

The output helped identify the local IPv4 address and network configuration required for the scanning activity.

### 4.2.2 Zenmap Configuration

After identifying the local subnet, I opened Zenmap and configured the scan.

**Scanning Procedure:**

1. Opened Zenmap on the Windows system.
2. Entered the local network subnet as the target.
3. Selected the Ping Scan profile.
4. Started the network discovery process.
5. Reviewed the discovered hosts and scan output.

### 4.2.3 Host Discovery Results

The practical notes recorded the following example host addresses:

| Host | IP Address |
|---|---|
| Host 1 | `10.251.186.123` |
| Host 2 | `10.251.186.152` |

The scan output also provided MAC address information for discovered devices.

*Note: These addresses are taken from the practical notes. Verify them against the original Zenmap output before final submission.*

### 4.2.4 Network Topology

After completing the host discovery scan, the Zenmap Topology section was used to visualize the discovered network devices.

The topology view helps present the relationship between discovered hosts and provides a graphical overview of the network.

**Activities Completed:**
- Opened the Topology tab.
- Reviewed the discovered hosts.
- Enabled the topology legend.
- Examined the graphical network layout.
- Saved the topology output for documentation.

**Evidence:** Zenmap scan results and topology screenshots.

# 5. Risk Analysis / Impact

Based on the information collected during the footprinting and network scanning activities, the following potential risks and observations were documented.

| # | Risk / Finding | Evidence / Observation | Potential Impact | Risk Level |
|---|---|---|---|---|
| 1 | Web technology information exposed | WhatWeb identified WordPress and WP Download Manager | May help identify software components requiring further security review | Medium |
| 2 | Server IP address identifiable | NSLookup resolved the domain to 192.232.216.135 | Provides information about the network location of the web service | Low |
| 3 | HTTP technical information exposed | cURL returned HTTP response headers and exposed `/wp-json/` | May assist technology fingerprinting and further enumeration | Low |
| 4 | WAF technology identifiable | WAFW00F identified ModSecurity (SpiderLabs) | Reveals information about the web application's security architecture | Low |
| 5 | DNS infrastructure information exposed | DNSRecon identified DNS, mail, and service-related records | Helps build a broader infrastructure profile | Medium |
| 6 | Multiple live hosts visible on local network | Zenmap identified active hosts in the local network | Unknown or unauthorized devices may potentially be present | Medium |

**Risk Level Key:**
- Critical – Very high security impact
- High – Significant security impact
- Medium – Moderate security concern
- Low – Limited security concern

**Assessment Limitation:**

The observations above are based on reconnaissance and network discovery activities. They are not confirmed vulnerabilities.

The practical exercises primarily involved information gathering and host discovery. No exploitation or vulnerability validation was performed as part of these modules.

The presence of information such as a software version, IP address, HTTP header, or DNS record does not automatically mean that a system is vulnerable. Further authorized security testing would be required to confirm any actual vulnerability.

# 6. Recommendations

Based on the observations from these activities, the following security improvements are recommended:

### 1. Review Publicly Exposed Technology Information

Organizations should regularly review publicly accessible information about their website technologies, CMS platforms, and plugins.

### 2. Keep Software Updated

CMS platforms, plugins, and other web technologies should be regularly updated and reviewed against current security advisories.

### 3. Review HTTP Headers

HTTP response headers should be reviewed to identify and minimize unnecessary technical information disclosure.

### 4. Review DNS Records Regularly

DNS records should be checked periodically to ensure that only required and valid information and services are publicly exposed.

### 5. Properly Configure and Monitor the WAF

The Web Application Firewall should be properly configured, maintained, and monitored to support web application protection.

### 6. Perform Regular Internal Network Discovery

Organizations should periodically scan their own networks to identify active devices and maintain network visibility.

### 7. Investigate Unknown Devices

Any unexpected device discovered during network scanning should be investigated and verified.

### 8. Maintain Network Documentation

Network topology, device information, and network configuration details should be documented and updated regularly.

### 9. Perform Security Testing with Authorization

Reconnaissance and scanning should only be performed against systems and networks where appropriate authorization has been provided.

# 7. Conclusion

During Week 02 of my Cybersecurity Internship at Networkwalks, I completed practical activities covering Footprinting, Reconnaissance, and Network Scanning.

In the reconnaissance activity, I used six Kali Linux tools to collect information about the target domain. I learned how WHOIS provides domain registration details, WhatWeb identifies website technologies, NSLookup resolves domain names, cURL inspects HTTP response headers, WAFW00F identifies WAF technology, and DNSRecon collects DNS infrastructure information.

In the network scanning activity, I used Zenmap to identify local network configuration and discover active hosts. I also reviewed IP and MAC address information and explored the graphical network topology.

These exercises improved my understanding of the initial stages of penetration testing and demonstrated how information gathering and network discovery contribute to a structured security assessment.

I also learned the importance of documenting technical activities clearly, analyzing collected information, and distinguishing potential security observations from confirmed vulnerabilities.

Finally, these practical exercises reinforced the importance of conducting reconnaissance and network scanning within an authorized scope.

# 8. Evidences Collected

The following screenshots should be attached to demonstrate the practical activities performed during the internship.

### 8.1 WHOIS – Domain Registration Information

_Add your WHOIS terminal screenshot here._

### 8.2 WhatWeb – Website Technology Fingerprinting

_Add your WhatWeb output screenshot here._

### 8.3 NSLookup – DNS Resolution

_Add your NSLookup output screenshot here._

### 8.4 cURL – HTTP Response Header Analysis

_Add your cURL output screenshot here._

### 8.5 WAFW00F – Firewall Detection

_Add your WAFW00F output screenshot here._

### 8.6 DNSRecon – DNS Enumeration

_Add your DNSRecon output screenshot here._

### 8.7 Zenmap – Network Discovery

_Add your Zenmap host discovery screenshot here._

### 8.8 Zenmap – Network Topology

_Add your Zenmap topology screenshot here._

---

## 👤 Author

**Sanyam Maurya**  
Cybersecurity Intern  
Networkwalks

**Technical Focus:** VAPT | Web Security | Reconnaissance | Network Security

---

## 📌 Project Information

| Project Details | Information |
|---|---|
| Program Name | Cybersecurity Internship at Networkwalks |
| Internship Week | 02 |
| Project | Footprinting & Network Scanning |
| Modules | W2-PM1 and W2-PM5 |
| Repository | GitHub |
| Author | Sanyam Maurya |

---

**END OF REPORT**
