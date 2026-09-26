# 🔍 Network Traffic Analyzer

A hands-on network security project analyzing live/captured network packets with **Wireshark** to identify unencrypted traffic, anomalous DNS behavior, and common protocol-level security gaps — mapped against the **OSI** and **TCP/IP** models.

---

## 📌 Project Overview

This project involved capturing and analyzing network packets to understand real-world data flow and uncover common security weaknesses in network traffic. Using Wireshark as the primary analysis tool, I filtered traffic across multiple protocol layers, identified unencrypted HTTP communications, flagged suspicious DNS activity, and documented all findings in a structured technical report.

The goal was to build practical, applied skills in packet-level traffic analysis — the kind of foundational skill used in network security monitoring, incident response, and SOC analyst roles.

---

## 🎯 Objectives

- Capture and inspect live network traffic using Wireshark
- Identify **unencrypted HTTP traffic** carrying potentially sensitive data
- Detect **anomalous DNS activity** (e.g., unusual query patterns, suspicious domains, high query volume)
- Apply **OSI** and **TCP/IP** model concepts to interpret traffic at each layer
- Document findings in a clear, professional technical report

---

## 🛠️ Tools & Technologies

| Tool / Concept        | Purpose                                              |
|------------------------|-------------------------------------------------------|
| **Wireshark**          | Packet capture and protocol analysis                 |
| **Display Filters**    | Isolating HTTP, DNS, TCP, and other protocol traffic |
| **OSI Model**          | Mapping traffic behavior to network layers            |
| **TCP/IP Model**       | Understanding real-world protocol stack interactions |
| **Follow TCP Stream**  | Reconstructing full conversations between hosts       |

---

## 🔬 Methodology

1. **Packet Capture** – Captured live network traffic on a test network interface using Wireshark.
2. **Protocol Filtering** – Applied filters such as `http`, `dns`, `tcp.port == 80`, and `tcp.flags.syn == 1` to isolate traffic of interest.
3. **HTTP Analysis** – Used "Follow TCP Stream" to inspect unencrypted HTTP requests/responses for cleartext credentials, headers, and payload data.
4. **DNS Analysis** – Reviewed DNS query/response patterns to identify anomalies such as repeated queries to unfamiliar domains, unusually high query rates, and mismatched query/response behavior.
5. **Layer Mapping** – Cross-referenced observed traffic with OSI and TCP/IP layers (Application, Transport, Network, Link) to understand where each type of activity occurs and why it matters.
6. **Documentation** – Compiled all findings, filters used, and screenshots into a structured technical report (see [`TECHNICAL_REPORT.md`](./TECHNICAL_REPORT.md)).

---

## 🔑 Key Findings

- Identified multiple instances of **unencrypted HTTP traffic** transmitting data in cleartext, highlighting the risk of credential/data interception on unsecured networks.
- Detected **anomalous DNS query patterns**, consistent with behavior seen in malware beaconing or DNS tunneling scenarios.
- Demonstrated how easily plaintext protocols expose data to any party capable of observing network traffic (e.g., on shared/public networks).
- Reinforced the importance of **HTTPS/TLS** and encrypted DNS (DoH/DoT) in preventing this class of exposure.

---

## 📂 Repository Structure

```
network-traffic-analyzer/
│
├── README.md                 # Project overview (this file)
├── TECHNICAL_REPORT.md        # Full technical write-up of findings
├── screenshots/                # Wireshark capture screenshots (redacted)
│   └── .gitkeep
├── filters/                    # Wireshark display filters used
│   └── filters.txt
└── .gitignore
```

> ⚠️ **Note:** No raw `.pcap` capture files or real personal/organizational data are included in this repository, since packet captures can contain sensitive information. Screenshots are redacted/sanitized before upload.

---

## 📖 What I Learned

- Practical experience translating textbook OSI/TCP-IP theory into real packet-level analysis
- How to build and refine Wireshark display filters for efficient traffic triage
- How unencrypted protocols leak information, and why encryption (TLS, DoH/DoT) matters
- Recognizing baseline vs. anomalous DNS behavior — a core skill in threat detection

---

## 🚀 Future Improvements

- Automate anomaly detection using a script (Python + `pyshark`/`scapy`) instead of manual review
- Add a small lab setup (e.g., using GNS3/VirtualBox) to reproducibly generate sample traffic
- Correlate findings with a SIEM tool (e.g., Splunk, ELK) for alerting

---

## 👤 Author

**[Smriti Kharbanda]**
**[arorasmriti1245@gmail.com]**

