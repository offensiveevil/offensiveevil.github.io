---
title: Cobalt Strike Attack and Defend
date: 2024-01-08 00:00:00 +0800
categories: [Cobalt Strike]
tags: [Offensive Security, Cobalt Strike]
render_with_liquid: false
---

<blockquote class="lf lg lh"><p id="8bfc" class="li lj lk ll b lm ln lo lp lq lr ls lt lu lv lw lx ly lz ma mb mc md me mf mg fi bj" data-selectable-paragraph="">Disclaimer: This blog serves solely for educational purposes. The author advocates for legal and ethical usage and does not support any unauthorized or malicious activities. The content is provided for educational use only, and readers are accountable for their actions and any resulting consequences.</p></blockquote>

<img alt="image" src="../images/image2.webp" height="50%" width="80%" style="display: block; margin: 0 auto;">

<p style="text-align: justify;">This blog navigates the complex terrain of cybersecurity, focusing on the advanced tactics in cyberattacks and the key role of digital forensics in analyzing these threats, reflecting a rising trend in cybersecurity risks. It aligns with key cybersecurity topics, notably in computer forensics and anti-forensics, as evidenced by detailed analyses of Cobalt Strike payloads and digital forensic techniques. Additionally, the blog enhances understanding of threat intelligence and the evolution of digital crimes. It also addresses the challenges in analyzing Cobalt Strike beacons, which are designed for evasion and persistence, complicating detection and analysis.</p>

<blockquote class="lf lg lh"><p id="8bfc" class="li lj lk ll b lm ln lo lp lq lr ls lt lu lv lw lx ly lz ma mb mc md me mf mg fi bj" data-selectable-paragraph="">The blog will be structured into two distinct parts: the first will detail the attack scenario, while the second part will focus on digital forensics.</p></blockquote>

<p style="text-align: justify;">In my blog, I will offer a brief and clear explanation of Cobalt Strike, outlining its basic functions and significance in cybersecurity. This will serve as an introduction or primer to the topic. For a more detailed exploration, readers can refer to the in-depth blog by my esteemed friend, batchmate, and coworker Mingmar Lama titled “Demystifying Cobalt Strike” which provides a comprehensive analysis of Cobalt Strike and its applications.</p>

<h1>Cobalt Strike</h1>

<p style="text-align: justify;">Cobalt Strike is a commercial penetration testing tool, renowned for its capability to simulate advanced cyber threats. Introduced in 2012 by Raphael Mudge, Cobalt Strike was designed to replicate the tactics, techniques, and procedures (TTPs) used by sophisticated attackers, providing security professionals with a robust platform for assessing the security of networks and systems.</p>

<img alt="image" src="../images/image3.png" height="50%" width="80%" style="display: block; margin: 0 auto;">

<p style="text-align: justify;">Recently, Advanced Persistent Threat (APT) groups have increasingly used Cobalt Strike. Below are some notable cyber threat incidents involving Cobalt Strike:</p>

<p style="text-align: justify;"><b>APT29 and Cobalt Strike (2018):</b> APT29, a hacking group, used Cobalt Strike in their assaults on the U.S. energy sector. They utilized it for network infiltration, payload execution, and theft of sensitive data, including login credentials and financial information (Mandiant, 2021).</p>
<p style="text-align: justify;"><b>Lazarus Group (2019):</b> The Lazarus hacking group employed Cobalt Strike in their attacks targeting banks and financial institutions. Their activities included network infiltration, backdoor execution, and stealing critical data such as customer records and transaction details (SentinelOne, 2023).</p>

<p style="text-align: justify;"><b>Emissary Panda’s Operations (2020):</b> In their attacks on government entities and defense contractors, the Emissary Panda group utilized Cobalt Strike for network penetration, malware deployment, and exfiltration of sensitive information like classified documents and research data (SentinelOne, 2023).</p>

<p style="text-align: justify;"><b>Trickbot Operators (2020):</b> Operators of Trickbot used PowerTrick and Cobalt Strike to implement their Anchor backdoor and deploy RYUK ransomware (Cisco Talos , 2022).</p>

<p style="text-align: justify;"><b>APT Attackers and CobaltStrike Beacon:</b> APT attackers employed a CobaltStrike beacon, using a previously unknown persistence method through DLL hijacking, to connect to a company’s VPN via a public PureVPN node (SentinelOne, 2023).</p>

