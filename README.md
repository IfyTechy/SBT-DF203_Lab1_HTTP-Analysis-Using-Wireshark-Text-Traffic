# SBT-DF203 Lab 1: HTTP Traffic Analysis Using Wireshark

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Platform](https://img.shields.io/badge/OS-Kali%20Linux-dragon.svg)](https://www.kali.org/)
[![Tool](https://img.shields.io/badge/Tool-Wireshark%20%7C%20tshark-gui.svg)](https://www.wireshark.org/)

## 📌 Overview
This repository contains the formal digital forensics investigation and network packet capture analysis for **SBT-DF203: Basic Networking Skills for Digital Forensics (Lab 1)**. 

The primary objective of this investigation is to capture, inspect, and analyze unencrypted plaintext HTTP traffic on a Linux workstation, verify evidence chain-of-custody using cryptographic hashing, reconstruct application-layer payloads, and analyze socket interaction states.

---

## 👤 Investigator Information
* **Lead Examiner:** Nebeuwa Ifeanyichukwu Raphael
* **Registration / ID No.:** `202520850LE`
* **Course Code:** SBT-DF203
* **Primary Target System:** Kali Linux (`kali@kali`)
* **Target Web Server:** Apache/2.4.68 (Debian) on TCP Port 80

---

## 🔑 Key Forensic Objectives & Findings

1. **Evidence Acquisition & Isolation:**
   * Established an isolated forensic workspace structure under `~/SBT-DF203-Lab1/`.
   * Recorded live TCP Port 80 traffic over the virtual loopback interface (`lo`) to produce `basic.pcapng`.

2. **Cryptographic Integrity Verification:**
   * Generated SHA-256 digests across primary evidence (`evidence/`) and working copies (`working/`) to guarantee zero bit-level alteration.
   * **SHA-256 Digest:** `48996916527842abf0114489c15dc1448c748af1b4c6a1bc9c3520213cbde502`

3. **Session Reconstruction (TCP Stream 0):**
   * Reconstructed a complete 10-packet TCP session encompassing the initial three-way handshake (`SYN`, `SYN-ACK`, `ACK`).
   * Extracted plaintext HTTP request (`GET /basic.html`) and server response (`HTTP/1.1 200 OK`).
   * Recovered HTML target payload revealing examiner identification data.

4. **Encapsulation & Session Termination Analysis:**
   * Documented standard `FIN-ACK` teardown mechanics.
   * Observed loopback MAC addressing (`00:00:00:00:00:00`), confirming inter-process communication without physical network hardware overhead.

---

## 📁 Repository Structure

```text
.
├── evidence/
│   └── basic.pcapng              # Raw network packet capture file
├── working/
│   └── basic_working.pcapng      # Cryptographically verified working copy
├── exported/
│   ├── http_metadata.tsv         # Extracted HTTP header parameters
│   └── payload_basic.html        # Reconstructed HTML response payload
├── reports/
│   ├── DF203_Lab1_Report.pdf     # Official PDF Forensic Investigation Report
│   └── report.md                 # Markdown source report
├── screenshots/                  # High-resolution evidence verification captures
└── scripts/
    └── setup_lab.sh              # Automated setup and verification script
```

## 🛠️ Tools & Technologies Used

* **Wireshark / tshark:** Network packet capture, display filtering, and field extraction.
* **Apache2:** Local HTTP server environment (`127.0.0.1:80`).
* **OpenSSL / sha256sum:** Cryptographic hashing and evidence verification.
* **Microsoft Word / Google Docs:** Report formatting and formal PDF document export.

## 📄 License
This project is released under the MIT License for educational and portfolio presentation purposes.
