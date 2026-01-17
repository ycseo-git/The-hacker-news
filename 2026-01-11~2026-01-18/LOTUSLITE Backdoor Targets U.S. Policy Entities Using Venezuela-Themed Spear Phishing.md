> Educational purpose only, 17, Jan, 2026

# LOTUSLITE Backdoor Targets U.S. Policy Entities Using Venezuela-Themed Spear Phishing

## Summary
Security experts have disclosed details of a new campaign that has targeted U.S. government and policy entities using **politically themed** lures to **deliver a backdoor** known as LOTUSLITE.

The targeted malware campaign **leverages decoys** related to the recent geopolitical developments between the U.S. and Venezuela to distribute a ZIP archive ("US now deciding what's next for Venezuela.zip") containing a malicious DLL that's launched using DLL side-loading techniques.

The activity has been **attributed with moderate confidence** to a Chinese state-sponsored group known as Mustang Panda(a.k.a. Earth Pret, HoneyMyte, and Twill Typhoon), citing tactical and infrastructure patterns. **It's worth that** the threat actor is known for extensively relying on DLL side-loading to launch its backdoors, including TONESHELL.

The backdoor ("kugou.dll") **employed in the attack**, LOTUSLITE, is a **bespoke(Tailor-made)** C++ implant that's designed to communicate with a hard-coded command-and-control (C2) server using Windows WinHTTP APIs to enable beaconing activity, remote tasking using "cmd.exe", and data exfiltration.

LOTUSLITE is also capable of establishing persistence by making Windows Registry modifications to ensure that it's automatically executed each time the user logs to the system.

## Note
### DLL and DLL Sideloading
DLL is Windows' shared library format, utilizing here as a DLL Side-loading attack vector. By placing a malicious DLL in a high-priority search path, the attacker hijacks the execution flow of a legitimate executable to achieve in-memory execution and process hollowing.

### Operational Code
These are Command IDs that define the communication protocol between the C2 and the implant. Each 1-byte hexadecimal value determines the control flow within a switch-case structure, mapping to specific routines (e.g., exfiltration, shell spawning). This is a form of protocol obfuscation designed to minimize payload size and hinder traffic analysis.

## Tag
\# Malware \#APT \#Mustang-Panda \#US \#Venezuela \#Phishing

## Reference
https://thehackernews.com/2026/01/lotuslite-backdoor-targets-us-policy.html