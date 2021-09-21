# Security and Risk Management

### Vulnerability vs Risk 

Vulnerability: A vulnerability is a weakness in a system or application that may be exploited to violate that specific system without any context to the impact involved. Vulnerability refers to the security flaws in or a computer or system that allow an attack to be successful. A successful compromise of a vulnerability may result in data manipulation, code execution, data loss etc. 

Risk: Risk is the intersection of threats, assets, and vulnerabilities. The potential for loss, damage or destruction of an asset as a result of a threat exploiting a vulnerability. Risk is essentially the level of possibility that an action will lead to lead to a loss or to an undesired outcome. The risk may even pay off and not lead to a loss, it may lead to a gain. A risk assessment is performed to determine the most important potential security breaches to address now, rather than later. 

### Threat vs Exploit 

Threat: A threat is what we’re trying to protect against. A potential danger to the machine system. It describes something that a company doesn’t want to happen. The successful exploitation of the vulnerability is a threat. A threat may be a malicious attacker who is attempting to obtain unauthorized access to an asset. Natural or man-made occurrence, individual, entity, or action that has or indicates the potential to harm life, information, operations, the environment and/or property. 

Exploit: The exploit is something that takes advantage of vulnerability in an asset to generate unintended or unexpected behavior in the target system, which would enable an attacker to get access to data or information. 

### How do you measure and quantify risk?

### How do you determine the risk appetite for the organization?

### What is the primary reason most companies haven’t fixed their vulnerabilities? 

### What’s the goal of information security within an organization? 

### If you were to start a job as head engineer or CSO at a Fortune 500 company due to the previous guy being fired for incompetence, what would your priorities be? 

(Imagine you start on day one with no knowledge of the environment. )

- Where is the important data? 
- Who interacts with it?
- What’s being logged an audited?
- Network diagrams. 
- Visibility touch points.
- Ingress and egress filtering. 
- Previous vulnerability assessments.

The key is to see that they could quickly prioritize, in just a few seconds, what would be the most important things to learn in an unknown situation. 

### As a corporate Information Security professional, what’s more important to focus on: threats or vulnerabilities? 

Vulnerabilities should usually be the main focus since we in the corporate world usually have little control over the threats. 

Threats (in terms of vectors) will always remain the same, and that the vulnerabilities we are fixing are only the known ones. 

Therefore we should be applying defense-in-depth based on threat modeling in addition to just keeping ourselves up to date. 

### When is it appropriate to respond to a business unit with a “no” when they ask permission?

### What are the top 2 items on the OWASP top 10 that our org should be concerned about, in terms of financial risk? What would you suggest we implement to reduce our risk?

### What will your 30-60-90 day plan when you get onboard?

### What is Open Source Software?

Open source software is software with source code that anyone can inspect, modify, and enhance. Programmers who have access to a computer program’s source code can improve that program by adding features to it or fixing parts that don’t always work correctly. 

### What is more secure? Open source project or proprietary project? 

The securities of these projects depend mainly on the size of the project, the total number of the developers who are working under this project and the one factor, which is most essential as well as important, is the control of the quality. Just the type of project won’t determine its quality, the inside matter of the corresponding projects will matter. 

### Where do you get your security news from? 

### What are the advantages offered by bug bounty programs over normal testing practices? 

You should hear coverage of many testers vs. one, incentivization, focus on rare bugs, etc. 

### How would you measure how well a security team is doing? 

Here we’re looking for them to ask us questions in return, such as, “What kind of team?” Answers that are bad include anything purely number-based like number of IDS events, or widget-thingies detected.  

### Who’s more dangerous to an organization, insiders or outsiders? 

### Vulnerability Assessment vs Penetration Testing 

Vulnerability Assessment is an approach used to find flaws in an application/network whereas Penetration testing is the practice of finding exploitable vulnerabilities like a real attacker will do. VA is like travelling on the surface whereas PT is digging it for gold. 

### Chain of Custody 

Protocol for handling physical proof that will be introduced in a courtroom, ensuring evidence complies with the rules of criminal procedure. 

When keeping track of data or equipment for use in legal proceedings, it needs to remain in a pristine state. 

Therefore, documenting exactly who has had access to what for how long is vital when dealing with this situation. 

Any compromise in the data can lead to legal issues for the parties involved and can lead to a mistrial or contempt depending on the scenario 

### Mitigations 

- Patching 
- Data Execution Prevention

- Address space layout randomization
  - To make it harder for buffer overruns to execute privileged instructions at known addresses in memory.

- Principle of least privilege
  - Eg running Internet Explorer with the Administrator SID disabled in the process token. Reduces the ability of buffer overrun exploits to run as elevated user.

- Code signing
  - Requiring kernel mode code to be digitally signed.

- Compiler security features
  - Use of compilers that trap buffer overruns.

- Encryption
  - Of software and/or firmware components.

- Mandatory Access Controls
  - (MACs)
  - Operating systems with Mandatory Access Controls - eg. SELinux.

- "Insecure by exception"
  - When to allow people to do certain things for their job, and how to improve everything else. Don't try to "fix" security, just improve it by 99%.

- Do not blame the user
  - Security is about protecting people, we should build technology that people can trust, not constantly blame users. 
