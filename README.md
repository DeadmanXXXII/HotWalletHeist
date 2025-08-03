<img src="./assets/banner.png" style="max-width: 100%;" align=left />

---
# HotWalletHeist

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

Here's a detailed walkthrough to help answer the questions from the PCAP file and artifacts you've provided. Here's a structured approach for each question, with insights into what to look for in the PCAP traffic and what tools to use.


---

Walkthrough for Each Question:


---

1. Which user account was compromised first?

Goal: Identify which user account was compromised first based on the network traffic.

How to Analyze:

Open the PCAP in Wireshark.

Filter RDP traffic using rdp or look for SMB authentication requests.

Check for user credentials passed over the network.

The first RDP or SMB session with a compromised user account should give you the answer.




---

2. What is the IP address of the host that initiated the RDP session to the wallet server?

Goal: Find the IP address of the system that initiated the RDP connection.

How to Analyze:

Open the PCAP in Wireshark.

Use the filter: tcp.port == 3389 (RDP's default port).

Look for the initial RDP handshake and examine the source IP.




---

3. What is the name of the exfiltrated file?

Goal: Identify the name of the exfiltrated file from the SMB traffic.

How to Analyze:

Open the PCAP in Wireshark or NetworkMiner.

Search for SMB file transfer traffic using the smb filter.

Find commands like SMB COM_TRANSACT or SMB COM_READ_ANDX, which indicate file transfers.

Look for the file path or filename in the SMB negotiation/transfer details.




---

4. What was the size of the reassembled exfiltrated file?

Goal: Find the total size of the file once reassembled.

How to Analyze:

The SMB transfer might have been split into chunks.

In Wireshark, look for multiple packets related to the same file transfer.

Reassemble the file chunks manually (or use NetworkMiner to help extract full files from the PCAP).

Use the file size from the reassembled file.




---

5. What is the file hash of the reassembled exfiltrated file?

Goal: Get the hash (e.g., SHA256) of the reassembled exfiltrated file.

How to Analyze:

After reassembling the file, calculate its hash using a tool like sha256sum or md5sum.

This hash will be your answer.




---

6. Which attacker tool was used for file exfiltration?

Goal: Identify which tool the attacker used to perform data exfiltration.

How to Analyze:

Examine the SMB traffic and other anomalous network behavior.

Tools like SMBExec, RClone, or Netcat are commonly used for exfiltration.

Look for unusual tool traffic or signature patterns in the PCAP.




---

7. What method did the attacker use to avoid detection by network monitoring?

Goal: Identify the stealth techniques used by the attacker.

How to Analyze:

Look for encrypted SMB traffic or split-file transfers (split up to avoid detection).

Check for tunneling protocols (e.g., SSH, VPN, Tor).

Look for long gaps between packets or use of uncommon ports.




---

8. What is the cryptocurrency wallet public address targeted by the attacker?

Goal: Find the wallet address that the attacker was targeting.

How to Analyze:

Search the PCAP for cryptocurrency wallet addresses. These might appear as plain text or in HTTP requests if the attacker tried to access the wallet.

Look for data exfiltration related to wallet files.




---

9. How did the attacker maintain persistence on the compromised host?

Goal: Identify how the attacker kept access to the compromised host.

How to Analyze:

Look for signs of backdoor installation via RDP or SMB.

Check for suspicious processes on the compromised machine (possibly indicated by SMB commands).

Examine registry modifications, task scheduler jobs, or services in the PCAP.




---

10. What CVE or vulnerability was exploited during the attack?

Goal: Identify the CVE used to gain initial access.

How to Analyze:

Look for known exploit patterns (e.g., RDP vulnerabilities like CVE-2019-0708 or SMB vulnerabilities).

Check for signs of exploit attempts or code execution in the PCAP.




---

Final Steps:

Once you've gathered the data from Wireshark, Zeek, NetworkMiner, and any other tools, the next steps are:

1. Reassemble any files that were split during exfiltration.


This should give you everything you need to solve the case step-by-step. Once you’ve completed your investigation, you can finalize your answers.


<img src="./assets/htb.png" style="max-width: 100%;" align=center />

---
