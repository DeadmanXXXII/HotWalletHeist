# HotWalletHeist
Sherlock for htb

#### Date: 03/08/2025

#### Prepared by: DeadmanXXXII and AirFryerRamsey

#### Machine Author(s): DeadmanXXXII

#### Difficulty: Hard

---

1. Scenario

CoinStash Exchange, a mid-sized cryptocurrency exchange, fell victim to a sophisticated attack. The attacker, known as *DeadmanXXXII*, successfully gained access to the internal network and exfiltrated high-value wallet data by leveraging RDP to gain access to a Windows workstation. Lateral movement was performed to a Linux-based wallet server, where data was siphoned via SMB-based file transfer. Stealthy exfiltration methods, such as split-file archiving and evasion of network monitoring tools, were used to avoid detection.

2. Descriptiom
Artifacts Provided

- bitvalutis_intrusion_capture.pcap - *<insert file hash here>*
- RAR-SFX malicious tool (password protected) - *<insert file hash here>*

Initial Analysis

The provided pcap file was analyzed with Wireshark, Zeek, and NetworkMiner. The focus was placed on identifying suspicious RDP connections and SMB traffic. Suspicious traffic was observed coming from a finance workstation that appeared to initiate an RDP connection to the backend wallet server.

Analysis Sub-Section

The analysis was focused on SMB traffic, specifically looking for large file transfers that may indicate exfiltration. The attacker utilized split-file archives, which required reassembly to recover the full exfiltrated data.


---
