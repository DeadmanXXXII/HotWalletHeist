<img src="./assets/banner.png" style="max-width: 100%;" align=left />

# HotWalletHeist
Sherlock for htb

#### Date: 03/08/2025

#### Prepared by: DeadmanXXXII and AirFryerRamsey

#### Machine Author(s): DeadmanXXXII

#### Difficulty: Hard

---

###### 1. Scenario

CoinStash Exchange, a mid-sized cryptocurrency exchange, fell victim to a sophisticated attack. The attacker, known as *DeadmanXXXII*, successfully gained access to the internal network and exfiltrated high-value wallet data by leveraging RDP to gain access to a Windows workstation. Lateral movement was performed to a Linux-based wallet server, where data was siphoned via SMB-based file transfer. Stealthy exfiltration methods, such as split-file archiving and evasion of network monitoring tools, were used to avoid detection.

###### 2. Description

Artifacts Provided:

- bitvalutis_intrusion_capture.pcap - *<insert file hash here>*
- RAR-SFX malicious tool (password protected) - *<insert file hash here>*

Initial Analysis

The provided pcap file was analyzed with Wireshark, Zeek, and NetworkMiner. The focus was placed on identifying suspicious RDP connections and SMB traffic. Suspicious traffic was observed coming from a finance workstation that appeared to initiate an RDP connection to the backend wallet server.

Analysis Sub-Section

The analysis was focused on SMB traffic, specifically looking for large file transfers that may indicate exfiltration. The attacker utilized split-file archives, which required reassembly to recover the full exfiltrated data.


---

###### Questions:
```yml
questions:
- number: 1
  type: free
  title: Which user account was compromised first?
  flag: compromised_user
  answer_case_sensitive: false
  placeholder: Enter the username of the first compromised user
  requires: null
- number: 2
  type: free
  title: What is the IP address of the host that initiated the RDP session to the wallet server?
  flag: rdp_ip
  answer_case_sensitive: false
  placeholder: Enter the RDP source IP
  requires: null
- number: 3
  type: free
  title: What is the name of the exfiltrated file?
  flag: exfil_file_name
  answer_case_sensitive: false
  placeholder: Enter the name of the exfiltrated file
  requires: null
- number: 4
  type: free
  title: What was the size of the reassembled exfiltrated file?
  flag: exfil_file_size
  answer_case_sensitive: false
  placeholder: Enter the size of the reassembled file in bytes
  requires: null
- number: 5
  type: free
  title: What is the file hash of the reassembled exfiltrated file?
  flag: exfil_file_hash
  answer_case_sensitive: false
  placeholder: Enter the file hash of the exfiltrated file
  requires: null
- number: 6
  type: free
  title: Which attacker tool was used for file exfiltration?
  flag: exfil_tool
  answer_case_sensitive: false
  placeholder: Enter the name of the exfiltration tool
  requires: null
- number: 7
  type: free
  title: What method did the attacker use to avoid detection by network monitoring?
  flag: evasion_method
  answer_case_sensitive: false
  placeholder: Describe the evasion method used by the attacker
  requires: null
- number: 8
  type: free
  title: What is the cryptocurrency wallet public address targeted by the attacker?
  flag: target_wallet
  answer_case_sensitive: false
  placeholder: Enter the wallet address
  requires: null
- number: 9
  type: free
  title: How did the attacker maintain persistence on the compromised host?
  flag: persistence_method
  answer_case_sensitive: false
  placeholder: Describe the persistence mechanism used
  requires: null
- number: 10
  type: free
  title: What CVE or vulnerability was exploited during the attack?
  flag: exploited_cve
  answer_case_sensitive: false
  placeholder: Enter the CVE ID
  requires: null
```
---


