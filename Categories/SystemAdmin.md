# System Admin

### Operating System

### Windows

- Windows registry and group policy. 
- Windows SMB. 
- Samba (with SMB).
- Buffer Overflows. 
- ROP. 

### *nix 

- SELinux.
- Kernel, userspace, permissions.
- MAC vs DAC.
- /proc
- /tmp - code can be saved here and executed.
- /shadow 
- LDAP - Lightweight Directory Browsing Protocol. Lets users have one password for many services. This is similar to Active Directory in windows.

### MacOS

- Gotofail error (SSL).
- MacSweeper.
- Research Mac vulnerabilities.

#### What are Linux’s strengths and weaknesses vs. Windows? 

### How do you change your DNS settings in Linux/Windows? 

Windows: Internet adapter/ 

Linux: sudo nano /etc/resolv.conf  add nameserver x.x.x.x 

### Cyber Crime vs Cyber-enabled crime 

Cyber-enabled crime: traditional crime that is amplified by the use of computer tech 

Cyber Crime: illegal action involving network or computer where it used to commit the crime 

### What is the main goal of information security within an organization or company? 

Protect CIA (Confidentiality, Integrity, Availability)

### What are the consequences of a cyber-attack? 

### Infrastructure (Prod / Cloud) Virtualization 

- Hypervisors.
- Hyperjacking.
- Containers.
- Escaping and privilege escalation techniques.
- Site isolation.
- Network connections from VMs / containers. 
- Side-channel attacks. 
- Beyondcorp by Google
  - Trusting the host but not the network.

### First step of securing Linux Server 

Auditing: A system scan is performed using a tool called Lynis for auditing. Every category is scanned separately and the hardening index is provided to the auditor for further steps. 

Hardening: After the audit is complete, the system is hardened depending on the level of security it further needs. It is an important process based on the decision of auditor. 

Compliance: The system needs to be checked almost every day for better results and also lesser threats from security point of view. 

### How to secure a Web Server 

- Anti-virus and firewalls 
- Safe installation and configuration of the web server software 
- Secure installation and configuration of the O.S 
- Scanning system vulnerability 
- Remote administration disabling 
- Removing of unused and default account 
- Changing of default ports and settings to customs port and settings 
- Update/Patch the web server software 
- Update Permissions/Ownership of files 
- Delete default data/scripts 
- Remove or protect hidden files and directories 
- Web Application and Web Server Security 
- Minimize the server functionality disable extra modules 
- Increase logging verboseness 
- Configured to display generic error messages 
- Make sure Input Validation is enforced within the code: Security QA testing 
- Implement a software security policy 

### Privilege escalation techniques, and prevention.

### Remote Code Execution / getting shells.

### Local databases

- Some messaging apps use sqlite for storing messages.
- Useful for digital forensics, especially on phones.

### IaaS?  

A IaaS, or Infrastructure as a Service, is one of the cloud service that the providers provide the server, storage and networking, the customers will take care of the OS and everything above that 

#### How much do you know about AWS IaaS? 

I do have experience setting up AWS ECS and manage it, therefore I know how to set them up and how it works. 

#### How do you get the logs from AWS IaaS? 

AWS do have a service called CloudWatch that will handle the logs and information from different AWS EC2 and other service, where you can view and manage the logs. 

If you want to see logs and console output for a single instance, it can be found in the Amazon EC2 console  

#### What logs can you get from AWS IaaS logs? 

You will be able to get system logs, console output 

#### What is IaaS vs PaaS vs SaaS? 

In IaaS, provider handles networking, virtual machines, storage. Client has the most flexibility but have to manage many things 

In PaaS, provider handles what's handled in IaaS and also OS, runtime and some of the software maintenance. 

In SaaS, provider handles everything, client can use the product directly without handling or maintaining anything. 