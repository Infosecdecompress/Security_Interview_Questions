# Penetration Testing

### Three ways to attack - Social, Physical, Network 

- **Social**
  - Ask the person for access, phishing. 
  - Cognitive biases - look at how these are exploited.
  - Spear phishing.
  - Water holing.
  - Baiting (dropping CDs or USB drivers and hoping people use them).
  - Tailgating.
- **Physical** 
  - Get hard drive access, will it be encrypted? 
  - Boot from linux. 
  - Brute force password.
  - Keyloggers.
  - Frequency jamming (bluetooth/wifi).
  - Covert listening devices.
  - Hidden cameras.
  - Disk encryption. 
  - Trusted Platform Module.
  - Spying via unintentional radio or electrical signals, sounds, and vibrations (TEMPEST - NSA).
- **Network** 
  - Nmap.
  - Find CVEs for any services running.
  - Interception attacks.
  - Getting unsecured info over the network.

### Exploit Kits and drive-by download attacks

An exploit kit is a toolkit hosted on a malicious or compromised site that automatically fingerprints a visitor's browser and plugins and launches matching exploits. A drive-by download is the result: malware installed simply by visiting the page, with no click required, by exploiting an unpatched vulnerability. Defenses: patching, disabling unneeded plugins, and browser sandboxing.

### Remote Control

Remote code execution and privilege.

Bind shell (opens port and waits for attacker).

Reverse shell (connects to port on attackers C2 server).

### Spoofing

Email spoofing.

IP address spoofing.

MAC spoofing.

Biometric spoofing.

ARP spoofing.

### Tools

Metasploit.

ExploitDB.

Shodan - Google but for devices/servers connected to the internet.

Google the version number of anything to look for exploits.

Hak5 tools.

### Look at MITRE attack matrix

https://attack.mitre.org/

### Pentest Experience Questions

#### How would you start a new pen test?

Begin with scoping and authorization: define targets, rules of engagement, and timing, and get written permission. Then follow the standard phases — reconnaissance (OSINT, passive/active), scanning and enumeration (Nmap, service/version discovery), vulnerability identification, exploitation to prove impact, post-exploitation/pivoting as scope allows, and finally reporting with reproducible steps and remediation. Confirm up front whether it is black/grey/white box, whether the systems are production or test, and whether a backup exists before you touch anything.

#### What is your your all-time favorite bug that you found?

#### What is your favorite tool, and why?

#### What is your least favorite tool, and why?

#### Do you have any tool you've written?

#### Have you attend any bug bounty program?

### Malware & Reversing

#### Interesting malware

Conficker.

Morris worm.

Zeus malware.

Stuxnet.

Wannacry.

CookieMiner.

Sunburst.

#### Malware features

Various methods of getting remote code execution. 

Domain-flux.

Fast-Flux.

Covert C2 channels.

Evasion techniques (e.g. anti-sandbox).

Process hollowing. 

Mutexes.

Multi-vector and polymorphic attacks.

RAT (remote access trojan) features.

#### Decompiling/ reversing 

Obfuscation of code, unique strings (you can use for identifying code).

IdaPro, Ghidra.

#### Static / dynamic analysis

Describe the differences.

Virus total. 

Reverse.it. 

Hybrid Analysis.