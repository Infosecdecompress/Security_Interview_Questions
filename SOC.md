* What is considered as an investigation? 
  * An act of spending time and/or effort trying to find more information or an answer or a thing. 
* What is a Cybersecurity event vs incident? 
  * An event will be anything that happens related to cybersecurity, incident, will be an event that may cause damage or create risk to assets. 
* How do you use Python to write log parsers and/or utilities in scripting languages? 
* What is DevOps? Why is it useful?  
  * DevOps is a methodology that combines the software development part and the technology operation part. It makes software delivering, fixing bugs and providing updates easier and faster for both developer and operator.  
* Describe Your familiarity with DevOps philosophy and toolset (Ansible, Terraform, Jenkins, etc.) 
* What is Jenkins? Why use it? When do you use it? How do you use it? How is it helping the company? 
* What is Ansible? Why use it? When do you use it? How do you use it? How is it helping the company? 
* How do you automate tasks? 
* What is an investigation methodology?  
  * An investigation methodology is a framework or guidelines that gave you instruction or point you an direction at what you should do during an investigation. 
  * Describe what I will do, what tool I will use 
  * Example: 
    * First step 
      * Determine the severity 
      * CVSS Common Vulnerability Scoring System 
      * Assessing 
        * What happens? 
        * When? 
        * How? 
	    * What did you do? 
	    * When did you notice? 
	    * Create the timeline 
	    * What was the symtion? 
	    * How many people affected? 
	    * What is the effect / lost / impact ? 
	    * What's the impact for doing OOXX (Shut down X system)? 
    * Second step 
      * If life & death incident > move all the living away 
	  * Look into the logs 
	  * Collect the logs 
	  * Stop the incident from spreading ( contain /isolate / shutdown) 
	  * Impact analysis / damage analysis 
    * Third step 
	  * Start investigation 
	  * Collect the logs 
	    * Firewalls, IDS/IPS, web app, web server, server logs 
	    * Container > docker engine logs, K8s logs 
	  * Collect whatever is available 
	  * Analyze the logs 
	    * What you will do? 
	    * If SIEM, mention the tools 
		  * Splunk, Alienvault, Snort, Elastic Search 
	    * Utilize the SIEM, correlate the logs 
	    * Create the chain of events 
	    * Find answers for Who What When Why How 
* If there is a suspicious network security event found and you are assigned to investigate: 
  * what will you first do? 
    * Depends on the severity of the event, I will either isolate the system or start collecting information I need. 
  * what will you need to do? 
    * I'll need to notify proper personnel who is in charge, escalate the severity of the event if needed, document every events and the time it happened. 
  * what info do you need? 
    * If possible, I'll try to collect every information that I can get. If not, I'll try to get at least the logs from security devices like IDS or SIEM and make sure they are properly timestamped. 
  * what’s your plan to investigate? 
    * I'll follow the incident response procedure that I learnt in CISSP, which is notification, escalation, reporting, system isolation, forensic analysis, evidence handling 
  * who do you need to talk to? 
    * Manager of the security operation team, the manager of the system where the event happened, and legal counsel if required 
    * Ask: who do I work for? 
    * System owners, all the people that are impacted 
  * what results should you show? 
    * A timeline of when each events happened and how each of them are related, also provide a brief information about what the impact might be if possible 
    * what action has been taken, how to prevent things from happening again, find root cause to fix the problem 
  * How long is an investigation going to take? 
    * It depends on the size and the complexity of the event 
    * Depends on many things and how much resource do I have 
  * how do you know if it’s a true incident or not? 
    * It will be evaluated by all the actions made by the attacker along with the all the information we gathers, basically it will be determined by experience  
    * IoC / IoA (Indicator of Compromise / Indicator of Attack) 
    * Look for indicator / evidence by going through logs and SIEM 
  * how do you determine the chain of events happened in an incident? 
    * By finding some related parts in the information that we gathered, for example, a same source IP may indicates that two events are done by a same user.  
    * Find evidence in logs that we gathered 
  * what open source tools will you use to investigate an incident? 
    * I might be using a SIEM which can aggregate logs from different resource and virtualize the information, it will be able to help us find correlation between different log sources 
    * System internals (for Windows) 
      * Process explorer 
      * TCP Viewer, see open ports and activities 
      * Image dump, use sandbox to restore image and investigate 
  * what scripts will you likely write or have you written to help you investigate an incident? 
    * I will be writing some scripts that can identify some malicious activities and notify for me, for example, it may be finding a source IP that had sending requesting more than 10 times in a second. 
  * when do you consider the Investigation is done/complete? 
    * When we find the answer for the reason why we did this investigation, or when the cost of the investigation is exceeding the value of knowing the result of this investigation. 
    * When the budget time is up 
    * If we cannot move further > cannot find any evidence, may close the case or move to 3rd party investigation 
  * what do you do when the investigation is complete? 
    * Document everything and make sure is preserved for reference in the future if similar incidents happens 
  * How do you identify indicators of attack and create effective monitoring and alerting? 
    * Finding the root cause of the attack and see if there's any characteristic that will only appears in this type of attack, after identified the indicators of attack, I'll see if I can create firewall rules or filters to keep an eye on similar incidents that happens in the future 
  * what is Indicator of attacks? Name a few… 
    * Hash of a malware, known malicious source IP, unauthorized access attempts 
  * what do you do for post-mortem / lessons learned Report? 
    * I'll see if there's anything that we can do to help prevent similar incidents from happening again, some examples will be like firewall rules or even policy and guidelines. 
    * What is the root cause 
  * Often there will be stress to investigate suspected serious security incident in a tight timeline, if you only have limited info to start with, but you are required to get this analysis done in 2 days,  
    * what will you plan to do for 2 days?  
	  * I will try to set out some goals and list the tasks that need to be done then prioritize them and start with the most important tasks. 
    * What will you plan to deliver in 2 days?  
	  * I will be hoping to provide at least a broad picture of the incident and also includes some direction of what future works can be done 
    * What if you don’t have enough info to start with?  
	  * I will be seeking for helps from others and see if we can gather information that might be able to provide us a different view that we can start with  
    * What if you can’t get the report done in 2 days?  
	  * I will provide a report of what I've done and what is currently is be doing, at the same time kept on working with the investigation 
    * How often will you provide update before the deadline is up?  
	  * I will be providing updates when any of the goals are reached or tasks are done 
    * What resources will you need? 
	  * I will need all the logs with timestamps of the systems and devices that are related to the incident, I might also need a help from engineers of the system who have better understand about the system and how incident like that might happens. 
