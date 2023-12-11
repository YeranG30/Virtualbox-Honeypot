# Virtualbox-Honeypot

# Overview
This documentation outlines the process of setting up a VirtualBox Honeypot using Docker and Cowrie, a medium interaction SSH and Telnet honeypot designed to log brute force attacks and the shell interaction performed by the attacker.

# Steps
# 1. Setting Up the Honeypot

``` sudo docker run -p 2222:2222 cowrie/cowrie:latest ```

Description: This command downloads the Cowrie image and runs it, mapping port 2222 of the host to port 2222 of the container. 
The selection of port 2222 was strategic: it is obscure enough not to be overly prominent, yet sufficiently commonplace to appear realistic to a hacker, thereby avoiding raising suspicion. 

  <img width="352" alt="image" src="https://github.com/YeranG30/VIrtualbox-Honeypot/assets/74067706/0e164073-2329-410b-948b-120da26f646c">

# 2. Scanning the Honeypot with Nmap (Hackers Perspective)

Running a simple Nmap scan from the perspective of a hacker simulates foreign active reconnaissance.

```nmap -sV host_ip```

Description: This scans the honeypot host to discover open ports and service versions.

Expected Result: Port 2222 should appear as open, possibly identified as OpenSSH or a similar service.

![image](https://github.com/YeranG30/VIrtualbox-Honeypot/assets/74067706/7a917be7-dfe1-4581-b36e-90b6a3433407)

# 3. Simulating Black Hat activity 

Attempt to SSH into the Honeypot: Use an SSH client to connect to the Honeypot on port 2222.
 ``` ssh -p 2222 user@host_ip ``` 
 
Description: This simulates an attacker trying to SSH into the honeypot.

![image](https://github.com/YeranG30/VIrtualbox-Honeypot/assets/74067706/17b73bc9-5d78-47d3-b1fe-1cdde067ecfe)

From the hacker's perspective, they might attempt to SSH into the machine under the assumption that it's a legitimate SSH server. However, unbeknownst to them, they are accessing a decoy server – a honeypot – which is designed to capture their information and log all their activities. I have simulated malicious prompts by a hacker to the SSH server, where a real hacker would try and either perform privilege escalation, information stealing, or any other form of black hat activity.  

![image](https://github.com/YeranG30/VIrtualbox-Honeypot/assets/74067706/2e583925-4eab-4989-a210-9fe64f5813d0)


# 4. Honeypot Interaction Logging
When a hacker logs into a honeypot, the system can capture a wide range of data depending on its configuration and capabilities. Here are some key pieces of information and activities that a honeypot typically records:

1. Source IP Address: The IP address of the attacker's machine, which is crucial for identifying the source of the attack.
   <img width="240" alt="image" src="https://github.com/YeranG30/Virtualbox-Honeypot/assets/74067706/d1e813f2-afc0-4f65-8975-a267f559295d">


2. Timestamps: Exact times of each action, helping in creating a timeline of the attack.
   <img width="172" alt="image" src="https://github.com/YeranG30/Virtualbox-Honeypot/assets/74067706/3b3df98a-1222-4598-b425-005ab71c52d6">

3. Login Credentials Used: Any usernames and passwords attempted by the hacker.
   <img width="819" alt="image" src="https://github.com/YeranG30/Virtualbox-Honeypot/assets/74067706/0f3926a4-aa07-4d61-b535-32e1fe276660">


7. Commands Executed: Detailed logs of commands entered by the attacker, which can reveal their intentions and techniques.
  <img width="910" alt="image" src="https://github.com/YeranG30/Virtualbox-Honeypot/assets/74067706/c2d08f48-cf6b-4c63-9616-2f921e5defb8">

Network Activity: Data on any outbound or inbound connections initiated by the attacker, including attempts to contact other servers or download additional tools.

![image](https://github.com/YeranG30/VIrtualbox-Honeypot/assets/74067706/612e8f34-a181-41cb-af3c-11103098478a)


Comprehensive Activity Logging in the Honeypot: Extensive Activity Monitoring Logs within the Honeypot - These logs provide a thorough record of all actions taken by a hacker inside the honeypot, ensuring that every command, movement, and interaction is meticulously captured and archived for analysis.

![image](https://github.com/YeranG30/VIrtualbox-Honeypot/assets/74067706/b1ca5689-7cef-44a7-8630-1b220fbc857d)

# Conclusion
The VirtualBox Honeypot project, utilizing Docker and Cowrie, serves as a practical and insightful exploration into cybersecurity defense mechanisms. Through the setup and operation of this medium interaction SSH and Telnet honeypot, I've gained valuable hands-on experience in understanding and mitigating brute force attacks and other malicious activities.

Key Learnings:

Strategic Deployment: The deployment of Cowrie on port 2222, balancing obscurity with realism, exemplifies the tactical considerations necessary in cybersecurity. This decision-making process highlighted the importance of thinking like potential attackers to effectively deter them.

Reconnaissance and Response: Simulating an Nmap scan from a hacker's perspective was crucial in understanding how attackers gather information and how honeypots can be designed to deceive them. This exercise reinforced the significance of being proactive in cybersecurity measures.

Attack Simulation: Engaging directly with the honeypot via SSH provided a first-hand view of how attackers might perceive and interact with a seemingly legitimate SSH server. This simulation was pivotal in appreciating the subtleties of honeypot design and its effectiveness in trapping unsuspecting hackers.

Logging and Analysis: The extensive logging of SSH access and comprehensive activity within the honeypot was instrumental in understanding the value of data collection in cybersecurity. Analyzing these logs offered insights into hacker behaviors, tactics, and potential vulnerabilities in the system.

Ethical Implications: The project underscored the ethical considerations in setting up and managing honeypots. It emphasized the need for responsible use of honeypot data and compliance with legal standards.

Overall, this project has been a robust educational journey in cybersecurity. It has enhanced my understanding of honeypot deployment, attacker psychology, and the importance of vigilant monitoring and logging. The experience gained from this project is invaluable for anyone looking to deepen their knowledge in network security and cyber defense strategies.



