# Cyber Kill Chain Analysis
A comprehensive analysis of the 7 stages of the cyber kill chain, including detailed reports for my Network Security course. It showcases the intricate process of identifying, exploiting, and maintaining control over digital environments. Each phase is demonstrated through extensive security assessments, simulated attacks, and the implementation of defence strategies across various network setups and operating systems. Here's an overview of my journey through each stage:
## 1. Reconnaissance
I conducted a detailed security analysis to identify vulnerabilities within network environments. Here's how I approached this first step:

- **ZENMAP**: I used Zenmap for network mapping and port scanning, which revealed 29 active devices and key services like SSH and VNC at BCIT. This helped pinpoint potential security risks.
- **MALTEGO**: Employed for gathering open-source intelligence, Maltego helped me understand network connections and digital footprints effectively.
- **THEHARVESTER**: This tool was crucial for collecting publicly available information about domains, enhancing my understanding of the target's external exposure.
- **WAFW00F** and **WHATWEB**: I identified the absence of robust Web Application Firewalls and detailed the web technologies in use, which indicated potential entry points for web-based attacks.
- **WHOIS** and **DMITRY**: These provided comprehensive information on domain registration and network-related details, crucial for understanding the target's administrative landscape and potential vulnerabilities.

## 2. Weaponization
I demonstrated how attackers exploit known vulnerabilities within a network to establish unauthorized access and create opportunities for further malicious actions. My work focused on simulating an attacker's process of exploiting network defences through a combination of advanced tools and techniques.

Here's a breakdown of my approach and execution:
- **Nmap Reconnaissance**: The detailed initial scanning with Nmap provided crucial insights into the network's vulnerable points, guiding the targeted use of Metasploit to exploit these vulnerabilities.
- **Metasploit Framework**: Allowed me to exploit identified vulnerabilities effectively. Using the reconnaissance results from Nmap, I selected appropriate Metasploit modules that targeted specific weaknesses in network services.
- **Social Engineering Toolkit (SET)**: I utilized SET to enhance the attack’s scope by creating phishing schemes and infectious media. This showcased the human element's susceptibility to cybersecurity, emphasizing the effectiveness of social engineering in bypassing traditional security measures.
- **Exploitations Highlighted**:
  - **Vsftpd**: An exploitable backdoor was used to gain root access.
  - **OpenSSH**: Weak credentials were exploited to allow unauthorized system login.
  - **Samba and PostgreSQL**: Exploits provided elevated privileges within these services.
  - **VNC**: A weak password vulnerability was exploited to access the system remotely.

## 3. Delivery
I focused on the mechanisms through which vulnerabilities can be exploited, and attacks can be delivered to the targets. This stage was instrumental in applying theoretical vulnerabilities to practical attack simulations.

- **Burp Suite**: I utilized Burp Suite as a critical tool for intercepting, inspecting, and modifying web traffic. This enabled me to  identify and exploit web vulnerabilities such as SQL injection, XSS, command injection, and more within the Damn Vulnerable Web Application (DVWA). Burp Suite’s Intruder and Repeater tools were valuable for testing different types of web attacks.
- **Gophish**: I employed Gophish to simulate and understand the effectiveness of phishing attacks. It allowed me to set up and execute controlled phishing campaigns to collect Instagram and Spotify credentials.
- **Case Study Analysis**: I analyzed the July 2020 Twitter spear-phishing attack as a real-world example to understand the sophistication of social engineering and its impact on even well-prepared organizations.
## 4. Exploitation
I focused on actively exploiting identified vulnerabilities within a Metasploitable 2 machine. This stage was critical for demonstrating how attackers leverage security weaknesses to gain unauthorized access and control over network systems.

Here's how I approached the exploitation:

