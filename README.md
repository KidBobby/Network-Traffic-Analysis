# Network-Traffic-Analysis
Network Traffic Analysis and Unencrypted Protocol Auditing



INTRODUCTION


This project focuses on the analysis and identification of security risks in network traffic data collected with Wireshark. The goal is to identify network communication patterns and detect how unencrypted protocols expose data across a shared connection. The data represents live network activity captured during a browsing session, including source and destination IP addresses, protocol types, and packet lengths. By looking closely at the packet payloads, this study highlights areas where plain text leaves systems exposed to eavesdropping.

TECHNICAL OVERVIEW


This project was created using Wireshark for packet capture and stream reconstruction. The data reveals exactly how a web browser interacts with an unsecure web platform versus normal background traffic. The analysis processes network statistics, tracks exposed configuration values, and maps out user device fingerprints, while Wireshark's stream reassembly engine reconstructs the exact plain text communication logs.


CONTRIBUTION


This project was completed to develop my practical skills in network security monitoring and data collection. I was responsible for capturing the raw traffic, filtering out background noise, and analyzing the raw hexadecimal and ASCII data streams. In order to identify the risks of unencrypted traffic, I also analyzed specific packet headers. This process improved my technical proficiency with packet inspection tools as well as my practical understanding of transport-layer security gaps.


METHODOLOGY and MILESTONES


The network traffic was captured, filtered, and analyzed to ensure a clear view of the session. The final documentation displays key aspects of the network interaction, including:
• Protocol distribution (Encrypted vs. Unencrypted)
• Application-layer header values
• Cleartext payload exposure
Stream reconstruction techniques were applied to identify unusual exposure patterns. This process involved:
• Traffic Baselining: Monitoring background network packets to see what normal, secure traffic looks like.
• Protocol Filtering: Isolating HTTP text data from encrypted TLS traffic.
• Stream Inspection: Reassembling the exact text conversation between my PC and the remote server

RESULTS

Protocol Distribution
From the initial capture, encrypted traffic completely dominates the network under normal conditions.


<img width="1920" height="1080" alt="Screenshot 2026-06-07 103936" src="https://github.com/user-attachments/assets/059c83fa-f932-4613-8fa8-0dce6cc82a8e" />


This proves that normal internet traffic is hidden by secure encryption layers.
When moving to an unsecure connection, applying the http display filter immediately drops the background noise down to 10 specific packets.





<img width="1920" height="1080" alt="Screenshot 2026-06-07 105555" src="https://github.com/user-attachments/assets/364dae93-2d24-49de-907a-16c6b43202a3" />

This demonstrates how targeting a specific protocol isolates unencrypted web data from thousands of background connections.



TARGET ENVIRONMENT AND PUBLIC ROUTING


During the active capture session, the connection path was established to an unsecure captive portal testing environment.

<img width="1920" height="1080" alt="Screenshot 2026-06-07 120630" src="https://github.com/user-attachments/assets/cf6108fa-df7e-4718-887d-74a29c87078f" />

 This captures the user-side scenario where data protection is dropped completely, broadcasting the session over the network.



 ANALYSIS AND DISCUSSION


 The reassembled data stream shows critical information leaks from both the client side and the server side.
 

 <img width="1920" height="1080" alt="Screenshot 2026-06-07 105636" src="https://github.com/user-attachments/assets/f9ddb98b-e161-41af-bdfc-63d4e9ec8b3f" />

 This is the raw transcript of the conversation traveling over the network in clear text.
Key Analytical Findings:
• Client Device Fingerprinting: Inside the request headers (red text), the system leaks User-Agent: Mozilla/5.0 (Windows NT 10.0; ...) Edg/149.0.0.0. This tells anyone watching the network that the source device is running Windows 10/11 and using the Microsoft Edge browser version 149. This allows an attacker to profile the device and look up specific software exploits without running an aggressive scan.
• Server Infrastructure Disclosure: The remote web server answers with Server: nginx/1.24.0 (Ubuntu). This leaks the exact backend software version and operating system of the website, giving attackers a roadmap of the server setup.
• Payload Exposure: The actual underlying website structure travels completely unprotected.

    This proves that an inline attacker could read or completely modify the webpage content in transit because there are no encryption integrity checks.

CONCLUSION


The analysis of network traffic, primarily contrasting protocols like TCP/TLS against plain HTTP, reveals typical communication behaviors alongside severe exposure risks that require attention. The concentration of plaintext data within standard HTTP streams highlights major security vulnerabilities, pointing to areas where data can be easily intercepted or modified mid-air.
The identified patterns show that using unsecure protocols allows simple device fingerprinting and infrastructure mapping. To fix this, networks must enforce secure HTTPS connections everywhere and implement strict transport security policies to ensure data efficiency and eliminate simple security bottlenecks.

    


 
