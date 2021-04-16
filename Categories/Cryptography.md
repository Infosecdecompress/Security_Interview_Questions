# Cryptography

### Asymmetric vs symmetric

Asymmetric is slow, but good for establishing a trusted connection.

Symmetric has a shared key and is faster. Protocols often use asymmetric to transfer symmetric key.

Perfect forward secrecy - eg Signal uses this.

#### Encryption standards + implementations

Symmetrical

* DES
* RCx
* Blowfish
* Rijndael ([AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)) 
* [Chacha/Salsa](https://en.wikipedia.org/wiki/Salsa20#ChaCha_variant)

Asymmetrical

- [RSA (asymmetrical)](https://en.wikipedia.org/wiki/RSA_(cryptosystem)).
- [ECC (namely ed25519) (asymmetric)](https://en.wikipedia.org/wiki/EdDSA)
- Diffie Hellman
- El Gamal
- DSAC 

### SSL & TLS

#### Different between SSL \ TLS \ HTTPS 

SSL:  standard technology for keeping an internet connection secure and safeguarding any sensitive data that is being sent between two systems, preventing criminals from reading and modifying any information transferred, including potential personal details. 

TLS: cryptographic protocol that provides secure communication over the Internet. TLS protocol aims primarily to provide privacy and data integrity between two communicating computer applications. 

HTTPS: secure version of HTTP, the protocol over which data is sent between your browser and the website that you are connected to. TLS and SSL are most widely recognized as the protocols that provide secure HTTP (HTTPS) for Internet transactions between Web browsers and Web servers. 

HTTPS uses TCP at the transport layer. SSL is used for data encryption. 

#### Does TLS use symmetric or asymmetric encryption? 

Both,  initial exchange is done using asymmetric and that bulk data encryption requires speed and therefore symmetric algorithms. 

#### What is HTTP Strict Transport Security (HSTS)?

HSTS is a header which allows a website to specify and enforce security policy in client web browsers. This policy enforcement protects secure websites from downgrade attacks, SSL stripping, and cookie hijacking. It allows a web server to declare a policy that browsers will only connect using secure HTTPS connections, and ensures end users do not “click through” critical security warnings. HSTS is an important security mechanism for high security websites. HSTS headers are only respected when served over HTTPS connections, not HTTP.

HSTS generally has the following behavior in user web browsers:

- Insecure HTTP links become secure HTTPS links
- SSL certificate warnings or other errors show an error message and cannot be bypassed by the user

More details: [Cloudflare Understanding HSTS (HTTP Strict Transport Security)](https://support.cloudflare.com/hc/en-us/articles/204183088-Understanding-HSTS-HTTP-Strict-Transport-Security-)

#### If someone steals the server’s private key can they decrypt all previous content sent to that server? 

#### What are some common ways that TLS is attacked, and/or what are some ways it’s been attacked in the past? 

weak ciphers, vulnerabilities like Heartbleed, BEAST, 

#### What is Forward Secrecy? 

a system that uses ephemeral session keys to do the actual encryption of TLS data so that even if the server’s private key were to be compromised, an attacker could not use it to decrypt captured data that had been sent to that server in the past. 

### Public Key Infrastructure

#### Cryptographically speaking, what is the main method of building a shared secret over a public medium? 

Diffie-Hellman 

#### What’s the difference between Diffie-Hellman and RSA? 

Diffie-Hellman is a key-exchange protocol, and RSA is an encryption/signing protocol. RSA required key material beforehand, DH does not 

#### What kind of attack is a standard Diffie-Hellman exchange vulnerable to? 

MITM 

### What’s the difference between encoding, encryption, hashing,  Obfuscation, and Signing? 

[Various attack models (e.g. chosen-plaintext attack)](https://en.wikipedia.org/wiki/Attack_model).

### What is an IV used for in encryption? 

### Cipher Modes

#### What are block and stream ciphers? What are the differences, and when would you use one vs. the other? 

Block-based encryption algorithms work on a block of cleartext at a time, and are best used for situations where you know how large the message will be, e.g., for a file. Stream ciphers work on single units of cleartext, such as a bit or a byte, and they’re best used when you’re not sure how long the message will be. 

- [Block vs stream ciphers](https://en.wikipedia.org/wiki/Cipher).
- [Block cipher modes of operation](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation).
- [AES-GCM](https://en.wikipedia.org/wiki/Galois/Counter_Mode).

#### What are some common block cipher modes? 

ECB (Electronic Code Book) and CBC (Cipher Block Chaining). 

#### What’s the main difference in security between ECB and CBC? 

ECB (Electronic Code Book) just does a one-to-one lookup for encryption, without using an IV, which makes it fairly easy to attack using a chosen-plaintext attack. 

CBC (Cipher Block Chaining) uses an IV for the first block and then propagates the XOR of the previous block onto subsequent ones. The difference in results can be remarkable. 

### Integrity and authenticity primitives

- [Hashing functions, e.g. MD5, Sha-1, BLAKE](https://en.wikipedia.org/wiki/Cryptographic_hash_function). Used for identifiers, very useful for fingerprinting malware samples.
- [Message Authentication Codes (MACs)](https://en.wikipedia.org/wiki/Message_authentication_code).
- [Keyed-hash MAC (HMAC)](https://en.wikipedia.org/wiki/HMAC).

### Entropy

- PRNG (pseudo random number generators).
- Entropy buffer draining.
- Methods of filling entropy buffer.

### What are the different ways in which the authentication of a person can be performed 

1. Passwords: Something user know 
2. Token: Something user have 
3. Biometrics: Someone user is 
4. OTP: one time password 

### Security Modules

#### What is HSM Hardware Security Module?

A security device you can add to a system to manage, generate, and securely store cryptographic keys.

#### What is TPM Trusted Platform Modules?

A hardware chip on the computer’s motherboard that stores cryptographic keys used for encryption. Many laptop computers include a TPM, but if the system doesn’t include it, it is not feasible to add one.

Trusted storage for certs and auth data locally on device/host.

#### HSM vs TPM

HSMs are removable or external devices. In comparison, a TPM is a chip embedded into the motherboard. You can easily add an HSM to a system or a network, but if a system didn’t ship with a TPM, it’s not feasible to add one later. Both provide secure encryption capabilities by storing and using RSA keys.