* what is IaaS?  
  * A IaaS, or Infrastructure as a Service, is one of the cloud service that the providers provide the server, storage and networking, the customers will take care of the OS and everything above that 
* How much do you know about AWS IaaS? 
  * I do have experience setting up AWS ECS and manage it, therefore I know how to set them up and how it works. 
* How do you get the logs from AWS IaaS? 
  * AWS do have a service called CloudWatch that will handle the logs and information from different AWS EC2 and other service, where you can view and manage the logs. If you want to see logs and console output for a single instance, it can be found in the Amazon EC2 console  
* What logs can you get from AWS IaaS logs? 
  * You will be able to get system logs, console output 
* what is IaaS vs PaaS vs SaaS? 
  * In IaaS, provider handles networking, virtual machines, storage. Client has the most flexibility but have to manage many things 
  * In PaaS, provider handles what's handled in IaaS and also OS, runtime and some of the software maintenance. 
  * In SaaS, provider handles everything, client can use the product directly without handling or maintaining anything. 
* How do you conduct an in-depth vulnerability assessments and information system auditing of assets (e.g. servers, Workstations, Network Appliances, Storage Devices, and Applications)? 
  * what is the methodology? 
  * what info do you need to start the assessment? 
  * what tools do you use to conduct a vuln assessment? 
  * what are the key items you need to ask / define before starting a vuln assessment?  
  * what is considered as a vulnerability in your opinion? 
  * if you find a vuln and you are not sure if it is exploitable, what will you do? 
  * what is the difference between penetration testing vs Vulnerability Assessment? 
  * what should you include in a vuln assessment report? 
  * Example 
    * Ask questions: 
    * What is the scope? 
    * What do you want me to assess? 
    * When do you want me to do the test? Date? Time? 
    * Is this live system or testing system? 
    * Is there a backup? 
    * Black box? Grey box? White box? 
    * Rule of engagement? 
    * Can I do OOXX attack? 
  * Report example 
    * Executive summary 
	  * What did I do 
	  * When I start / end 
	  * The scope of assess 
	  * What test I ran 
	  * What I found 
	  * The servility of the things I found 
    * Methodology 
	  * How did I do it 
	  * What tools I used 
    * Vulnerabilities 
	  * Description of the vulnerable 
	  *  what I found 
	  * How to recreate the issue (include all the steps) 
	    * If you cannot recreate it, it's not an issue 
	  * Actual risk / actual impact 
* Have you heard of Indicator of Compromise (IOC)? 
* How do you use IoC to help you in an investigation? 
* Will you use OSInt?  
* What is OSInt? How do you use it? Any tools you will use to help you? 
  * dig 
  * Censys 
  * Shodan 
  * Whois 