<p style="text-align: justify;"><b>LockBit Ransomware and Cobalt Strike:</b> LockBit ransomware discovered a novel method to bypass security measures by utilizing a Windows Defender command-line tool to decrypt and execute Cobalt Strike payloads (Toulas, 2022).</p>

<h1>Starting the Cobalt Strike Teamserver and Crafting a Stageless payload</h1><br>

<blockquote class="lf lg lh"><p id="8bfc" class="li lj lk ll b lm ln lo lp lq lr ls lt lu lv lw lx ly lz ma mb mc md me mf mg fi bj" data-selectable-paragraph="">Disclaimer: The use of cracked or unauthorized versions of Cobalt Strike software is strictly prohibited and not encouraged. Users are advised to handle such tools responsibly and ethically, adhering to legal and professional standards.</p></blockquote>

<img alt="image" src="../images/image24.png" height="50%" width="80%" style="display: block; margin: 0 auto;">

<p style="text-align: justify;">The Cobalt Strike team server is initiated and hosted on a public IP address. This setup enables the Cobalt Strike graphical user interface (GUI) client to effectively communicate and interact with the Cobalt Strike server. This configuration is essential for establishing the necessary command and control infrastructure for operations.</p>

<img alt="image" src="../images/image25.jpeg" height="50%" width="80%" style="display: block; margin: 0 auto;">

<p style="text-align: justify;">The client establishes a connection with the Cobalt Strike server by inputting the required credentials. For security and confidentiality purposes, these credentials have been omitted from this documentation.
</p>

<img alt="image" src="../images/image26.jpeg" height="50%" width="80%" style="display: block; margin: 0 auto;">

<p style="text-align: justify;">Following the successful establishment of the connection, access to the Cobalt Strike graphical user interface (GUI) is now available.
</p>

<img alt="image" src="../images/image27.jpeg" height="50%" width="80%" style="display: block; margin: 0 auto;">

<p style="text-align: justify;">In this operation, Cobalt Strike’s extensive payload capabilities are utilized, with a particular focus on the Windows Stageless payload.</p>

<img alt="image" src="../images/image28.png" height="50%" width="80%" style="display: block; margin: 0 auto;">

<p style="text-align: justify;">The operation progresses with the establishment of a listener, designed to receive and manage connections from the Cobalt Strike beacon. This listener is configured to operate on port 1234.</p>

<img alt="image" src="../images/image29.jpeg" height="50%" width="80%" style="display: block; margin: 0 auto;">

<p style="text-align: justify;">A Windows PowerShell stageless payload is generated, and the previously set up listener is employed to handle the reverse connection, in the event of a successful connection establishment.</p>

<img alt="image" src="../images/image30.jpeg" height="50%" width="80%" style="display: block; margin: 0 auto;">

<p style="text-align: justify;">The payload has been successfully crafted, and the listener is now configured and ready to capture the incoming connection.</p>

<h1>Delivering and waiting for the execution of the Cobalt Strike Beacon</h1><br>

<img alt="image" src="../images/image4.jpeg" height="50%" width="80%" style="display: block; margin: 0 auto;">

<p style="text-align: justify;">In order to deliver the malicious payload, a scenario is contrived where an email, appearing to be from the IT support team, urgently requests employees to run a PowerShell script. This script is purportedly necessary for adhering to recent changes made within the organization’s network. The email is crafted to create a sense of urgency, emphasizing the importance of immediate compliance to avoid potential issues, thereby persuading the recipients to execute the payload without suspicion..</p>

<img alt="image" src="../images/image5.jpeg" height="50%" width="80%" style="display: block; margin: 0 auto;">

<p style="text-align: justify;">Following the successful execution of the payload, it initiates a callback to the previously configured listener. This action signifies that the computer has now been compromised, as the payload has established communication with an external controller, potentially allowing unauthorized access and control over the system.</p>

<img alt="image" src="../images/image6.jpeg" height="50%" width="80%" style="display: block; margin: 0 auto;">

<p style="text-align: justify;">When granted administrator privileges, Cobalt Strike has the capability to run Mimikatz, resulting in the dumping of NTLM hashes from the compromised computer.</p>
