<h1 align="center">FOOTPRINTING & RECONNAISSANCE PHASE</h1><br><br>


| Field | Details |
|---|---|
| **Program** | Networkwalks-B082 |
| **Date** | August 21, 2026 |
| **Modules Completed** | W2-PM1: Footprinting with Multiple Kali Tools<br>W2-PM2: GHDB-based Footprinting Attacks<br>W2-PM3: Maltego-based Footprinting Attacks<br>W2-PM4: theHarvester-based Footprinting Attacks<br>W2-PM5: Zenmap-based Footprinting Attacks |
| **Report Code** | W2-PM-FINAL |
| **Target** | 1. Networkwalks<br>2. Own local LAN network |
| **Permission Acquired?** | Yes |

<br>**Note:<br>**
- [Penetration Testing Report Section](#PENETRATION-TESTING-REPORT): Contains W2-PM1, W2-PM3, W2-PM4, W2-PM5<br>
- [GHDB Section](#Google-Hacking-Database-(GHDB)): Contains WM-2
<br>

# PENETRATION TESTING REPORT

## 1. EXECUTIVE SUMMARY <br>
This report presents the footprinting and reconnaissance phase of a penetration testing assessment conducted as part of Netowrkwalks-B082 internship program. The assessment was conducted against the authorized target networkwalks.com and the tester’s own local LAN network to gather information about the targets and document the findings identified during this phase. Modules completed in this report include W2-PM1: Footprinting with Multiple Kali Tools, W2-PM3: Maltego-based Footprinting Attacks, W2-PM4: theHarvester-based Footprinting Attacks, and W2-PM5: Zenmap-based Footprinting Attacks.<br><br>


## 2. LIABILITY DISCLAIMER <br>
This assessment was conducted as part of the Networkwalks-B082 internship program for internal and educational purposes. The testing was limited to the authorized targets, networkwalks.com and the tester’s own local LAN network. <br>

The findings, risk analysis, and recommendations presented are based on observations identified during the footprinting and reconnaissance phase and may require further validation during subsequent assessment phases.<br><br>

## 3. TOOLS <br>
These are tools that were used in this report.
| Tool | Purpose |
|---|---|
| **whois** | Find the domain registration details |
| **whatweb** | Fingerprint the web technologies |
| **nslookup** | Resolve the domain to its IP address |
| **curl -I** | Read the HTTP response headers |
| **wafw00f** | Detect a WAF (Web Application Firewall) |
| **dnsrecon** | Enumerate all DNS records |
| **Maltego** | Find email addresses related to the target using transforms |
| **theHarvester** | Information gathering. Gather emails, sub-domains, hosts, employee names, open ports, and banners from different public sources. |
| **Zenmap** | A security scanner open-source software tool. The official GUI version of Nmap. |
| **Kali Linux** | OS for this module. |
| **Windows** | OS for this module. |
| **Windows CMD** | Check local IP and MAC address identification. |<br><br>

## 4. ACTIVITIES PERFORMED <br>
### 4.1 Footprinting & Reconnaissance <br>
For this step, I’m using whois, whatweb, nslookup, curl -I, wafw00f, dnsrecon, theHarvester to gain information about the target.<br><br>

**4.1.1 whois**<br>
The whois command was used to retrieve information related to the domain's registration and configuration, as shown in the table below.

| Field | Details |
|---|---|
| **Domain Name** | NETWORKWALKS.COM |
| **Registrar** | GoDaddy.com, LLC |
| **Registrar URL** | http://www.godaddy.com |
| **Creation Date** | 2019-11-06 |
| **Update Date** | 2025-11-12 |
| **Registry Expiry Date** | 2027-11-06 |
| **Domain Status** | clientDeleteProhibited<br>clientRenewProhibited<br>clientTransferProhibited<br>clientUpdateProhibited |
| **Name Server** | NS6135.HOSTGATOR.COM<br>NS6136.HOSTGATOR.COM |
| **DNSSEC** | unsigned |
<br>
The domain is registered through GoDaddy.com, LLC and uses HostGator as its DNS provider. Multiple domain management restrictions are enabled, including restrictions on deletion, renewal, transfer, and update. These restrictions help prevent unauthorized domain management operations.<br><br>

DNSSEC is reported as unsigned, indicating that DNSSEC is not enabled for the domain. As a result, DNS responses do not have DNSSEC-based cryptographic validation, which may increase exposure to certain DNS-related attacks.
<br><br>

**4.1.2 whatweb**<br>
The following are web technologies and information identified on the target using whatweb:

| Web Technology/Information | Description |
|---|---|
| **Apache** | Web server |
| **WordPress 7.1** | Content Management System (CMS) |
| **WordPress Download Manager 3.3.58** | WordPress plugin |
| **jQuery 3.7.1** | JavaScript library |
| **IP Address** | 192.232.216.135 |

This information can help attackers identify the technologies and versions used by the target. If any of these have known vulnerabilities, the attackers may use this information to identify potential attack vectors. The exposed internal IP address can provide additional information about the target.<br><br>

**4.1.3 nslookup**<br>
Nslookup resolves the domain name to its actual IP address (192.232.216.135). This information can help an attacker perform further reconnaissance, identify other websites hosted on the same IP, and gather information about the target's infrastructure.<br><br>

**4.1.4 curl -I**<br>
The HTTP headers obtained using curl -I show that the target is using the WordPress REST API with the /wp-json/ endpoint. An attacker can access this endpoint to gather information about the WordPress application and its available resources.<br><br>

**4.1.5 wafw00f**<br>
wafw00f detected that the target is protected by WAF called ModSecurity (SpiderLabs). Knowing that a WAF is present can help an attacker understand the target’s security controls and adjust their testing approach.<br><br>

**4.1.6 dnsrecon**<br>
dnsrecon identified the target's DNS information, including mail servers, BIND version (9.16.23-RH), SPF records, and cPanel service records. This information helps an attacker understand the target's DNS, email, and hosting infrastructure and identify potential services for further testing.

| Record | Result |
|---|---|
| **SOA** | ns6135.hostgator.com (50.87.144.87) |
| **NS** | ns6135.hostgator.com (50.87.144.87) |
| **NS** | ns6136.hostgator.com (192.232.216.131) |
| **MX** | mail.networkwalks.com (192.232.216.135) |
| **BIND Version** | 9.16.23-RH |
| **A** | networkwalks.com → 192.232.216.135 |
| **TXT (SPF)** | `v=spf1 +a +mx +ip4:50.87.144.87 +include:websitewelcome.com ~all` |
| **SRV** | `_autodiscover._tcp → cpanelemaildiscovery.cpanel.net:443` |<br><br>

**4.1.7 Maltego**<br>
Maltego identified an email address associated with the target domain called info@networkwalks.com. This information may help an attacker identify potential targets for email-based attacks, such as phishing.<br><br>

**4.1.8 theHarvester**<br>
theHarvester was used to perform passive reconnaissance against the target domain by querying multiple publicly available data sources. These are the findings:

| Finding | Result |
|---|---|
| **ANSs Identified** | 3 – AS13335, AS31898, AS46606 |
| **Interesting URLs** | 2 – http://networkwalks.com/, https://networkwalks.com/ |
| **IPs Identified** | 2 unique IPs – 172.67.198.228, 192.232.216.135 |
| **Emails Identified** | 1 – info@networkwalks.com |
| **Hosts Identified** | 32 |


The identified information provides useful intelligence for mapping the target's publicly exposed infrastructure. ASNs and IP addresses provide insight into the associated network infrastructure, while hosts/subdomains may indicate publicly exposed services. The identified email address may also be relevant for assessing potential exposure to email-based attacks.<br><br>

### 4.2 Network Scanning<br>
Before doing network scanning, check our IP address and subnet using this command on Windows CMD:
ifconfig

Then, I performed network scanning against my own LAN network using the Zenmap Quick scan option. It shows there are 5 hosts up in my subnet (including my PC):
1. `192.168.1.1`
   - **Open Ports:** `80/tcp` — HTTP

2. `192.168.1.2`
   - **Open Ports:**
     - `8008/tcp` — HTTP
     - `8009/tcp` — AJP13
     - `8443/tcp` — HTTPS-ALT

3. `192.168.1.6`
   - **Open Ports:** None identified

4. `192.168.1.14`
   - **Open Ports:** None identified

5. `192.168.1.22`
   - **Open Ports:**
     - `135/tcp` — MSRPC
     - `139/tcp` — NetBIOS-SSN
     - `445/tcp` — Microsoft-DS
<br>
Including the MAC Addresses. As for the graph result included on the 8th section of this report.
<br><br>

## 5. RISK ANALYSIS<br>

| No | Finding | Evidence | Potential Impact | Risk |
|---:|---|---|---|---|
| 1 | **Web technology information exposed** | WhatWeb identified WordPress and WP Download Manager with its versions. | Helps attackers identify known potential vulnerabilities. | 🟠 **Medium** |
| 2 | **Server IP address exposed** | Nslookup resolved to IP address `192.232.216.135`. | Helps attackers perform further reconnaissance. | 🟠 **Medium** |
| 3 | **Multiple live hosts visible on local network** | Zenmap identified five active hosts in the subnet. | Increases the internal attack surface. | 🟠 **Medium** |
| 4 | **HTTP technical information exposed** | cURL exposed `/wp-json/`. | May reveal application information. | 🟡 **Low** |
| 5 | **WAF technology identifiable** | Wafw00f detected ModSecurity (SpiderLabs) WAF. | Reveals security controls information. | 🟡 **Low** |


The findings presented in this section reflect potential security concerns identified during reconnaissance and network scanning, rather than verified vulnerabilities.

The activities were limited to collecting publicly available information and identifying reachable devices and services. No attempts were made to exploit or validate the identified findings. Additional authorized testing would be necessary to determine whether these observations could lead to an actual security weakness.
<br><br>

## 6. RECOMMENDATIONS <br>
These are some recommendations can be applied according to the findings:
1. Keep WordPress and plugins updated and minimize version disclosure.
2. Restrict unnecessary services and apply firewall rules.
3. Restrict network access and disable unnecessary services.
4. Review and restrict unnecessary /wp-json/ information.
5. Keep WAF rules updated and properly configured.
<br><br>

## 7. CONCLUSION <br>
Through this lab, I completed hands-on sessions to do footprinting, reconnaissance, and network scanning against the authorized targets. A total of nine tools were used in this phase. Whois to find the domain registration details, whatweb to fingerprint the web technologies, nslookup to resolve the domain to its IP address, curl to read the HTTP response headers, wafw00f to detect a WAF, dnsrecon to enumerate all DNS records, maltego to find email addresses related to the target using transforms, theHarvester to gather emails, sub-domains, hosts, employee names, open ports, and banners from different public sources. Those were used against networkwalks.com, meanwhile the ninth tool, Zenmap, was used to scan my own local subnet. 

Information gathering is important because we need to know the target before we can start attempting to exploit it. I also learned how to document the findings clearly.
<br><br>

## 8. EVIDENCES COLLECTED<br>

EVIDENCE-W2-PM1-01 Multiple Kali Tools: whois
<img width="908" height="462" alt="result - 01a - whois" src="https://github.com/user-attachments/assets/7245fa85-5c2e-4610-ab2c-ee05dce041e6" />
<br>
<br>
EVIDENCE-W2-PM1-02 Multiple Kali Tools: whatweb
<img width="1079" height="355" alt="result - 01b - whatweb" src="https://github.com/user-attachments/assets/1cd1c18e-4690-4929-ace2-7b074ba3914b" />
<br>
<br>
EVIDENCE-W2-PM1-03 Multiple Kali Tools: nslookup
<img width="1069" height="179" alt="result - 01c - nslookup" src="https://github.com/user-attachments/assets/a51a61f7-32f5-483c-b5e3-caa43136f2a0" />
<br>
<br>
EVIDENCE-W2-PM1-04 Multiple Kali Tools: curl -I
<img width="1076" height="376" alt="result - 01d - curl I" src="https://github.com/user-attachments/assets/69957930-21a9-4c80-a05f-e8219056b661" />
<br>
<br>
EVIDENCE-W2-PM1-05 Multiple Kali Tools: wafw00f
<img width="1069" height="412" alt="result - 01e - wafw00f" src="https://github.com/user-attachments/assets/6cac6778-5092-4c25-a8ea-160c23904d96" />
<br>
<br>
EVIDENCE-W2-PM1-06 Multiple Kali Tools: dnsrecon
<img width="1333" height="517" alt="result - 01f - dnsrecon" src="https://github.com/user-attachments/assets/56c2e2e5-a687-4b38-9e24-391f81af71b2" />
<br>
<br>
EVIDENCE-W2-PM3 Maltego
<img width="1919" height="1018" alt="result - 02 - maltego" src="https://github.com/user-attachments/assets/fec91041-64ad-48ca-acef-0e4d12708e7f" />
<br>
<br>
EVIDENCE-W2-PM4-01 theHarvester: command 1
<img width="966" height="577" alt="theHarvester - 1000 baidu - networkwalks" src="https://github.com/user-attachments/assets/7197e9d3-e831-4e0f-8d61-ccf495bfe540" />
<br>
<br>
EVIDENCE-W2-PM4-02 theHarvester: command 2
<img width="1275" height="754" alt="Screenshot 2026-08-21 153744" src="https://github.com/user-attachments/assets/ab3557d4-8dcd-4e09-a9f9-58cd2eeaedc4" />
<img width="1271" height="761" alt="Screenshot 2026-08-21 153845" src="https://github.com/user-attachments/assets/ca875653-db87-47bc-9057-59d636d5ee08" />
<img width="1257" height="757" alt="Screenshot 2026-08-21 153916" src="https://github.com/user-attachments/assets/9d155886-af3f-4d06-b035-fafb0355e7f9" />
<br>
<br>
EVIDENCE-W2-PM5-01 Zenmap Quick Scan
<img width="1114" height="915" alt="result - zenmap - quick scannn" src="https://github.com/user-attachments/assets/50c51aba-49ea-4334-aa76-a2170c763350" />
<br>
<br>
EVIDENCE-W2-PM5-01 Zenmap Quick Scan Graph
<img width="855" height="394" alt="Screenshot 2026-08-21 224546" src="https://github.com/user-attachments/assets/10463bea-fe40-4a23-b8fa-bcb02c7118e0" />


# Google Hacking Database (GHDB)
The GHDB (Google Hacking Database) is an index of search queries, known as “dorks,” that can be used to find publicly available information. These dorks use normal Google search operators in different ways to find information that websites accidentally expose, such as camera feeds, open directories, login pages, configuration files, and documents. The GHDB can be accessed through https://www.exploit-db.com/google-hacking-database.

In this GHDB-based module, there are two tasks: Find ten live vulnerable security camera links that are exposed accessible from Internet, and find ten downloadable mathematics e-books - PDF format.

These are the dorks I used to complete to tasks:
## Vulnerable Security Camera Links
1. intitle:"webcam 7" inurl:'/gallery.html'
2. intitle:"webcamXP 5" inurl:admin.html
3. intitle:"Webcam" inurl:WebCam.htm
4. inurl:webcam site:skylinewebcams.com inurl:roma
5. inurl:/multi.html intitle:webcam
6. intitle:"webcamxp" "Flash JPEG Stream"
7. inurl:"view.shtml" "camera"
8. intitle:"ContaCam" "Snapshot Image"
9. intitle:"NetCamXL*"
10. "Camera Live Image" inurl:"guestimage.html"

## Mathematics E-Book PDFs
1. intitle:"index of" "math.pdf"
2. site:edu "math" filetype:pdf
3. filetype:pdf "mathematics" "edition"
4. site:drive.google.com mathematics edition*.pdf
5. "calculus" Ext:pdf site:.edu
6. filetype:pdf intitle:"discrete math"
7. "linear algebra" ext:pdf
8. site:mit.edu math OR mathematics filetype:pdf
9. RE: inurl:/wp-content/uploads/math_pdf
10. "mathematics" inurl:PDF

You could check the WM2-PM2 file in Reports to see more detailed result.
