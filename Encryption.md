* SSL \ TLS \ HTTPS 
  * SSL:  standard technology for keeping an internet connection secure and safeguarding any sensitive data that is being sent between two systems, preventing criminals from reading and modifying any information transferred, including potential personal details. 
  * TLS: cryptographic protocol that provides secure communication over the Internet. TLS protocol aims primarily to provide privacy and data integrity between two communicating computer applications. 
  * HTTPS: secure version of HTTP, the protocol over which data is sent between your browser and the website that you are connected to. TLS and SSL are most widely recognized as the protocols that provide secure HTTP (HTTPS) for Internet transactions between Web browsers and Web servers. 
  * HTTPS uses TCP at the transport layer. SSL is used for data encryption. 
* Does TLS use symmetric or asymmetric encryption? 
  * Both,  initial exchange is done using asymmetric and that bulk data encryption requires speed and therefore symmetric algorithms. 
* If someone steals the server’s private key can they decrypt all previous content sent to that server? 
* What are some common ways that TLS is attacked, and/or what are some ways it’s been attacked in the past? 
  * weak ciphers, vulnerabilities like Heartbleed, BEAST, 
* What is Forward Secrecy? 
  * a system that uses ephemeral session keys to do the actual encryption of TLS data so that even if the server’s private key were to be compromised, an attacker could not use it to decrypt captured data that had been sent to that server in the past. 
* Cryptographically speaking, what is the main method of building a shared secret over a public medium? 
  * Diffie-Hellman 
* What’s the difference between Diffie-Hellman and RSA? 
  * Diffie-Hellman is a key-exchange protocol, and RSA is an encryption/signing protocol. RSA required key material beforehand, DH does not 
* What kind of attack is a standard Diffie-Hellman exchange vulnerable to? 
  * MITM 
* What’s the difference between encoding, encryption, and hashing? 
* What is an IV used for in encryption? 
* What are block and stream ciphers? What are the differences, and when would you use one vs. the other? 
  * Block-based encryption algorithms work on a block of cleartext at a time, and are best used for situations where you know how large the message will be, e.g., for a file. Stream ciphers work on single units of cleartext, such as a bit or a byte, and they’re best used when you’re not sure how long the message will be. 
* What are some examples of symmetric encryption algorithms? 
  * DES, RCx, Blowfish, Rijndael (AES) 
* What are some examples of asymmetric encryption algorithms? 
  * Diffie Hellman, RSA, EC, El Gamal, DSAC 
* What are some common block cipher modes? 
  * ECB and CBC. 
* What’s the main difference in security between ECB and CBC? 
  * ECB just does a one-to-one lookup for encryption, without using an IV, which makes it fairly easy to attack using a chosen-plaintext attack. CBC uses an IV for the first block and then propagates the XOR of the previous block onto subsequent ones. The difference in results can be remarkable. 
* What are the different ways in which the authentication of a person can be performed 
  * Passwords: Something user know 
  * Token: Something user have 
  * Biometrics: Someone user is 
  * OTP: one time password 