- **Initial Reconnaissance with Nmap**: I conducted an Nmap scan using the -sV flag on the target host at 10.0.0.86, which identified exploitable services such as an outdated IRC service and an HTTP service.
- **HTTP Service Investigation**: Using browser developer tools, I inspected HTTP response headers and discovered the server was running an outdated Apache version with vulnerable PHP configurations. Further examination of the robots.txt file uncovered plaintext credentials in the /passwords directory—a critical security oversight.
### Metasploit Framework Utilization:
- **HTTP and PHP Version Confirmation**: I used the auxiliary/scanner/http/http_version module to confirm service versions and further identified a remote code execution vulnerability in the cgi-bin directory using the searchsploit command.
- **Remote Code Execution**: I executed the exploit/multi/http/php_cgi_arg_injection module with a php/meterpreter/reverse_tcp payload, gaining a Meterpreter session and full access to the filesystem.
- **IRC Service Exploitation**: A Nmap script verified a backdoor in the UnrealIRCd service. I utilized a corresponding Metasploit exploit to obtain a command shell session, achieving root access with the whoami command.
#### Privilege Escalation:
- **Distcc Service Exploit**: I exploited a vulnerability using Metasploit’s distcc_exec module, which granted me access as the daemon user.
- **Glibc Library Exploit**: I escalated my privileges to root by exploiting a local vulnerability in the glibc library, enhancing my control over the system.
## 5. Installation
I focused on securing a stable foothold within the compromised system to maintain persistent access. Here’s an overview of the tools and methodologies I employed:

- **Strings and nm Tools**: I used the strings command to analyze binaries for exposed sensitive information, while the nm tool helped me understand the compiled binary’s structure and potential vulnerabilities without source code access.
- **Objdump**: This tool provided a deeper look into assembly-level operations and dependencies, crucial for identifying vulnerabilities that could be exploited.
- **System Call Tracing with Strace and Ltrace**: Monitoring system and library calls with these tools gave insights into the application’s interactions with the operating system.
- **VirusTotal Scans**: I conducted scans to check the integrity of files and URLs, using VirusTotal to ensure they were not recognized as malicious by antivirus engines.
- **Chkrootkit**: To guard against rootkits, I used Chkrootkit to scan for known threats and flag suspicious files.
## 6. Command and Control
I delved into the intricacies of managing and directing compromised systems through reverse shell attacks. This phase is pivotal as it demonstrates how attackers maintain communication with and control over infiltrated systems across various platforms.
Here's how I approached the command and Control
- **Ncat (Network Cat)**: I extensively used Ncat for its capability to handle inbound and outbound network connections which is instrumental in establishing reverse shells. This utility allowed me to create a listening state on the attacker's server, receive incoming connections from the target system, and execute commands remotely.
- **Reverse Shell Attacks**: I applied reverse shell techniques across different operating systems (Linux, Windows, macOS) to evaluate the effectiveness of C2 tactics under diverse environments. Using Linode as a simulated attacker's server.
- **Hardware-based Attacks**: I explored physical vulnerabilities by deploying a BadUSB attack using the `Flipper Zero` device on a macOS system. This experiment involved a keystroke injection attack via Ducky Script, which successfully compromised the system.
## 7. Actions on Objectives
I investigated password vulnerabilities using John the Ripper to illustrate the risks and effectiveness of different password-cracking methods. This phase is crucial as it directly addresses the attacker's goals of extracting valuable data or maintaining persistent access.

Approach and Execution:

- **Dictionary Attack**: I initiated this phase by conducting a dictionary attack using John the Ripper on my Kali Linux machine. This involved testing a series of passwords against the hashed passwords from user accounts I created. Using the rockyou.txt wordlist, I successfully cracked simple passwords like 'LAKERS', 'dolphin', and '123abc'.
- **Brute Force Attack**: After the dictionary attack, I shifted to a brute force approach. I ran John the Ripper in incremental mode over a span of 40 hours. Despite the extended duration, the brute force attack did not succeed in cracking the more complex password of my main account. It led to the compromise of only one additional account after an exhaustive 31 hours.

# Disclaimer
All the activities, demonstrations, and processes described in this repository are conducted in controlled environments designed for educational purposes only. This content is intended to demonstrate cybersecurity concepts, tools, and potential vulnerabilities within a legal and ethical framework. The techniques and methods shown are strictly for academic use and should not be applied without proper authorization and in compliance with all applicable laws and ethical guidelines.

I do not condone unauthorized or illegal use of the information and tools provided. Any misuse of this information to conduct criminal activities is strictly prohibited and is not endorsed by me. The responsibility lies solely with individuals who choose to apply or misuse the knowledge, tools, and techniques described herein.
