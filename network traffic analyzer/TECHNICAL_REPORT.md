# Technical Report: Network Traffic Analysis Using Wireshark

**Author:** [Smriti Kharbanda]
**Tool Used:** Wireshark v[X.X]

---

## 1. Objective

The purpose of this analysis was to capture and inspect network traffic to identify security-relevant patterns — specifically unencrypted HTTP communication and anomalous DNS activity — and to interpret the traffic in the context of the OSI and TCP/IP models.

## 2. Environment / Setup

- **Capture interface:** [e.g., Wi-Fi adapter / Ethernet / loopback / test VM]
- **Capture duration:** [e.g., 30 minutes]
- **Network type:** [e.g., isolated lab network / home network — no third-party production traffic captured]
- **Wireshark version:** [X.X]

## 3. Methodology

1. Started a live capture in Wireshark on the target interface.
2. Generated representative traffic (web browsing, DNS lookups) in a controlled environment.
3. Applied protocol-specific display filters to isolate traffic of interest.
4. Used "Follow TCP Stream" to reconstruct full application-layer conversations.
5. Cross-mapped each traffic type to its corresponding OSI/TCP-IP layer.
6. Captured screenshots (redacted) of key findings for documentation.

### Filters Used

| Filter | Purpose |
|---|---|
| `http` | Isolate all HTTP (unencrypted) traffic |
| `dns` | Isolate all DNS queries and responses |
| `tcp.port == 80` | Show traffic on the standard HTTP port |
| `tcp.flags.syn == 1 && tcp.flags.ack == 0` | Identify TCP connection initiations (SYN scans/handshakes) |
| `dns.qry.name contains "[domain]"` | Track queries to a specific suspicious domain |
| `http.request.method == "POST"` | Highlight form submissions (potential credential exposure) |

## 4. Findings

### 4.1 Unencrypted HTTP Traffic

- Observed [N] HTTP sessions transmitting data in cleartext.
- Using "Follow TCP Stream," it was possible to view [request headers / form data / cookies] in plaintext, meaning this data would be visible to anyone able to intercept traffic on the same network segment (e.g., via ARP spoofing on a shared LAN).
- **Risk:** Credentials, session tokens, or personal data sent over HTTP (rather than HTTPS) can be captured by a passive or active on-path attacker.
- **OSI Layer:** Application Layer (Layer 7) — the protocol itself defines the lack of encryption.

### 4.2 Anomalous DNS Activity

- Identified [N] DNS queries to domains with characteristics consistent with anomalous behavior, such as:
  - High-frequency repeated queries to the same domain in a short window
  - Queries to non-standard or randomly-generated-looking domain names
  - DNS responses with unusually short TTLs or mismatched record types
- **Risk:** This pattern is consistent with behaviors seen in malware command-and-control (C2) beaconing or DNS tunneling, where DNS is abused as a covert communication channel.
- **OSI Layer:** DNS operates at the Application Layer (Layer 7), riding over UDP/TCP at the Transport Layer (Layer 4).

### 4.3 Protocol Layer Mapping Summary

| Layer (OSI) | Example Traffic Observed | Relevance |
|---|---|---|
| Layer 7 – Application | HTTP requests, DNS queries | Where cleartext data and suspicious domains are visible |
| Layer 4 – Transport | TCP handshakes (SYN/ACK), port numbers | Confirms which service (port 80 = HTTP) is in use |
| Layer 3 – Network | Source/destination IP addresses | Identifies communicating hosts |
| Layer 2 – Data Link | MAC addresses (local segment only) | Confirms local vs. routed traffic |

## 5. Recommendations

1. **Enforce HTTPS/TLS** for all web traffic; disable fallback to HTTP where possible.
2. **Monitor DNS traffic** for anomalies using DNS logging/analytics tools, and consider deploying DNS filtering (e.g., blocking known-bad domains).
3. **Adopt encrypted DNS** (DNS-over-HTTPS or DNS-over-TLS) to prevent on-path observation of lookups.
4. **Segment networks** to limit the blast radius of a compromised host performing DNS tunneling or beaconing.
5. **Baseline normal DNS/HTTP behavior** for the network so anomalies are easier to spot going forward.

## 6. Conclusion

This analysis demonstrated how packet-level inspection with Wireshark, combined with an understanding of the OSI and TCP/IP models, can surface real security gaps — specifically plaintext data exposure over HTTP and suspicious DNS patterns that may indicate compromise. These are foundational techniques used in network security monitoring and SOC-analyst-level traffic triage.

---

*Note: All traffic analyzed was captured in a controlled/lab environment. No real user credentials or third-party production data are included in this report or its accompanying screenshots.*
