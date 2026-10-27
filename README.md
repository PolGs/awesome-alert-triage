# 🚨 Awesome Alert Triage [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of **free and open-source** tools, platforms, and resources for security analysts doing day-to-day alert triage — from first alert to closed ticket.

Built for SOC analysts, blue teamers, and incident responders who need to move fast without spending money. Every tool listed here is **free**, **open-source**, or has a **meaningful free tier** that doesn't cripple actual workflow. No upsell bait, no "contact us for pricing."

**Pull requests welcome.** If you use it daily and it's free, add it.

---

## Contents

- [🔍 IP & Domain Enrichment](#-ip--domain-enrichment)
- [🗂️ File & Hash Analysis](#️-file--hash-analysis)
- [🌐 URL & Web Analysis](#-url--web-analysis)
- [📧 Email & Phishing Analysis](#-email--phishing-analysis)
- [🧪 Sandboxes & Dynamic Analysis](#-sandboxes--dynamic-analysis)
- [🔎 IOC Extraction & Enrichment](#-ioc-extraction--enrichment)
- [🧠 Threat Intelligence Platforms](#-threat-intelligence-platforms)
- [📡 IOC Feeds & Blocklists](#-ioc-feeds--blocklists)
- [🔭 OSINT & Pivoting](#-osint--pivoting)
- [🛠️ SOAR & Automation](#️-soar--automation)
- [📋 Case Management & IR Tracking](#-case-management--ir-tracking)
- [🔐 SIEM & Log Analysis](#-siem--log-analysis)
- [🧰 Endpoint Triage & Forensics](#-endpoint-triage--forensics)
- [🔑 Credential & Breach Lookup](#-credential--breach-lookup)
- [📚 Playbooks & SOPs](#-playbooks--sops)
- [🧑‍💻 Training & Labs](#-training--labs)
- [📖 Frameworks & References](#-frameworks--references)
- [🧭 The Triage Workflow](#-the-triage-workflow)

---

## 🔍 IP & Domain Enrichment

The first thing you reach for on any network-based alert. These tools answer: *Is this IP or domain something I should care about, and why?*

- [AbuseIPDB](https://www.abuseipdb.com/) - Community-powered IP reputation database returning abuse category, confidence score, ISP, and country. Free API returns JSON. One of the fastest ways to qualify an IP before digging deeper.
- [BGP Ranking (CIRCL)](https://bgpranking.circl.lu/) - Ranks ASNs by volume of malicious activity reported across multiple feeds. Free, run by Luxembourg's national CERT. Useful for flagging entire hosting providers used by threat actors.
- [Censys Search](https://search.censys.io/) - Internet-wide scan data with exceptional TLS certificate pivoting. Find all hosts sharing a certificate or belonging to a specific org. Free for individual researchers.
- [DNSlytics](https://dnslytics.com/) - Reverse IP lookup, domain history, and co-hosted domain discovery. Quickly find what else lives on a suspicious IP. Free.
- [GreyNoise](https://www.greynoise.io/) - Classifies IPs as internet background noise (mass scanners) versus targeted threats. Dramatically reduces alert fatigue. Free Community tier with daily lookup quota.
- [Hurricane Electric BGP](https://bgp.he.net/) - ASN routing and peering data. Reliable for IP-to-ASN attribution and quickly identifying hosting providers. Free.
- [IPinfo](https://ipinfo.io/) - Fast ASN, geolocation, carrier, and org lookup with a clean API. Free for up to 50k requests/month — covers heavy daily analyst use.
- [MXToolbox](https://mxtoolbox.com/) - DNS lookups, blacklist checks, email infrastructure analysis, and WHOIS all in one place. Completely free, no account required.
- [RDAP Lookup (ICANN)](https://lookup.icann.org/) - ICANN's official registration data lookup. More structured output than traditional WHOIS. Free, no account.
- [RiskIQ Community](https://community.riskiq.com/) - Passive DNS history, certificate chains, and WHOIS history going back years. Excellent for infrastructure pivoting. Free community tier.
- [Robtex](https://www.robtex.com/) - Reverse DNS, AS routing data, and graph-based domain relationship mapping. Free.
- [SecurityTrails](https://securitytrails.com/) - Historical DNS records, subdomain enumeration, and IP-to-domain correlation. Free tier: 50 API queries/month.
- [Shodan](https://www.shodan.io/) - Search engine for internet-connected devices. Pivot on open ports, banners, and certificates to understand what's running on a suspicious IP. Free tier available.
- [ThreatMiner](https://www.threatminer.org/) - Data mining portal searchable by IP, domain, hash, SSL cert, and more. Aggregates data from multiple passive sources without requiring an account. Free.
- [VirusTotal](https://www.virustotal.com/) - The analyst's Swiss Army knife. Scan IPs, domains, URLs, and files against 70+ detection engines. Check historical detections without re-uploading. Free tier with rate-limited API.

> **Analyst tip:** When a new IP hits your SIEM, run AbuseIPDB and GreyNoise in parallel first. GreyNoise noise classification alone closes many alerts instantly. If it's targeted and unknown, move to Shodan and Censys to understand the infrastructure before escalating.

---

## 🗂️ File & Hash Analysis

You have a suspicious binary, a hash from an EDR alert, or an attachment you're not sure about. These tools let you dig in without touching the file yourself.

- [Assemblyline](https://github.com/CybercentreCanada/assemblyline) - Scalable open source file triage and analysis platform from the Canadian Centre for Cyber Security. Modular pipeline integrates community tools and handles high-volume automated analysis. Fully free.
- [ClamAV](https://www.clamav.net/) - Open source antivirus engine from Cisco Talos. Scan files locally in air-gapped environments, integrate into pipelines, no data ever leaves your network. Free.
- [Detect-It-Easy (DiE)](https://github.com/horsicq/Detect-It-Easy) - Identifies file type, compiler, packer, linker, and protector for PE files, ELFs, and more. Essential first step before any binary analysis. Free and open source.
- [ExifTool](https://exiftool.org/) - Read, write, and edit metadata from almost any file type. Reveals author names, creation timestamps, embedded paths, and GPS coordinates — all potential pivot points. Free.
- [FileScanner.online](https://filescanner.online/) - Fast, free online file scanner. Upload files and get results from multiple detection engines — no account needed, no concerns about sample sharing for typical triage use cases.
- [hashdeep](https://github.com/jessek/hashdeep) - Compute and audit multiple hashes (MD5, SHA1, SHA256, Tiger, Whirlpool) simultaneously. Great for bulk verification or building file integrity baselines. Free.
- [Loki](https://github.com/Neo23x0/Loki) - Free standalone host-based IOC scanner from Florian Roth. Scans endpoints using YARA rules, hash databases, filename patterns, and C2 indicators. Runs locally — no data leaves your environment.
- [MalwareBazaar](https://bazaar.abuse.ch/) - abuse.ch malware sample repository. Search by hash, tag, file type, or YARA rule. Download samples for your own analysis. Community-driven and completely free.
- [Malwoverview](https://github.com/alexandreborges/malwoverview) - CLI first-response tool that queries VirusTotal, Hybrid Analysis, MalwareBazaar, URLHaus, ThreatFox, AlienVault OTX, and others simultaneously from a single command. Enormous time saver for bulk IOC lookups. Open source.
- [nsrllookup](https://github.com/rjhansen/nsrllookup) - Query NIST's National Software Reference Library to verify if a hash belongs to known legitimate software. Eliminates benign files from your queue fast. Free.
- [PEframe](https://github.com/guelfoweb/peframe) - Static analysis of Windows PE executables and malicious Office documents. Extracts imports, strings, packer hints, and suspicious patterns. Open source.
- [VirusTotal](https://www.virustotal.com/) - Search existing reports by SHA256 hash instantly, without uploading the file. 70+ AV engines plus behavioral reports and community comments. Free.
- [YARA](https://github.com/VirusTotal/yara) - The pattern-matching engine underlying most modern malware detection. Write signatures, run them against files, automate detection logic. Open source, runs everywhere.
- [yarGen](https://github.com/Neo23x0/yarGen) - Automatically generate YARA rules from a malware sample set. Filters common strings using a whitelist DB to reduce false positives. Free.

> **Analyst tip:** Check the SHA256 in VirusTotal before anything else — if a report already exists, you get results in seconds without uploading. Only upload or use FileScanner.online if the hash has zero hits and the file came from a controlled source.

---

## 🌐 URL & Web Analysis

Suspicious redirect, unknown domain in a proxy log, or a link from a phishing email — these tools let you see what a URL actually does without risking your browser or endpoint.

- [CheckPhish](https://checkphish.ai/) - AI-powered phishing URL detection with screenshots, redirect chain analysis, and brand impersonation detection. Free community tier handles typical analyst workloads.
- [CyberChef](https://gchq.github.io/CyberChef/) - Decode base64, URL-encode, deobfuscate strings, extract IOCs, XOR payloads, and manipulate data in almost any format. Entirely browser-based, no server-side processing, works offline. GCHQ open source.
- [dnstwist](https://github.com/elceef/dnstwist) - Generates domain permutations (typosquats, homoglyphs, bit-flips) and checks which are registered and actively serving content. Essential for phishing investigation and brand protection. Open source.
- [Google Safe Browsing Lookup](https://transparencyreport.google.com/safe-browsing/search) - Check whether Google has flagged a URL as phishing, malware, or unwanted software. Instant, free, no account required.
- [IsItPhishing](https://isitphishing.org/) - Real-time phishing URL detection with verdicts and categorization. Free API for integration into automated triage pipelines.
- [PhishTank](https://phishtank.org/) - Community-verified phishing URL database. Cross-reference links from suspicious emails against thousands of confirmed phishing pages. Free API.
- [Sucuri SiteCheck](https://sitecheck.sucuri.net/) - Scans URLs for known malware, blocklist status, and outdated software. Quick reputation check on websites appearing in alerts. Free.
- [Unfurl](https://github.com/obsidianforensics/unfurl) - Deconstructs URLs and exposes hidden data — base64 blobs, timestamps, tracking parameters, session tokens. Open source; also available as a [web app](https://dfir.blog/unfurl/).
- [URLhaus](https://urlhaus.abuse.ch/) - abuse.ch database tracking URLs actively serving malware. Submit new finds, search existing ones. Widely used as an enrichment data source. Completely free.
- [URLScan.io](https://urlscan.io/) - Submits a URL to a sandboxed browser and records every HTTP request, DOM element, script, certificate, and screenshot. The most heavily used free URL analysis tool in daily SOC work. Free with public and private scans.
- [URLScanner.online](https://urlscanner.online/) - Fast, free URL scanner for malicious URL detection. Ideal for quick verdicts on links extracted from phishing emails or proxy logs — instant results without infrastructure setup.

> **Analyst tip:** Never click a suspicious URL directly. Always defang it first (`hxxps://` and `[.]` instead of `.`) for documentation, then submit to URLScan.io or URLScanner.online. Save a screenshot of the result before the page disappears.

---

## 📧 Email & Phishing Analysis

The highest-volume alert type in most SOCs. The goal: *Is this a real phish? What are the IOCs? How far did it spread?*

- [EmailRep](https://emailrep.io/) - Reputation lookup for email addresses. Returns risk level, breach history, associated domains, and social presence. Free API for low-volume automated triage.
- [Google Admin Toolbox – Message Header](https://toolbox.googleapps.com/apps/messageheader/) - Google's email header parser. Especially useful for investigating Gmail-related deliveries. Clean output, free, no account required.
- [iocextract](https://github.com/InQuest/iocextract) - Python library and CLI that pulls URLs, IPs, hashes, and email addresses from raw text — including defanged IOCs using bracket notation. Integrates cleanly into email parsing pipelines. Open source.
- [MXToolbox Email Header Analyzer](https://mxtoolbox.com/EmailHeaders.aspx) - Paste raw email headers and get a color-coded breakdown of routing hops, SPF/DKIM/DMARC results, and delivery delays. Fast, free, essential.
- [OLE Tools (Didier Stevens)](https://github.com/DidierStevens/DidierStevensSuite) - Suite of Python tools for dissecting Office documents: oledump, rtfdump, pdfid, pdf-parser. Extract macros, embedded objects, and hidden URLs from maldocs. Open source and battle-tested.
- [OpenPhish](https://openphish.com/) - Real-time feed of active phishing URLs updated continuously. Cross-reference sender domains or email body links against it directly. Completely free.
- [phishing-analyzer](https://github.com/njodzela/phishing-analyzer) - Python CLI for automated `.eml` analysis. Validates SPF/DKIM/DMARC, extracts all IOCs, enriches against VirusTotal and AbuseIPDB, and outputs an HTML report suitable for tickets. Open source.
- [PhishTool](https://www.phishtool.com/) - Purpose-built phishing email forensics platform. Parses raw emails, extracts headers, URLs, and attachments into a structured investigation view, and auto-enriches via VirusTotal. Free Community edition for individual analysts.
- [SpamAssassin](https://spamassassin.apache.org/) - Open source spam scoring engine using header analysis, IP blacklists, and heuristic rules. Run locally to pre-score inbound email before it reaches analysts. Free.
- [ThePhish](https://github.com/emalderson/ThePhish) - Automated phishing email analysis platform built on TheHive, Cortex, and MISP. Extracts observables from headers and body, runs automated enrichment across all configured analyzers, calculates a verdict, and exports confirmed IOCs to MISP. Fully open source.
- [URLScanner.online](https://urlscanner.online/) - Submit links extracted from phishing emails for instant verdicts without touching your own browser. Free.

> **Analyst tip:** Build a three-step reflex: (1) MXToolbox headers — SPF/DKIM/DMARC fail is a major signal, (2) defang all URLs and submit to URLScanner.online or URLScan.io, (3) hash any attachment and check VirusTotal before downloading it. ThePhish automates all three steps if you've got the stack deployed.

---

## 🧪 Sandboxes & Dynamic Analysis

When static indicators aren't enough and you need to see what a file, URL, or script actually *does* when it runs.

- [Any.run](https://app.any.run/) - Interactive sandbox where you can watch malware execute in real time. Click through prompts, see process trees, network connections, file drops, and registry changes live. Free community tier with public reports.
- [Browserling](https://www.browserling.com/) - Live cross-browser testing in an isolated environment. Test suspicious URLs that require browser interaction without risking your own machine. Free tier available.
- [CAPE Sandbox](https://github.com/kevoreilly/CAPEv2) - Actively maintained Cuckoo fork with enhanced malware config extraction, unpacking capabilities, and broader anti-evasion techniques. Community edition is free and open source. Preferred over vanilla Cuckoo for modern malware.
- [Cuckoo Sandbox](https://github.com/cuckoosandbox/cuckoo) - The original open source, self-hosted sandbox. Full environment control, no external data sharing. Requires setup but gives unlimited private analysis.
- [FileScanner.online](https://filescanner.online/) - Quick multi-engine file analysis without standing up your own sandbox. Good for fast verdicts on files you can safely share externally.
- [Hybrid Analysis](https://www.hybrid-analysis.com/) - Powered by CrowdStrike Falcon Sandbox. Automated behavioral reports with network traffic, process activity, dropped files, and MITRE ATT&CK mapping. One of the most comprehensive free sandboxes available.
- [Intezer Analyze](https://analyze.intezer.com/) - Genetic malware analysis that classifies code reuse from thousands of known malware families. Especially useful for attribution and tracking malware lineage. Free community tier.
- [Joe Sandbox Community](https://www.joesandbox.com/) - Deep behavioral analysis with hundreds of data points per report. Supports Office documents, PDFs, scripts, and executables. Free community tier.
- [Tria.ge](https://tria.ge/) - Fast multi-OS sandbox supporting Windows 7/10, Linux, macOS, and Android. Excellent malware family detection and C2 config extraction. Free community tier. Built by Hatching.
- [VMRay Community](https://www.vmray.com/pricing/) - Hypervisor-based sandbox that's harder for malware to detect than traditional VMs. Limited free submissions per month but produces high-quality reports for evasive samples.

> **Analyst tip:** Use Any.run when you need to interact with the sample (click through prompts, respond to UAC). Use Hybrid Analysis or Tria.ge when you need automated reports fast with zero setup. Use Cuckoo or CAPE when samples are sensitive and can't leave your environment.

---

## 🔎 IOC Extraction & Enrichment

Pulling indicators out of raw text, emails, logs, and reports — then adding enough context to make a triage decision.

- [Cortex](https://github.com/TheHive-Project/Cortex) - Observable analysis engine from TheHive Project. Configure analyzers (VirusTotal, Shodan, MISP, AbuseIPDB, etc.) once, then trigger them against any observable automatically from any case. Open source.
- [CyberChef](https://gchq.github.io/CyberChef/) - Decode base64, refang URLs, extract strings, XOR-decode payloads, and manipulate any encoded artifact into something readable. Browser-based, fully offline-capable. GCHQ open source.
- [iocextract](https://github.com/InQuest/iocextract) - Extracts IPs, domains, URLs, hashes, and email addresses from any text — including defanged IOCs using bracket notation. Python library and CLI. Open source.
- [IntelOwl](https://github.com/intelowlproject/IntelOwl) - Open source threat intelligence aggregator querying 100+ analyzers from a single API call. Self-hosted, free, and highly extensible. One of the most powerful free enrichment platforms available.
- [iocsearcher](https://github.com/malicialab/iocsearcher) - Extracts IOCs from PDF, HTML, Word, and plain text security reports. Especially useful for pulling indicators from threat intel PDFs that aren't machine-readable. Open source.
- [Malwoverview](https://github.com/alexandreborges/malwoverview) - CLI first-response triage tool querying VirusTotal, Hybrid Analysis, MalwareBazaar, URLHaus, ThreatFox, OTX, and more simultaneously. Single command for multi-source IOC enrichment. Open source.
- [MISP Warninglists](https://github.com/MISP/misp-warninglists) - Curated lists of known false-positive indicators: Google IPs, CDN ranges, Microsoft subnets, Tor exits. Import into your SIEM or TIP to suppress noise before alerting. Free.
- [Pulsedive](https://pulsedive.com/) - Community-driven IOC enrichment with risk scoring, threat actor tagging, and historical tracking. Free tier handles typical daily analyst volumes without needing API keys to start.
- [ThreatIngestor](https://github.com/InQuest/ThreatIngestor) - Automates IOC extraction from Twitter, RSS feeds, MISP, SQS, and more, then pushes results to your TIP or SIEM. Pairs directly with iocextract. Open source.

---

## 🧠 Threat Intelligence Platforms

Platforms that aggregate, correlate, and contextualize threat data so you understand *what* you're dealing with, not just *that* something looks malicious.

- [AlienVault OTX](https://otx.alienvault.com/) - One of the largest community threat intel sharing platforms. "Pulses" package IOCs with campaign context, TTPs, and attribution. Over 19 million new IOCs processed daily. Free, no subscription.
- [IBM X-Force Exchange](https://exchange.xforce.ibmcloud.com/) - IBM's threat intelligence sharing platform. Search IPs, URLs, hashes, and vulnerabilities against community and IBM research data. Free tier gives meaningful access.
- [ICHI — Internet Cyber Health Index](https://ichi.global/) - Free daily barometer of internet-wide cyber health. Aggregates 28 live threat intel feeds (CISA KEV, EPSS, ransomware trackers, C2 infrastructure, DShield) into a composite hourly score. Useful for morning briefings — calibrate alert priority against current macro threat conditions before diving into individual enrichment. Source-transparent, published methodology, no account required.
- [IntelOwl](https://github.com/intelowlproject/IntelOwl) - Threat intelligence aggregation with 100+ analyzers. Submit a single observable and get enrichment from all sources simultaneously. Self-hosted and free.
- [MISP](https://www.misp-project.org/) - The gold standard open source threat intelligence platform. Share and correlate IOCs across teams, organizations, and trust groups. STIX/TAXII support, extensive APIs, massive community. Fully free and open source.
- [OpenCTI](https://github.com/OpenCTI-Platform/opencti) - Modern threat intel platform built natively around STIX2. Strong graph visualization, connector ecosystem for automatic feed ingestion, and a beautiful interface. Free open source community edition.
- [Pulsedive](https://pulsedive.com/) - Community IOC enrichment platform with risk scores, threat actor context, and campaign tracking. Free tier is practical for solo analysts and small teams.
- [ThreatFox](https://threatfox.abuse.ch/) - abuse.ch platform dedicated to sharing C2 infrastructure IOCs: IPs, domains, and URLs associated with malware command-and-control. Free API, entirely community-driven.
- [ThreatMiner](https://www.threatminer.org/) - Free threat intelligence portal with no account required. Search IPs, domains, hashes, SSL certs, and user agents against aggregated passive data sources.
- [YETI](https://github.com/yeti-platform/yeti) - Your Everyday Threat Intelligence platform. Organizes observables, IOCs, TTPs, and threat actors with relationships and timelines. Great for small teams that need structure without MISP complexity. Open source.

---

## 📡 IOC Feeds & Blocklists

Free, community-maintained feeds you can push directly into your SIEM, firewall, or TIP to enrich detections and block known bad infrastructure.

- [abuse.ch Feeds](https://abuse.ch/) - The best free threat feed ecosystem available. URLhaus (malicious URLs), MalwareBazaar (malware hashes), ThreatFox (C2 IOCs), Feodo Tracker (botnet C2 IPs), and SSL Blacklist — all free and API-accessible.
- [Bambenek DGA Feeds](https://osint.bambenekconsulting.com/feeds/) - OSINT feeds based on DGA analysis for active malware families. Catch infected machines attempting to phone home. Free for non-commercial use.
- [Botvrij IOCs](https://www.botvrij.eu/) - Open source IOC data from the Botvrij.eu community in CSV and MISP-compatible formats. Free.
- [Cyber Cure Free Intel](https://www.cybercure.ai/free-cyber-threat-intelligence/) - Daily updated feeds for malicious IPs, URLs, and file hashes. Free, no registration.
- [Emerging Threats (Proofpoint)](https://rules.emergingthreats.net/) - Community Snort/Suricata rulesets updated daily by threat researchers. Free community rules cover thousands of attack patterns. No license required.
- [ESET Malware IOCs](https://github.com/eset/malware-ioc) - IOCs from ESET Research's public investigations including APT campaign indicators. Free GitHub repo, regularly updated.
- [FireHOL IP Lists](https://iplists.firehol.org/) - Aggregates and normalizes 350+ IP blocklists with overlap analysis, age tracking, and country maps. The most comprehensive open-source IP blocklist resource. Free.
- [MISP Warning Lists](https://github.com/MISP/misp-warninglists) - Curated lists of known-good indicators to suppress false positives: CDN ranges, email providers, update servers. Free.
- [OpenPhish](https://openphish.com/) - Real-time phishing URL feed updated continuously. Free tier provides a daily list used by email gateways and proxies worldwide.
- [PhishTank](https://phishtank.org/) - Community-verified phishing database with free API. Cross-reference domains and URLs against confirmed phishing pages.
- [Unit 42 IOC Repository](https://github.com/pan-unit42/iocs) - Indicators from Palo Alto Unit 42's public threat reports. Regularly updated from published research. Free GitHub repo.

---

## 🔭 OSINT & Pivoting

When you need to go beyond the initial indicator and understand the attacker's infrastructure, identity, or campaign. Every tool here lets you start from one IOC and expand outward.

- [Censys Search](https://search.censys.io/) - TLS certificate pivoting is Censys's superpower. Find all hosts sharing a certificate, or all infrastructure registered to a specific org. Free for individual researchers.
- [grep.app](https://grep.app/) - Search across 500,000+ public GitHub repositories. Invaluable for finding IOCs, malware strings, leaked credentials, or tools linked to a threat actor. Free.
- [IntelligenceX](https://intelx.io/) - Search Tor, I2P, paste sites, WHOIS, and data leaks for emails, domains, and credentials. Free tier returns limited results but confirms exposure across dark web sources.
- [Maltego Community Edition](https://www.maltego.com/ce/) - Visual link analysis for OSINT investigations. Map relationships between domains, IPs, people, and organizations using graph transforms. Community Edition is free with limited transforms.
- [Recon-ng](https://github.com/lanmaster53/recon-ng) - Modular web reconnaissance framework with a Metasploit-style interface. 45+ modules for DNS, social media, credential exposure, and more. Included in Kali. Open source.
- [RiskIQ Community](https://community.riskiq.com/) - Passive DNS history and certificate chain data going back years. Reveals when a domain was first active, previous IPs, and associated infrastructure. Free community tier.
- [SecurityTrails](https://securitytrails.com/) - Historical DNS, reverse IP, and subdomain data. Correlate current indicators to historical infrastructure. Free tier: 50 API queries/month.
- [Shodan](https://www.shodan.io/) - Pivot on an IP to find other infrastructure using the same certificate, ASN, banner, or HTTP header. Free tier available.
- [SpiderFoot](https://github.com/smicallef/spiderfoot) - Automated OSINT collection with 200+ modules correlating passive DNS, WHOIS, social media, and dark web sources. Open source, self-hosted.
- [theHarvester](https://github.com/laramies/theHarvester) - Gather emails, subdomains, hosts, employee names, open ports, and banners from public sources. Included in Kali. Open source.
- [Wayback Machine](https://web.archive.org/) - Check what a suspicious domain looked like historically. A domain registered last week with archived content from years prior is a significant red flag. Free.

---

## 🛠️ SOAR & Automation

Stop doing the same five enrichment steps by hand on every alert. These tools let you build playbooks that handle the mechanical work automatically.

- [Cortex](https://github.com/TheHive-Project/Cortex) - Observable analysis and active response engine from TheHive Project. Configure analyzers (VirusTotal, Shodan, MISP, AbuseIPDB) and responders (block IP, disable AD account) once — then trigger from any case. Open source.
- [GRR Rapid Response](https://github.com/google/grr) - Google's open source remote live forensics framework. Deploy agents, run hunts, and collect artifacts from endpoints at scale. Best suited for large environments. Free.
- [n8n](https://github.com/n8n-io/n8n) - Open source workflow automation with 350+ integrations. Widely used for building custom SOC pipelines: ingest alert → enrich → create ticket → notify. Self-hosted version is free.
- [Shuffle](https://github.com/Shuffle/Shuffle) - Open source SOAR with a visual drag-and-drop workflow builder and 400+ app integrations. Sigma rule support and webhook triggers built in. Free community tier is functional for small teams.
- [StackStorm](https://stackstorm.com/) - Event-driven automation platform for complex multi-step security runbooks. More powerful than n8n for conditional logic and large-scale orchestration. Open source community edition.
- [TheHive](https://github.com/TheHive-Project/TheHive) - Scalable open source IR platform with native SOAR capabilities. Integrate with MISP and Cortex to auto-enrich all case observables on creation. TheHive 4 is fully free and open source.
- [Velociraptor](https://github.com/Velocidex/velociraptor) - Endpoint interrogation and response at scale. Collect artifacts from hundreds of endpoints simultaneously, run hunts, and execute response actions — all from one console. Open source.
- [Watcher](https://github.com/thalesgroup-cert/Watcher) - Automated OSINT threat intelligence monitoring. Watches domains, certificates, and paste sites for new IOCs and sends alerts. Open source from Thales Group CERT.

---

## 📋 Case Management & IR Tracking

Keep investigations organized, consistent, and auditable. These platforms turn scattered notes and Slack threads into structured incident records with timelines and evidence.

- [DFIR IRIS](https://github.com/dfir-iris/iris-web) - Collaborative web-based IR platform with case timelines, evidence management, structured note-taking, and export-ready reporting. Built specifically for DFIR investigations. Lightweight, modern, and free.
- [DFIRTrack](https://github.com/dfirtrack/dfirtrack) - Incident tracking focused on affected systems, artifacts, and case tasks. Designed for tracking scope across large compromise investigations. Open source.
- [FIR (Fast Incident Response)](https://github.com/certsocietegenerale/FIR) - Lightweight, agile incident management platform from CERT Société Générale. Minimal setup, adapts easily to existing workflows. Free and open source.
- [TheHive](https://github.com/TheHive-Project/TheHive) - Full-featured open source case management purpose-built for SOC and CSIRT teams. Templates, task tracking, observable management, and bidirectional MISP integration. The most widely deployed free IR platform. TheHive 4 is fully free.
- [Timesketch](https://github.com/google/timesketch) - Google's open source collaborative timeline analysis tool. Build shared forensic timelines from EVTX, Plaso, and CSV data sources and annotate events with team context. Free.

> **Analyst tip:** Even if you use a commercial ticketing system like ServiceNow, running TheHive in parallel for complex incidents is worth it. The observable graph, MISP integration, and Cortex enrichment flows have no equivalent in general-purpose ITSM tools.

---

## 🔐 SIEM & Log Analysis

Ingest, normalize, correlate, and search logs at scale. The platform everything else feeds into.

- [Elastic SIEM](https://www.elastic.co/siem) - SIEM built on the Elastic Stack with prebuilt detection rules, ML anomaly detection, and MITRE ATT&CK-aligned dashboards. Self-hosted deployment is free and handles production workloads.
- [Graylog Open](https://graylog.org/products/source-available/) - Log management platform with fast full-text search, alerting, and dashboards. Source-available community edition handles significant log volumes and is relatively easy to deploy.
- [HELK](https://github.com/Cyb3rWard0g/HELK) - Pre-configured Hunting ELK stack with Elasticsearch, Logstash, Kibana, and Jupyter notebooks for threat hunting analytics. Spin it up in minutes. Open source.
- [OpenSearch Security Analytics](https://opensearch.org/docs/latest/security-analytics/) - AWS's open source Elasticsearch fork with native security analytics capabilities. SIEM rules, threat detection, and prebuilt dashboards. Fully free.
- [Sigma](https://github.com/SigmaHQ/sigma) - Vendor-agnostic detection rule format. Write one rule, convert it to Splunk SPL, Sentinel KQL, Elastic EQL, QRadar AQL, and more. Community-maintained rules cover thousands of TTPs. The Rosetta Stone of detection engineering. Free.
- [SigmaHQ Rules Repository](https://github.com/SigmaHQ/sigma/tree/master/rules) - 3,000+ community-maintained detection rules for Windows, Linux, cloud, web, and network sources — all in Sigma format, ready to convert for your stack. Free.
- [Suricata](https://suricata.io/) - High-performance network IDS/IPS/NSM engine. Reads Emerging Threats and custom rules. Generates structured EVE JSON logs that integrate with every major SIEM. Free and open source.
- [Wazuh](https://github.com/wazuh/wazuh) - The most complete free open source SIEM/XDR platform. Combines log analysis, file integrity monitoring, vulnerability detection, configuration assessment, and automated response. Built on the Elastic Stack. Recognized as Best SIEM Solution by SC Media 2023. Free.
- [Zeek](https://zeek.org/) - Network security monitoring framework that generates rich structured logs from packet captures or live traffic. Foundation of many open source SIEM deployments. Free and open source.

---

## 🧰 Endpoint Triage & Forensics

When you need artifacts from the actual endpoint — live machine, RAM dump, or disk image.

- [Assemblyline](https://github.com/CybercentreCanada/assemblyline) - Open source file triage and analysis platform from the Canadian Centre for Cyber Security. Handles bulk file processing with modular analysis pipelines. Free.
- [Autoruns](https://learn.microsoft.com/en-us/sysinternals/downloads/autoruns) - Sysinternals tool that enumerates every persistence mechanism on a Windows system: registry run keys, scheduled tasks, services, browser extensions, and more. Free from Microsoft.
- [DFIR-ORC](https://github.com/DFIR-D3/dfir-orc) - Forensically sound artifact collection from Windows systems, developed by ANSSI (France's national cybersecurity agency). Reliable, tested, and free.
- [Eric Zimmerman Tools](https://ericzimmerman.github.io/) - Suite of free, battle-tested Windows forensic parsers: MFTECmd, PECmd (Prefetch), RECmd (Registry), Timeline Explorer, and more. The gold standard for Windows artifact parsing.
- [FastIR Collector](https://github.com/SekoiaLab/Fastir_Collector) - Rapid Windows forensic artifact collection from Sekoia. Runs in minutes, produces structured output ready for immediate analysis. Free.
- [KAPE](https://www.kroll.com/en/insights/publications/cyber/kroll-artifact-parser-extractor-kape) - Kroll Artifact Parser and Extractor. Fastest targeted collection of Windows forensic artifacts: event logs, prefetch, registry, browser history. Free. Created by Eric Zimmerman.
- [Loki](https://github.com/Neo23x0/Loki) - Standalone IOC scanner. Run against live endpoints or forensic images to detect known malware by hash, YARA rule, filename, or C2 indicator. Free.
- [Osquery](https://github.com/osquery/osquery) - SQL-powered endpoint visibility. Query file system, processes, network connections, users, and registry as if they were database tables. Integrates with every major SIEM and EDR. Free and open source.
- [Process Monitor](https://learn.microsoft.com/en-us/sysinternals/downloads/procmon) - Real-time monitoring of file system, registry, and process activity on Windows. Indispensable for live malware analysis and endpoint triage. Free from Microsoft.
- [Velociraptor](https://github.com/Velocidex/velociraptor) - The most impactful free endpoint tool you can add to your SOC. Query 100 endpoints in seconds using VQL, collect artifacts at scale, run hunts, and push response actions — all from one console. Completely free, actively developed.
- [Volatility 3](https://github.com/volatilityfoundation/volatility3) - Industry-standard open source memory forensics. Extract running processes, network connections, injected code, encryption keys, and credentials from RAM dumps. Free.
- [Wireshark](https://www.wireshark.org/) - The standard network traffic analysis tool. Capture and analyze packets, filter by protocol or IOC, follow TCP streams, and dissect almost any protocol. Free and open source.

> **Analyst tip:** If you deploy only one new tool from this entire list, make it Velociraptor. The ability to run a hunt across your entire endpoint fleet in under a minute changes how you respond to incidents.

---

## 🔑 Credential & Breach Lookup

Verify whether credentials, emails, or usernames from an alert have been exposed in known breaches.

- [CIRT.net Default Passwords](https://cirt.net/passwords) - Large database of default credentials for network devices, routers, and software. Useful when investigating attacks on unpatched or factory-default equipment. Free.
- [Dehashed](https://dehashed.com/) - Search leaked databases for email addresses, usernames, IPs, hashes, and passwords. Paid subscription but has limited free daily lookups. The most comprehensive breach search engine available.
- [Hashes.com](https://hashes.com/en/decrypt/hash) - Free hash lookup and cracking database. Submit NTLM, MD5, or SHA1 hashes to check if they've been cracked and mapped to plaintext. Useful during credential theft investigations.
- [Have I Been Pwned](https://haveibeenpwned.com/) - The most trusted public breach database. Check email addresses against 13+ billion records from 700+ breaches. API free for personal use and non-profits. The first stop for any credential-related alert.
- [IntelligenceX](https://intelx.io/) - Search paste sites and data leaks for emails, domains, and credential dumps. Free tier returns limited results but confirms exposure across dark web sources.
- [Leak-Lookup](https://leak-lookup.com/) - Free breach lookup for emails and usernames covering a large number of breach datasets. No per-lookup fees on the free tier.

---

## 📚 Playbooks & SOPs

Don't reinvent the wheel for every incident type. Adapt these battle-tested procedures to your environment instead of starting from scratch under pressure.

- [CISA Ransomware Response Guide](https://www.cisa.gov/stopransomware/ransomware-guide) - CISA's step-by-step ransomware response guide covering detection, containment, eradication, and recovery with specific technical steps. Free PDF.
- [DFIQ Project](https://dfiq.org/) - Digital Forensics Investigative Questions. Structured framework defining exactly what questions to answer during an investigation and which data sources address them. Free.
- [IRM by CERT Société Générale](https://github.com/certsocietegenerale/IRM) - Incident Response Methodologies for common attack types: ransomware, phishing, DDoS, web compromise, and more. Structured checklists ready to adapt. Free and open source.
- [NIST SP 800-61 Rev 2](https://csrc.nist.gov/publications/detail/sp/800-61/rev-2/final) - The authoritative US government guide to computer security incident handling. Covers preparation through post-incident activity. Free PDF.
- [PagerDuty Incident Response Docs](https://response.pagerduty.com/) - PagerDuty's open source IR documentation. Covers severity definitions, on-call procedures, communication templates, and post-incident review. Free.
- [SANS Incident Handler's Handbook](https://www.sans.org/white-papers/33901/) - SANS PICERL-based incident response methodology: Preparation, Identification, Containment, Eradication, Recovery, Lessons Learned. Free.
- [Sigma Rules Repository](https://github.com/SigmaHQ/sigma) - 3,000+ community-maintained detection rules for common attack patterns, mapped to MITRE ATT&CK. Ingest directly into your SIEM. Free.
- [Velociraptor Artifact Exchange](https://docs.velociraptor.app/exchange/) - Community-contributed VQL artifacts for common triage and threat hunting tasks. Deploy instantly against your endpoint fleet. Free.
- [Awesome Incident Response](https://github.com/meirwah/awesome-incident-response) - Companion list with extensive IR tools and resources worth bookmarking alongside this one.

---

## 🧑‍💻 Training & Labs

You can't triage effectively without muscle memory. These platforms let you build it before a real incident forces you to improvise.

- [Blue Team Labs Online](https://blueteamlabs.online/) - Hands-on DFIR, security operations, reverse engineering, and threat hunting challenges. Different scenario library from CyberDefenders. Free tier available.
- [CyberDefenders](https://cyberdefenders.org/) - Blue team CTF challenges simulating real incidents: PCAP analysis, memory forensics, log investigation, malware analysis. High quality, community-created scenarios. Free tier available.
- [DetectionLab](https://github.com/clong/DetectionLab) - Terraform/Vagrant lab with a pre-configured Windows domain, Splunk, Fleet, and endpoint telemetry. Build your own triage practice environment locally. Free.
- [Hack The Box – SOC Analyst Path](https://www.hackthebox.com/) - Structured SOC analyst learning path with labs covering SIEM operation, log analysis, and blue team techniques. Free tier with limited content.
- [LetsDefend](https://letsdefend.io/) - Closest free platform to actual SOC work. Realistic alert queue, SIEM interface, and case management. Excellent for building L1/L2 triage speed. Free tier.
- [Malware Traffic Analysis](https://www.malware-traffic-analysis.net/) - Brad Duncan's enormous library of malicious PCAP files with exercises and write-ups. The best free resource for network-based malware investigation practice. Free.
- [SANS Cyber Aces](https://www.sans.org/cyberaces/) - Free foundational security courses from SANS covering OS internals, networking, and security operations basics.
- [Splunk BOTS (Boss of the SOC)](https://bots.splunk.com/) - SANS/Splunk CTF datasets built around real attack scenarios. Practice SPL queries and incident investigation on data that mirrors production environments. Free.
- [TryHackMe](https://tryhackme.com/) - Guided learning paths covering SOC analyst skills, phishing analysis, log investigation, SIEM operations, and malware analysis. Browser-based labs, no local setup. Free tier with substantial content.

---

## 📖 Frameworks & References

The conceptual foundations every triage analyst should know. These aren't tools — they're the mental models that make tools useful.

- [DFIQ Project](https://dfiq.org/) - Digital Forensics Investigative Questions. Structured approach to defining what questions to answer during an investigation and which data sources address them. Free.
- [ENISA Incident Management Guide](https://www.enisa.europa.eu/publications/good-practice-guide-for-incident-management) - European Union Agency for Cybersecurity's guide to incident handling processes and team structure. Free PDF.
- [MITRE ATT&CK](https://attack.mitre.org/) - The universal adversary tactics and techniques knowledge base. Use it to understand *what an attacker was doing* from an alert, not just what the raw indicator was.
- [MITRE ATT&CK Navigator](https://mitre-attack.github.io/attack-navigator/) - Browser-based tool to visualize ATT&CK coverage, map detections, highlight gaps, and track threat actor profiles. Free.
- [MITRE D3FEND](https://d3fend.mitre.org/) - Defensive countermeasures knowledge graph. For each offensive technique, shows the defensive technique that counters it. Free.
- [NIST Cybersecurity Framework](https://www.nist.gov/cyberframework) - Identify, Protect, Detect, Respond, Recover. The canonical framework for understanding where triage fits in the broader program. Free.
- [11 Strategies for a World-Class SOC (MITRE)](https://www.mitre.org/news-insights/publication/11-strategies-world-class-cybersecurity-operations-center) - The most practical SOC management paper ever written. Covers staffing, tooling, metrics, and operations with real-world grounding. Free PDF.
- [Pyramid of Pain (David Bianco)](http://detect-respond.blogspot.com/2013/02/the-pyramid-of-pain.html) - Foundational model for understanding the relative value and durability of different IOC types. Required reading before designing any detection strategy.
- [Sigma Rule Writing Guide](https://github.com/SigmaHQ/sigma/wiki/Rule-Creation-Guide) - How to write, test, and contribute Sigma detection rules. Free.

---

## 🧭 The Triage Workflow

Every tool in this list maps to one or more stages of the core triage loop. Knowing where you are in the loop helps you pick the right tool for the moment.

```
┌─────────────────────────────────────────────────────────────────────┐
│                         ALERT RECEIVED                              │
│         (SIEM, EDR, Phishing Report, IDS, Proxy, User Report)       │
└────────────────────────────┬────────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────────────┐
│  1. ENRICH                                                          │
│     IPs/Domains   →  AbuseIPDB · VirusTotal · GreyNoise · Shodan   │
│     Files/Hashes  →  VT · MalwareBazaar · FileScanner.online       │
│     URLs          →  URLScan.io · URLScanner.online · URLhaus       │
│     Emails        →  MXToolbox · PhishTool · EmailRep              │
└────────────────────────────┬────────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────────────┐
│  2. CORRELATE                                                       │
│     Cross-ref IOCs  →  MISP · AlienVault OTX · ThreatFox           │
│     Check feeds     →  abuse.ch · FireHOL · Emerging Threats        │
│     Auto-enrich     →  Cortex · IntelOwl · Malwoverview             │
└────────────────────────────┬────────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────────────┐
│  3. INVESTIGATE                                                     │
│     Sandbox         →  Any.run · Hybrid Analysis · Tria.ge          │
│     Endpoint        →  Velociraptor · KAPE · Volatility · Osquery   │
│     Pivot           →  Maltego · SpiderFoot · Censys · RiskIQ       │
└────────────────────────────┬────────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────────────┐
│  4. DECIDE                                                          │
│     True Positive       →  Escalate and Respond                    │
│     False Positive      →  Document and Tune                        │
│     Insufficient Data   →  Return to step 1 with new IOCs          │
└────────────────────────────┬────────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────────────┐
│  5. RESPOND & DOCUMENT                                              │
│     Case management  →  TheHive · DFIR IRIS · FIR                  │
│     Automate         →  Shuffle · Cortex · StackStorm              │
│     Share IOCs       →  MISP · ThreatFox · AlienVault OTX          │
│     Tune detections  →  Sigma rules · SIEM adjustments             │
└─────────────────────────────────────────────────────────────────────┘
```

> **Key principle:** The goal of triage is not full investigation — it's a fast, confident **decision**. Move to step 3 only when steps 1 and 2 don't give you enough to close or escalate. The majority of alerts should be resolved at enrichment.

---

## Contributing

Contributions are very welcome! Please read the [contribution guidelines](CONTRIBUTING.md) before submitting a PR.

**To add a tool, it must:**
1. Be **free**, **open-source**, or have a **real free tier** — not just a trial
2. Be **actively maintained** — updated within the last 2 years
3. Be **directly useful during alert triage**, not just generally useful for security
4. Be placed in **alphabetical order** within its section
5. Have a description of **one to two sentences** focused on the specific triage use case

**To propose a new section**, open an issue first to discuss scope fit.

---

## License

[![CC0](https://mirrors.creativecommons.org/presskit/buttons/88x31/svg/cc-zero.svg)](https://creativecommons.org/publicdomain/zero/1.0)

To the extent possible under law, the authors have waived all copyright and related rights to this work.
