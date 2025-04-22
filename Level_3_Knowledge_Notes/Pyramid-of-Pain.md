The Pyramid of Pain is a hierarchical framework for categorising cybersecurity threat indicators and behaviours based on how difficult it is for attackers to change in order to evade detection.


Hashes (Trivial)
Cryptographic hashes are unique file signatures. While helpful for basic detection, they are easy for attackers to change.

Common Hash Types:
- MD5 – 128-bit hash (insecure; collision-prone, deprecated by RFC 6151).
- SHA-1 – 160-bit hash (deprecated due to collision attacks; see RFC 3174).
- SHA-2 – 256-bit+ hash (secure, standard for digital signatures & SSL/TLS).
- If two different files generate the same hash, it is not cryptographically secure.

----------------------------------------------------------------------------------------------

IP Addresses (Easy)
IP addresses are often used to identify malicious infrastructure but are easy to rotate.

Key Points:
- Low-cost for attackers to replace (green level in the Pyramid).
- Useful short-term for blocking known malicious traffic.
- Attackers often bypass by switching IPs or using Fast Flux techniques.

Fast Flux:
- Maps a domain to many rotating IPs via DNS.
- Used in botnets, phishing, malware delivery.
- Increases attacker persistence and stealth.

----------------------------------------------------------------------------------------------

Domain Names (Simple)
Domains are harder to change than IPs but still manageable for attackers.

Why Domains Matter:
- Used for C2 servers, phishing, malware hosting.
- Registration and DNS changes take more effort than IP switching.

Defensive Techniques:
- Analyze DNS logs, proxy logs, and shortened URLs (e.g., bit.ly, tinyurl).
- Watch for Punycode lookalike domains (e.g., xn--addas-o4a.de instead of adidas.de).

Tools like Any.run provide insight via:
- HTTP Requests
- DNS Queries
- Host-to-host communications

----------------------------------------------------------------------------------------------

Host Artifacts (Annoying)
Host-based indicators left on compromised systems. Harder to change and more revealing.

Examples:
- Suspicious registry entries
- Unexpected process launches (e.g., Word > PowerShell)
- Dropped malware files
- Anomalous file paths and filenames

Why They Matter:
- Attackers must recompile, redesign tools to evade.
- Effective for creating EDR/SIEM detection rules.

----------------------------------------------------------------------------------------------

Network Artifacts (Annoying)
Behavioral traces in network traffic can help spot attacker activity in real time.

Examples:
- Abnormal User-Agent strings
- Suspicious HTTP POSTs or URI patterns
- Unusual communication frequency or destinations

Detect using:
- Wireshark / TShark (e.g., tshark -Y http.request -T fields -e http.host -e http.user_agent)
- IDS logs (e.g., Snort)

----------------------------------------------------------------------------------------------

Tools (Challenging)
If a specific attacker tool is detected, they must rebuild or find alternatives — this causes real pain.

Common Attacker Tools:
- Maldocs with embedded macros
- Custom EXEs / DLLs
- Credential stealers or droppers

Detection Techniques:
- Antivirus scans
- Custom SIEM/EDR rules
- YARA rules
- Fuzzy hashing (e.g., SSDeep) for spotting file variants

Resources:
- MalwareBazaar
- Malshare
- SOC Prime Threat Detection Marketplace

----------------------------------------------------------------------------------------------

TTPs (Tactics, Techniques & Procedures)
Top of the pyramid. When you detect TTPs, you’re monitoring the attacker’s behavior — not just their tools.

What Are TTPs?

Tactics – Strategic goals (e.g., data exfiltration).

Techniques – How they achieve it (e.g., phishing).

Procedures – Specific methods/tools used.
 
Use the MITRE ATT&CK Framework to track:
- Initial Access → Privilege Escalation → Exfiltration

Why It Hurts Attackers:
- They must redesign their approach.
- May abandon the target.

Defender’s Goal: Force attackers to choose an easier target.

Understanding the Pyramid of Pain enables analysts to prioritise which signs to monitor and respond to. Focussing on higher layers (such as TTPs and tools) increases the possibility of detecting sophisticated threats early and pushing attackers to reconsider their tactics.
