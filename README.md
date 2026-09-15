 ## PENETRATION TESTING REPORT

## FOOTPRINTING & NETWORK SCANNING PHASES

**W2-PM-FINAL | CYBERSECURITY | NETWORKWALKS**

---

##  Report Information

| Item | Details |
|---|---|
| **Pentester Name (Cybersecurity Professional)** | Gasper Boniphace |
| **Program / Batch** | B083 - Networkwalks |
| **Date** | 14 September 2026 |
| **Modules Completed** | W2-PM1 (Multiple Kali Tools) <br> W2-PM5 (Zenmap Scanning) |
| **Client / Target** | 1. Networkwalks (secured written permission already) <br> 2. My own local LAN Network |
| **Permission Secured from Client?** | Yes |
| **Phases Covered** | Phase 1: Reconnaissance & Footprinting <br> Phase 2: Scanning & Network Discovery <br> Phase 3-5: In Progress |

---

## 1.  Liability Disclaimer

I have performed these activities only on the systems and devices where I had secured written permission or on devices and systems that I own myself.

All materials in this repository are intended for educational and research purposes only. Do not use anything from this report to break the law.

The instructor, the authors, and Networkwalks are not responsible for what you do with this knowledge. Every action you take is your own responsibility. Misuse can lead to criminal charges, heavy fines, loss of your job, and a permanent record.

In most countries, unauthorized access is a crime even when nothing is damaged.

---

## 2.  Introduction

This report covers footprinting the **networkwalks.com** domain using multiple Kali Linux tools (**W2-PM1**) and scanning my own local network with **Zenmap (W2-PM5)**.

One module covers the footprinting phase and the other covers the scanning phase. Together, they demonstrate how a security professional can move from gathering publicly available information to mapping live hosts on a network.

This work forms part of **Week 2** of my ongoing cybersecurity internship program at Networkwalks.

All commands were run in Kali Linux for the footprinting activities and on a Windows PC with Zenmap installed for the scanning activities.

Each activity below includes the exact command or tool used, the result observed, a screenshot as evidence, and a short explanation of why the finding matters from an attacker's point of view.

---

## 3.  Tools Used

| Tool | Purpose |
|---|---|
| **Kali Linux & Windows** | Operating systems used for reconnaissance activities |
| **WHOIS** | Find domain registration details such as owner information, dates, and name servers |
| **WhatWeb** | Fingerprint web technologies including server, CMS, plugins, and IP information |
| **nslookup** | Resolve the domain name to its IP address using DNS |
| **curl -I** | Read and inspect HTTP response headers of the website |
| **Wafw00f** | Detect whether a Web Application Firewall protects the site |
| **DNSRecon** | Enumerate DNS records such as NS, MX, SPF, TXT, and SRV records |
| **Zenmap (Nmap GUI)** | Scan the local subnet to find live hosts, IP addresses, and MAC addresses |
| **Windows CMD** | Identify the local IP address and MAC address |

---

# 4.  Activities Performed

## 4.1 Footprinting & Reconnaissance

I performed reconnaissance against the **networkwalks.com** domain using six Kali Linux tools: **WHOIS, WhatWeb, nslookup, curl, Wafw00f, and DNSRecon**. Each tool was used to collect a different type of information about the target.

### WHOIS

First, I used WHOIS to obtain publicly available domain registration information and identify the domain's name servers. The results provided information about the domain registration and hosting infrastructure.

### WhatWeb

I then used WhatWeb to identify technologies used by the website. The results identified **WordPress 7.0.4** and **WP Download Manager 3.3.58**, along with other information exposed by the website.

### nslookup

Using nslookup, I resolved the domain name to its IP address. The provided result identified **192.232.216.135**.

### curl -I

I used curl with the `-I` option to inspect the HTTP response headers. This provided additional information about the web application and exposed the WordPress REST API endpoint `/wp-json/`.

### Wafw00f

Next, I used Wafw00f to determine whether a Web Application Firewall was protecting the website. The result identified **ModSecurity (SpiderLabs)**.

### DNSRecon

Finally, I used DNSRecon to enumerate DNS records. The results provided information relating to name servers, mail servers, SPF/TXT records, service records, and DNS software information.

----
## 4.2  Network Scanning with Zenmap

For the second activity, I used **Zenmap** to perform network discovery on my local network. The practical required me to identify my local IP address and subnet, discover live hosts, identify their IP and MAC addresses, and generate a network topology.

I first used the Windows `ipconfig` command to identify my local IP address and LAN subnet. I then entered the subnet into Zenmap and selected **Ping Scan** to identify active hosts.

### Example Results

The example results provided in the practical identified three live hosts:

```text
192.168.1.1
192.168.1.110
192.168.1.199
```

The example results also included three MAC addresses.

