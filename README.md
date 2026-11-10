# 🤖 PENETRATION TESTING REPORT
## FOOTPRINTING & RECONNAISSANCE AND NETWORK SCANNING

<div align="center">

![Cybersecurity](https://img.shields.io/badge/Skill-Cybersecurity-red)
![Penetration Testing](https://img.shields.io/badge/Focus-Penetration%20Testing-critical)
![Kali Linux](https://img.shields.io/badge/Platform-Kali%20Linux-black)
![Windows](https://img.shields.io/badge/Platform-Windows-blue)
![Networkwalks](https://img.shields.io/badge/Internship-Networkwalks-orange)

**👨‍💻 Pentester: Sanyam Maurya**

---

**W2-PM-FINAL | CYBERSECURITY | NETWORKWALKS**

</div>

---

## 🚧 Project Overview

| Field | Detail |
|---|---|
| Pentester | Sanyam Maurya |
| Program | Cybersecurity Internship – Networkwalks |
| Internship Week | Week 02 |
| Date | 10 November 2026 |
| Module 1 | W2-PM1 – Multiple Kali Linux Tools |
| Module 2 | W2-PM5 – Zenmap Scanning |
| Target Domain | `networkwalks.com` |
| Network Scanning Target | `10.42.185.121` |
| Environment | Kali Linux and Windows |
| Assessment Phases | Footprinting, Reconnaissance and Host Discovery |

# 1. Liability Disclaimer

This report documents practical cybersecurity activities performed as part of my Cybersecurity Internship at Networkwalks.

The activities described include domain information gathering, website technology fingerprinting, DNS enumeration, HTTP response header analysis, Web Application Firewall detection, and local host discovery.

All security testing must be conducted within an authorized scope and with appropriate permission from the relevant system owner.

This report is intended for educational, training, and professional documentation purposes. The observations included in this document are based on the outputs collected during the practical exercises. They should not automatically be interpreted as confirmed security vulnerabilities.

The author is not responsible for unauthorized use or misuse of the information presented in this report.

# 2. Introduction

Reconnaissance and footprinting are the initial stages of a penetration testing engagement. These activities involve gathering information about a target's domain, DNS infrastructure, web technologies, server configuration, and publicly accessible services.

During Week 02 of my Cybersecurity Internship at Networkwalks, I completed two practical modules focused on information gathering and network discovery.

**Module 1 – W2-PM1: Multiple Kali Linux Tools**

This module focused on using different Kali Linux utilities to collect domain and website-related information. The exercises included WHOIS lookup, website technology fingerprinting, DNS resolution, HTTP response analysis, WAF detection, and DNS enumeration.

**Module 2 – W2-PM5: Zenmap Scanning**

This module focused on using Zenmap to perform a Ping Scan against a local network host, identify whether the host was active, and understand basic network discovery.

The practical exercises helped strengthen my understanding of the information-gathering and host-discovery phases of penetration testing.

# 3. Tools Used

The following tools and technologies were used during the practical exercises.

| Tool | Purpose |
|---|---|
| Kali Linux | Operating system for reconnaissance activities |
| WHOIS | Collects domain registration and registrar information |
| WhatWeb | Identifies website technologies and software fingerprints |
| NSLookup | Resolves domain names and retrieves DNS information |
| cURL | Retrieves and analyzes HTTP response headers |
| WAFW00F | Detects Web Application Firewall technologies |
| DNSRecon | Enumerates DNS records and related infrastructure |
| Zenmap | Graphical interface for Nmap-based network scanning |
| Windows CMD | Checks local IP and network configuration |

# 4. Activities Performed

## 4.1 Footprinting & Reconnaissance Using Kali Linux

### 4.1.1 WHOIS – Domain Information Gathering

**Objective:** To retrieve publicly available domain registration information and identify the registrar and associated name servers.

**Command Executed:**

```bash
whois networkwalks.com
```

**Information Observed:**

The WHOIS output provided the following information:

| Parameter | Observed Result |
|---|---|
| Domain Name | `NETWORKWALKS.COM` |
| Registrar | GoDaddy.com, LLC |
| WHOIS Server | `whois.godaddy.com` |
| Creation Date | 06 November 2019 |
| Updated Date | 10 November 2025 |
| Registry Expiry Date | 06 November 2027 |
| Name Server 1 | `NS6135.HOSTGATOR.COM` |
| Name Server 2 | `NS6136.HOSTGATOR.COM` |
| DNSSEC | Unsigned |

**Security Relevance:**

WHOIS information helps identify domain registration details, registrar information, and name server configuration. This information can provide an initial understanding of the target's domain infrastructure.

**Observation:**

The domain was registered through GoDaddy, while the configured name servers belong to HostGator.

### 4.1.2 WhatWeb – Website Technology Fingerprinting

**Objective:** To identify the technologies, CMS, plugins, and web server information associated with the target website.

**Command Executed:**

```bash
whatweb networkwalks.com
```

**Information Observed:**

| Parameter | Observed Result |
|---|---|
| Web Server | Apache |
| CMS | WordPress |
| WordPress Version | 7.1.4 |
| Plugin | WP Download Manager |
| Plugin Version | 3.3.76 |
| Server IP | `192.232.216.135` |
| Country Detection | United States |
| Google Tag Manager | Identified |
| Bootstrap | Identified |
| HTML5 | Identified |
| Open Graph Protocol | Identified |

**Additional Observation:**

The initial HTTP request returned a `301 Moved Permanently` response and redirected to the HTTPS version of the website. The HTTPS endpoint returned a `200 OK` response.

**Security Relevance:**

Technology fingerprinting helps identify the software components and technologies used by a web application. The identified versions can be reviewed against relevant security advisories to determine whether further security testing is necessary.

**Observation:**

WordPress and WP Download Manager were identified through the WhatWeb fingerprinting process. Their presence alone does not confirm a vulnerability.

### 4.1.3 NSLookup – DNS Resolution

**Objective:** To resolve the target domain into its associated IPv4 and IPv6 addresses.

**Command Executed:**

```bash
nslookup networkwalks.com
```

**Information Observed:**

| Parameter | Result |
|---|---|
| DNS Server | `10.42.185.12` |
| DNS Server Port | `53` |
| Domain | `networkwalks.com` |
| IPv4 Address | `192.232.216.135` |
| IPv6 Address | `64:ff9b::c0e8:d887` |

**Security Relevance:**

DNS resolution provides information about the IP addresses associated with a domain. This information supports infrastructure identification and further reconnaissance activities.

**Observation:**

The DNS lookup returned both an IPv4 address and an IPv6-format address using the `64:ff9b::` prefix.

### 4.1.4 cURL – HTTP Response Header Analysis

**Objective:** To retrieve and inspect HTTP response headers returned by the target website.

**Command Executed:**

```bash
curl -I networkwalks.com
```

**Information Observed:**

| HTTP Header / Parameter | Observed Result |
|---|---|
| HTTP Status | `301 Moved Permanently` |
| Server | Apache |
| Date | 10 November 2026 |
| Location | `https://networkwalks.com/` |
| X-Redirect-By | WordPress – Really Simple Security |
| X-Nginx-Cache | WordPress |
| Content-Type | `text/html; charset=UTF-8` |
| Connection | Upgrade |
| Upgrade | `h2,h2c` |

**Security Relevance:**

HTTP response header analysis helps identify server information, redirect behavior, caching information, and application-related details exposed through HTTP communication.

**Observation:**

The HTTP endpoint returned a permanent redirect to the HTTPS endpoint. The response also disclosed Apache server information and WordPress-related redirect details.

This behavior does not, by itself, indicate a security vulnerability.

### 4.1.5 WAFW00F – Web Application Firewall Detection

**Objective:** To identify whether a Web Application Firewall is deployed in front of the target website.

**Command Executed:**

```bash
wafw00f networkwalks.com
```

**Information Observed:**

| Parameter | Result |
|---|---|
| Tool | WAFW00F |
| Tool Version | 2.3.1 |
| Target | `https://networkwalks.com` |
| WAF Detected | ModSecurity |
| WAF Provider | SpiderLabs |
| Number of Requests | 2 |

**Detection Result:**

`The site https://networkwalks.com is behind ModSecurity (SpiderLabs) WAF.`

**Security Relevance:**

WAF detection helps security professionals understand the protective technologies deployed in front of a web application.

**Observation:**

WAFW00F identified ModSecurity (SpiderLabs) as the Web Application Firewall technology associated with the target.

### 4.1.6 DNSRecon – DNS Enumeration

**Objective:** To enumerate DNS records and collect information about the target domain's DNS infrastructure.

**Command Executed:**

```bash
dnsrecon -d networkwalks.com
```

**Information Observed:**

The DNSRecon output reported 16 records during enumeration.

| Record Type | Observed Information |
|---|---|
| SOA | `ns6135.hostgator.com` |
| NS | `ns6135.hostgator.com` |
| NS | `ns6136.hostgator.com` |
| A | `192.232.216.135` |
| AAAA | `64:ff9b::c0e8:d887` |
| MX | `mail.networkwalks.com` |
| SPF TXT | SPF policy record identified |
| TXT | Google site verification record identified |
| SRV | Autodiscover service records identified |

**Additional DNS Information:**

- DNS software fingerprint: BIND `9.16.23-RH`
- Mail server: `mail.networkwalks.com`
- Total records reported: 16

**Security Relevance:**

DNS enumeration provides information about domain infrastructure, name servers, mail services, and other associated records. This information helps security professionals build an understanding of the target's external infrastructure.

**Observation:**

DNSRecon successfully completed the enumeration process and reported 16 records, including NS, SOA, A, AAAA, MX, TXT, and SRV information.

# 5. Risk Analysis / Impact

Based on the information collected during the reconnaissance and network scanning exercises, the following observations were documented.

| No. | Observation | Evidence Source | Potential Security Impact |
|---|---|---|---|
| 1 | Domain registration and name server details exposed | WHOIS | Provides publicly available domain ownership and infrastructure information |
| 2 | Website technologies and software versions identified | WhatWeb | May help identify components requiring further security review |
| 3 | IPv4 and IPv6 addresses resolved | NSLookup | Provides information about the target's network addressing |
| 4 | HTTP response headers disclose server and application information | cURL | May assist technology fingerprinting |
| 5 | ModSecurity WAF technology identified | WAFW00F | Reveals information about deployed web protection technology |
| 6 | DNS infrastructure and service records enumerated | DNSRecon | Helps map domain, mail, and service infrastructure |
| 7 | One active host identified | Zenmap | Confirms that the scanned host responded to the discovery probe |

**Risk Assessment Notes:**

The above observations represent information collected during reconnaissance and host discovery. They should not be considered confirmed vulnerabilities.

No exploitation, authentication testing, or vulnerability validation was performed during these practical exercises.

The identification of software versions, server information, DNS records, or WAF technology does not automatically establish a security weakness. Further authorized testing would be required to determine whether any actual vulnerability exists.

# 6. Recommendations

Based on the observations collected during the practical exercises, the following security recommendations are suggested.

### 6.1 Review Publicly Exposed Domain Information

Organizations should periodically review publicly accessible domain registration and DNS information to ensure that unnecessary information is not exposed.

### 6.2 Maintain Updated Website Technologies

CMS platforms, plugins, and server-side components should be regularly updated. Identified software versions should be reviewed against applicable security advisories.

### 6.3 Review HTTP Response Headers

HTTP response headers should be reviewed to minimize unnecessary disclosure of technical information about the application and hosting environment.

### 6.4 Maintain Proper DNS Configuration

DNS records should be periodically reviewed to ensure that only valid and required records are configured.

### 6.5 Monitor WAF Configuration

The Web Application Firewall should be properly configured, updated, and monitored to support web application protection.

### 6.6 Perform Regular Network Discovery

Organizations should periodically perform authorized internal network discovery to maintain visibility into active devices and network assets.

### 6.7 Verify Unknown Network Devices

Any unfamiliar device identified during network discovery should be investigated to determine whether it is authorized to connect to the network.

### 6.8 Maintain Security Documentation

Domain information, DNS configurations, network assets, and security observations should be documented and reviewed regularly.

# 7. Conclusion

During Week 02 of my Cybersecurity Internship at Networkwalks, I completed practical exercises focused on Footprinting, Reconnaissance, and Network Scanning.

In the first module, I used six Kali Linux tools to collect and analyze information associated with the `networkwalks.com` domain.

WHOIS helped identify domain registration and name server details. WhatWeb identified website technologies and software components. NSLookup resolved the domain into IPv4 and IPv6 addresses. cURL was used to inspect HTTP response headers, WAFW00F identified ModSecurity (SpiderLabs), and DNSRecon collected DNS infrastructure information.

In the second module, I used Zenmap to perform a Ping Scan against the target host `10.42.185.121`. The scan successfully identified the host as active, with one IP address scanned and one host reported up.

These practical exercises strengthened my understanding of information gathering, website technology fingerprinting, DNS enumeration, HTTP response analysis, WAF detection, and basic network host discovery.

Overall, the exercises provided valuable hands-on exposure to the initial stages of a penetration testing engagement and improved my ability to document technical observations in a structured manner.

# 8. Evidences Collected

The following screenshots provide supporting evidence of the practical activities performed during Week 02.

### 8.1 WHOIS – Domain Information Gathering

The screenshot demonstrates domain registration details, registrar information, domain dates, and name server records collected using WHOIS.

**Evidence:** WHOIS terminal output.

### 8.2 WhatWeb – Website Technology Fingerprinting

The screenshot demonstrates the identification of Apache, WordPress 7.1.4, WP Download Manager 3.3.76, and other website technologies.

**Evidence:** WhatWeb terminal output.

### 8.3 NSLookup – DNS Resolution

The screenshot demonstrates the DNS resolution of `networkwalks.com`, including its IPv4 and IPv6-format addresses.

**Evidence:** NSLookup terminal output.

### 8.4 cURL – HTTP Response Header Analysis

The screenshot demonstrates the HTTP 301 redirect response, Apache server information, and redirect destination.

**Evidence:** cURL terminal output.

### 8.5 WAFW00F – Web Application Firewall Detection

The screenshot demonstrates the identification of ModSecurity (SpiderLabs) as the WAF technology.

**Evidence:** WAFW00F terminal output.

### 8.6 DNSRecon – DNS Enumeration

The screenshot demonstrates DNS enumeration results, including NS, SOA, A, AAAA, MX, TXT, and SRV records, with 16 records reported.

**Evidence:** DNSRecon terminal output.

### 8.7 Zenmap – Network Host Discovery

The screenshot demonstrates the Ping Scan performed against `10.42.185.121`.

**Evidence:** Zenmap scan output showing:

- Target IP: `10.42.185.121`
- Scan command: `nmap -sn 10.42.185.121`
- Host status: Up
- IP addresses scanned: 1
- Hosts up: 1
- Scan duration: 0.20 seconds
- Nmap version: 7.92

---

## 👨‍💻 Author Information

**Name:** Sanyam Maurya  
**Role:** Cybersecurity Intern  
**Organization:** Networkwalks  
**Technical Focus:** VAPT | Reconnaissance | Web Security | Network Security

---

## 📌 Project Summary

| Field | Details |
|---|---|
| Internship | Cybersecurity Internship |
| Organization | Networkwalks |
| Week | 02 |
| Modules | W2-PM1 and W2-PM5 |
| Project Title | Footprinting, Reconnaissance & Network Scanning |
| Primary Environment | Kali Linux and Windows |
| Reconnaissance Tools | WHOIS, WhatWeb, NSLookup, cURL, WAFW00F, DNSRecon |
| Network Scanning Tool | Zenmap |
| Author | Sanyam Maurya |

---

<div align="center">

**LEARNING • PRACTICING • SECURING**

**END OF REPORT**

</div>
