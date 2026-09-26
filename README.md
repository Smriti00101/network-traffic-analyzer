 🔍 Network Traffic Analyzer

A hands-on network security project analyzing network packets with **Wireshark** to identify unencrypted traffic, anomalous DNS activity, and common security gaps — using OSI and TCP/IP model concepts.

 📌 Overview

This project involved capturing and analyzing network packets using Wireshark to understand real-world data flow and uncover common security weaknesses in network traffic. I filtered traffic across multiple protocol layers, identified unencrypted HTTP communications, flagged suspicious DNS activity, and documented findings in a technical report.

 🎯 Objectives

- Capture and inspect live network traffic using Wireshark
- Identify unencrypted HTTP traffic carrying sensitive data
- Detect anomalous DNS activity
- Apply OSI and TCP/IP model concepts to interpret traffic
- Document findings in a clear technical report

 🛠️ Tools Used

- **Wireshark** – packet capture and protocol analysis
- **Display Filters** – isolating HTTP, DNS, and TCP traffic
- **OSI / TCP-IP Models** – mapping traffic to network layers

🔬 Methodology

1. Captured live network traffic using Wireshark
2. Applied filters (`http`, `dns`, `tcp.port == 80`) to isolate relevant traffic
3. Used "Follow TCP Stream" to inspect unencrypted HTTP data
4. Analyzed DNS query patterns for anomalies
5. Mapped findings to OSI/TCP-IP layers
6. Documented results in `TECHNICAL_REPORT.md`

 🔑 Key Findings

- Identified unencrypted HTTP traffic transmitting data in cleartext
- Detected anomalous DNS query patterns
- Demonstrated the risk of plaintext protocols on unsecured networks
- Reinforced the importance of HTTPS/TLS and encrypted DNS

 📖 What I Learned

- Applying OSI/TCP-IP theory to real packet-level analysis
- Building Wireshark filters for efficient traffic triage
- Recognizing normal vs. anomalous DNS behavior

👤 Author
Smriti Kharbanda
