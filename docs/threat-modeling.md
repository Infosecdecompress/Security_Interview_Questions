# Threat Modeling

### How does threat modeling work?

Identify

* Potential threat

* Potential occurrence

* Concern Priority

* Means to eradicate or mitigate threat

Categorized

Analyze

### What is STRIDE?

- Spoofing : using someone else's credentials to gain access to otherwise inaccessible assets
- Tampering : Changing data to mount an attack
- Repudiation : Occurs when a user denies performing an action, but the target of the action has no     way to prove otherwise
- Information Disclosure : disclosure of information to a user who does not have permission to see it
- Denial of Service : Reducing the ability of valid users to access resources
- Elevation of Privilege :  occurs when an unprivileged user gains privileged status

### What is DREAD?

A risk-rating scheme that scores each threat (historically 1-10) across five factors and averages them to prioritize:
- **Damage** - how bad the impact is if exploited
- **Reproducibility** - how reliably it can be reproduced
- **Exploitability** - the effort/skill needed to exploit it
- **Affected users** - how many users are impacted
- **Discoverability** - how easily the flaw is found

Microsoft originally paired DREAD with STRIDE but later deprecated it because the scores are subjective and hard to keep consistent.

### Threat Modeling exercise examples
1. Instant messaging system
2. Password storage system
3. Ecommerce store
4. Given an application where a client wants to look up a service from service discovery provider