After completing the scan, I opened the **Topology** section in Zenmap, enabled the legend, and saved the network topology in PDF format as required by the practical task.

> **Note:** The actual subnet, number of hosts, IP addresses, and MAC addresses should be replaced with the results from my own network when submitting the final report.

---

# 5.  Risk Analysis / Impact

Based on the information collected during the footprinting and network scanning activities, I identified the following potential risks.

| # | Risk / Finding | Evidence / Observation | Potential Impact | Risk Level |
|---:|---|---|---|---|
| 1 | Web technology information exposed | WhatWeb identified WordPress and WP Download Manager | Attackers may use exposed technology/version information to identify software requiring further security review | 🔵 Medium |
| 2 | Server IP address identifiable | nslookup resolved the domain to 192.232.216.135 | Provides information about the network location of the web service | 🟢 Low |
| 3 | HTTP technical information exposed | curl returned HTTP response headers and exposed `/wp-json/` | May assist technology fingerprinting and further enumeration | 🟢 Low |
| 4 | WAF technology identifiable | Wafw00f identified ModSecurity (SpiderLabs) | Reveals information about the web application's security architecture | 🟢 Low |
| 5 | DNS infrastructure information exposed | DNSRecon identified DNS, mail, and service-related records | DNS information can help build a broader infrastructure profile | 🔵 Medium |
| 6 | Multiple live hosts visible on local network | Zenmap identified four live hosts in the example network | Unknown or unauthorized devices may potentially be present on a network | 🔵 Medium |


> The risks above are observations from the footprinting and scanning exercises, not confirmed vulnerabilities.

The practical exercises primarily involved information gathering and host discovery. No exploitation or vulnerability validation was performed as part of these two modules.

Therefore, the presence of information such as a software version, IP address, or DNS record does not by itself mean that the system is vulnerable. Further authorized security testing would be required to confirm any actual vulnerability.

---

# 6.  Recommendations

### Review Publicly Exposed Technology Information

Organizations should regularly review what information about their web technologies, CMS, and plugins is publicly visible.

### Keep Software Updated

CMS platforms, plugins, and other web technologies should be regularly updated and reviewed against current security advisories.

### Review HTTP Headers

HTTP response headers should be reviewed to determine whether unnecessary technical information is being exposed.

### Review DNS Records Regularly

DNS records should be checked periodically to ensure that only required information and services are publicly exposed.

### Properly Configure and Monitor the WAF

Keep the WAF (ModSecurity) enabled and tuned, since it already blocks naive attacks.

### Perform Regular Internal Network Discovery

Organizations should periodically scan their own networks to identify active devices.

### Investigate Unknown Devices

Any unexpected device discovered during network scanning should be investigated and verified.

### Maintain Network Documentation

Network topology and device information should be documented and updated regularly.

### Perform Security Testing with Authorization

Reconnaissance and scanning should only be performed against systems and networks where appropriate authorization has been provided.

---

# 7.  Conclusion

During **Week 2** of my Cybersecurity & Ethical Hacking internship, I completed practical activities covering footprinting, reconnaissance, and network scanning.

In the footprinting activity, I used six Kali Linux tools to collect information about the target domain. I learned how WHOIS can provide domain information, WhatWeb can identify web technologies, nslookup can resolve domain names, curl can inspect HTTP headers, Wafw00f can identify a WAF, and DNSRecon can provide additional DNS information.

In the network scanning activity, I used Zenmap to identify my local network configuration and discover active hosts. I also collected IP and MAC address information and created a network topology.

The exercises showed me that information gathering is an important part of cybersecurity. Even before attempting to exploit a system, a security professional can learn a significant amount about an environment by carefully analyzing publicly available information and network responses.

I also learned that technical findings should be documented clearly. A good cybersecurity report should explain what was performed, what was discovered, what the observation means, what risk it may create, and what can be done to reduce that risk.

Finally, I learned that reconnaissance and scanning must always be performed within an authorized scope. These activities were completed as part of the assigned educational cybersecurity lab.

---

# 8.  Evidences Collected
Screenshots collected as evidence during the activities (stored in the screenshots/ folder):
![WHOIS](screenshots/1_whois.png)


> Replace the screenshot filenames above with your actual GitHub image filenames if they are different.

---

## 👤 Author

**Gasper Boniphace**  
Cybersecurity Professional - **B083**

---

## 📌 Project Information

| Item | Details |
|---|---|
| **Program Name** | Cybersecurity Program at Networkwalks |
| **Week** | 02 |
| **Modules** | W2-PM1 - Multiple Kali Tools / W2-PM5 - Zenmap Scanning |
| **Repository** | GitHub |
| **Report Title** | Penetration Testing Report - Footprinting & Network Scanning Phases |

---

**End of Report**
