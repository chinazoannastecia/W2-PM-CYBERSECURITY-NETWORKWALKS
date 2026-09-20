# W2-PM-CYBERSECURITY-NETWORKWALKS
FOOTPRINTING &amp; NETWORK SCANNING PHASES
# PENETRATION TESTING REPORT

## Footprinting & Network Scanning Phases
### W2-PM | CYBERSECURITY | NETWORKWALKS

| Field | Detail |
| :--- | :--- |
| Pentester Name (Cybersecurity Professional) | Ugwuoke Annastecia |
| Program/Batch | B083-Networkwalks |
| Date | 20 September 2026 |
| Modules completed | W2-PM1 (Footprinting & Reconnissance Attacks with Multiple Kali Tools) W2-PM5 (Zenmap Scanning)
| Client/Target |1.networkwalks.com 2. My own local Wi-fi hotspot network |
| Permission | Yes - secured written permission |
| Phases covered | Phase 1: Reconnaissance & Footprinting<br>Phase 2: Scanning & Network Discovery<br>Phase 3-5: in progress |
| Tools Used | whois, whatweb, nslookup, curl, wafw00f, dnsrecon, zenmap |
| Summary | This report contains footprinting and scanning results for networkwalks.com |

1. ## **1. Liability Disclaimer**
 
Every task in this report was carried out either against networkwalks.com, for which the internship program already has documented written approval, or against a Wi-Fi network that belongs to me and that I administer myself. Nothing here is intended for anything beyond learning and personal skill-building. This document should not be used to target a system that has not been authorised for testing, that responsibility sits entirely with whoever chooses to do so, not with Networkwalks, the instructors, or me. Unauthorised access carries real legal consequences in most jurisdictions, whether or not any actual damage occurs.
## **2. Introduction**
This report documents the second week of my cybersecurity internship at Networkwalks, split across two hands-on exercises. The first (W2-PM1) focuses on footprinting the networkwalks.com domain using various Kali Linux command-line tools. The second (W2-PM5) focuses on scanning a network I control using Zenmap, the graphical front end for Nmap. Together, both exercises show the steps an attacker usually follows at the start of an engagement, starting with information that is already public and then moving to actively probing which hosts and services are reachable.

All activities below were executed from my Kali Linux terminal. For each tool, I documented the exact command I ran, the result I got, a screenshot of the actual session, and a short note on why that piece of information is important for profiling this target.
## 4. Activities Performed

### 4.1 Footprinting & Reconnaissance

I executed six different Kali Linux tools on networkwalks.com — WHOIS, WhatWeb, Nslookup, curl, WafW00f and DNSRecon. Each tool was used to collect a different type of public information about the target, from domain ownership to the technologies running on the web server.

**WHOIS** was the first step because domain registration information is usually the easiest place to start. The result showed the domain is hosted with GoDaddy.com, LLC, registered on 20 November 2019 and set to expire on 20 November 2027, last updated on 11 November 2021. The record has four client-side locks (clientDeleteProhibited, clientRenewProhibited, clientTransferProhibited, clientUpdateProhibited) which means the domain is protected from unauthorized changes. The Name Servers are NS6133.HOSTGATOR.COM and NS6134.HOSTGATOR.COM.
### 4.1.3 Nslookup

I used nslookup to find the IP address mapped to the domain networkwalks.com. This tool queries the DNS server directly and is useful for confirming where a website is hosted and what DNS resolver is being used.

I ran the command `nslookup networkwalks.com` and the query was resolved by Google's public DNS server at 8.8.8.8 on port 53. The result returned a non-authoritative answer showing that networkwalks.com points to IP address 192.232.216.135. This confirms the domain is active and publicly resolvable.

From this, I learned that footprinting with nslookup is important because it reveals the underlying IP of the target, which can be used for further enumeration of the hosting infrastructure.
### 4.1.5 WafW00f

I used WafW00f to detect if a Web Application Firewall (WAF) is protecting networkwalks.com. The tool sent 2 requests to https://networkwalks.com.

The result shows the site is behind **ModSecurity (SpiderLabs) WAF**. This means the website has a firewall filtering malicious traffic.
### 4.1.6 DNSRecon

I used DNSRecon for DNS enumeration on networkwalks.com. The tool started general enumeration for the domain.

The results showed:
- SOA record: ns6135.hostgator.com at 50.87.144.87
- NS records: ns6135.hostgator.com and ns6136.hostgator.com
- MX record: mail.networkwalks.com pointing to 192.232.216.135
- A record: networkwalks.com pointing to 192.232.216.135

This confirms the domain uses HostGator name servers and the same IP for mail and web hosting.

### 4.1.4 Curl

I used curl to fetch the HTTP response and HTML source of networkwalks.com. The command `curl -I https://networkwalks.com` returned the page header and meta tags.

The result shows the site uses WordPress with Yoast SEO plugin v27.9. The meta description states it specializes in Network training courses including Cisco CCNA, CCNP, Cybersecurity, Ethical Hacking, Python Programming and Linux. It also shows Open Graph tags like og:title "Networkwalks Academy" and og:type website.

This helps in footprinting because it reveals the CMS, SEO plugin version and the purpose of the website.




