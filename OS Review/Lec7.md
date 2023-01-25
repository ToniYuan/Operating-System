# Operating System
## Lec7 OS Security:
### There’s a big security problem with OS
Every computational device has one!
- A system is secure if resources used and accessed as intended(预期的) under all circumstances
  - Absolutely unachievable!
- Intruders(闯入者) will attempt to breach(突破) security
- A **threat** is a potential security violation(违反)
- An **attack** is an attempt to breach security
  - Attack can be accidental or malicious(恶意的)
- It’s easier to protect against accidental than malicious misuse
### Categories of security violation
- Breach of confidentiality(保密性)
  - Unauthorised reading of/ access to data
- Breach of integrity(诚信？？？)
  - Unauthorised modification of data
- Breach of availability
  - Unauthorised destruction of data
- Theft of service
  - Unauthorised use of resources
- Denial of service (DOS) (拒绝服务)
  - Prevention of legitimate use 
### Methods of security violation
Masquerading (breach authentication) ()伪装
- Pretending to be an authorised user to escalate privileges
Replay attack
- As-is or with message modification
Man-in-the-middle attack
- Intruder sits in data flow, masquerading as sender to receiver and vice versa
Session hijacking
- Intercept an already-established session to bypass authentication
Privilege escalation
- Common attack type with access beyond what a user or resource is supposed to have
### Four-layer security model
|**Types of attack**|           |**Prevention method**|
|:----------------------------------:|:-----------------------:|:-----------------------------:|
|Design flaws(缺陷)/ Code injection  |Application              |Sandboxing/ s/w restrictions|
|Platform vulnerabilities(漏洞)     |OS                       |Patches(补丁)/ Hardening    |
|Sniffing(偷窥)/Spoofing(欺骗)/Masquerading(伪装)|Network.      |Encryption/ Authentication  |
|Hardware based attacks            |Physical                  |Guards/Vaults/Encryption    |
### Threat type 1: Program/Application threats
Lots of variations!
**Trojan Horse**
- Code segment that misuses its environment
- Exploits mechanisms for allowing programs written by users to be executed by other users
- Spyware, pop-up browser windows, covert channels
- Up to 80% of spam delivered by spyware-infected systems
**Trap Door**
- Specific user identifier or password that circumvents normal security procedures
- Could be included in a compiler
- How can we detect them?
### Principle of Least Privilege
    All these methods try to violate this!
    “Only the minimum necessary rights should be assigned to a subject that requests access to a resource and should be in effect for the shortest duration necessary (remember to relinquish privileges). Granting permissions to a user beyond the scope of the necessary rights of an action can allow that user to obtain or change information in unwanted ways. Therefore, careful delegation of access rights can limit attackers from damaging a system.”
### Threat type 2: System/ Network threats
- Some systems are “open” rather than secure by default
  - Need to reduce attack surface
  - Harder to use, more knowledge needed to administer
- Network threats harder to detect, prevent
  - Protection systems weaker
  - More difficult to have a shared secret on which to base access
  - No physical limits once system attached to internet
### Security Fundamentals
- Typically in computing systems, we need to implement some form of security. This primarily comes down to ensuring correct access control and secure communication.
- Access control ensures that only an entity that is authorised to access, modify, or use a service/piece of information can do so.
- This becomes even more important in distributed, networked systems, such as Clouds and Web-based Software-as-a-Service (SaaS)
The communication medium is insecure - information in transit may be intercepted, read, or altered by unauthorised parties.
- Access control is centered around two important concepts: ○ Authentication
  - Authorisation
- End-to-end consistency of security mechanisms is required.
- While the source and destination systems for information transfer may be as secure as required, information may pass through intermediate systems; their degree of security must be specified (e.g. who is the weakest link?).
### Authentication
- The idea of authentication is to establish the identity of a principal involved in any computational procedure.
- For example, the use of a login procedure and a password is part of authentication. “You are who you say you are”, and it is up to the system to decide whether what you said can be trusted.
- A principal can be thought of as a process running a program on behalf of a logged-on user. A principal can also be a person, a program, a machine, or a device etc.
- Identity is typically based on knowledge of a secret, such as password, or possession of an object, such as a swipe card.
### Authorisation/ Validation
An authorisation policy specifies which principals may be allowed to access a service and in what way. The system must have mechanisms which can enforce the policies, i.e. policy enforcement.
- The access control policies and mechanisms may be damaged by the careless use of unchecked software.
- When you download and run a program, that program runs with all your access rights. It could read, overwrite or delete your files. It is therefore desirable that the source of software can be authenticated and verified (e.g. from a trusted site)!
### Encryption for secure comms
- Asymmetric encryption based on each user having two types of keys:
  - public key – published key used to encrypt data
  - private key – key known only to individual user used to decrypt data
- Must be an encryption scheme that can be made public without making it easy to figure out the decryption scheme (as long as the private key is secure and safe)
- Most common (although a bit old) is RSA encryption algorithm
- Efficient algorithm for testing whether or not a number is prime
- No efficient algorithm is known for finding the prime factors of a number (as long as the key is long enough)
### Digital Signatures
- In practice, encrypting and decrypting entire files would be an un-scalable practice in large-scale distributed systems
- We typically create a hash (eg. MD5/SHA1) of the file and encrypt that using our private key
- This encrypted hash is known as a digital signature of the file, i.e. the file is signed digitally
- Typically, a file system can compare two files using their hashes; when identical hashes are found, the two files are regarded as identical
It doesn’t secure a file, but can be used to confirm the contents are authentic.
