

# **Threat Hunter's Network Visibility Toolkit (NVT)**

*A defender-focused network analytics tool for detecting beaconing, high-entropy payloads, rare-port activity, and other C2-like behavior.*

---

## Overview

The **Network Visibility Toolkit (NVT)** provides automated visibility into live network flows using threat-hunting heuristics inspired by real SOC workflows. Instead of relying on PCAP files, NVT captures traffic directly, builds bi-directional flows, and evaluates them for indicators of command-and-control (C2) activity, exfiltration, or suspicious beacon patterns.

This toolkit is designed for cybersecurity students, threat hunters, and analysts who want practical, behavioral-based detection capability without needing an entire home lab.

---

##  Key Features

* **Live traffic capture** (no PCAP required)
* **Bi-directional flow building** with timestamps, byte counts, and packet stats
* **Beaconing detection** using timing intervals and jitter
* **Payload entropy analysis** to spot encryption/packing
* **Rare port identification** for unusual service behavior
* **Suspicion scoring engine** with tunable thresholds
* **Client/server role inference**
* **Exports to JSON & SIEM-friendly logs**
* **Graceful fallback if Scapy is not installed**

---

##  What This Shows (Portfolio Value)

This project demonstrates:

* Understanding of **threat-hunting analytics**
* Knowledge of **network flow behavior**
* Ability to detect **early-stage C2 and exfiltration patterns**
* Clean software structure using data classes and modular design
* Practical defender-oriented engineering (logging, config, output formats)

Perfect for SOC, threat-hunting, cybersecurity analyst, and detection engineering roles.

---

## Architecture

NVT is built around two core structures:

### **`PacketSample`**

Holds timestamp, size, and entropy for each observed packet.

### **`FlowStats`**

Represents a normalized bi-directional flow containing:

* packet list
* duration
* average/variance of inter-packet intervals
* average entropy
* inferred client/server roles

A configurable **`DetectionConfig`** controls the aggressiveness of beacon detection, entropy thresholds, jitter requirements, and minimum flow size.

---

##  Detection Heuristics

NVT uses practical, signal-based heuristics:

* **Low jitter + consistent timing = beaconing**
* **High entropy = encrypted/packed payloads**
* **Uncommon ports = suspicious when combined with other signals**
* **Small but long-lived flows = possible C2/exfil**
* **Score-based system** to determine when to flag a flow as suspicious

This mirrors real-world detection engineering.

---

##  Output Files

NVT generates three outputs:

| File                 | Description                             |
| -------------------- | --------------------------------------- |
| `nvt_findings.json`  | Suspicious flows only (structured JSON) |
| `nvt_siem.log`       | Key=value SIEM-friendly output          |
| `nvt_all_flows.json` | Summary of all observed flows           |

---

##  Usage

```bash
python nvt.py
```

Optional configuration changes can be made at the top of the script:

```python
CAPTURE_DURATION = 30
ENABLE_ENTROPY = True
DETECTION_CFG.high_entropy_threshold = 7.0
```

---

##  Requirements

* Python 3.10+
* Scapy (optional but recommended)

## Disclaimer

This tool is intended **for educational and defensive security purposes only**.
Capture traffic only on networks you own or are authorized to analyze.

---

##  Future Enhancements

* CLI arguments for configuration
* Visual dashboards for flow analysis
* Machine-learning assisted clustering
* Integration with ELK / Splunk / OpenSearch
* DNS, TLS, and HTTP metadata extraction
