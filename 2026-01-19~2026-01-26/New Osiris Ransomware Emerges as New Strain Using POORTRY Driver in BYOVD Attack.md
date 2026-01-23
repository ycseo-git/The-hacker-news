> Educational purpose only, 23, Jan, 2026

# New Osiris Ransomware Emerges as New Strain Using POORTRY Driver in BYOVD Attack

## Summary
Cybersecurity researchers have disclosed details of a new ransomware family called Osiris that targeted a major food service franchisee operator in Southeast Asia in November 2025.

The attack leveraged a malicious driver called POORTRY as part of a known technique referred to as bring your own vulnerable driver(BYOVD) to disarm security software.

It's worth noting that Osiris is assessed to be a brand-new ransomware strain, sharing no similarities with another variant of the same name that emerged in December 2016 as an iteration of the Locky ransomware. It is currently not known who the developers of the locker are, or if it is advertised as a ransomware-as-a-service(RaaS).

However, the Broadcom-owned cybersecurity division said it identified cluse that suggest the threat actors who deplyed the ransomware may have been previously associated with INC ransomware (a.k.a Warble).

"The exfiltration of data by attackers to Wasabi buckets, and the use of a version of Mimikatz that was previously used, with the same filename (kaz.exe), by attackers deploying the INC ransomware, point to potential links between this attack and some attacks involving INC.", the company said.

Described as an "effective encryption payload" that's likely wielded by experienced attackers, Ositis makes use of a hybrid encryption scheme and a unique encryption key for each file. It is also flexible in that it can stop services, specify which folders and extensions need to be encrypted, terminate processes, and drop a ransom note.

By default, it is designed to kill a long list of processes and services related to Microsoft Office, Exchange, Mozilla Firefox, Wordpad, Notepad, Volume Shadow Copy, and Veeam, among others.

First Signs of malicious activity on the target's network involved the exfiltration of sensitive data using Rclone to a Wasabi cloud storage bucker prior to the ransomware deployment. Also utilized in the attack were a number of dual-ise tools like Netscan, Netexec, and MeshAgent, as well as a custom version of the Rustdesk remote desktop software.

"KillAV, which is a tool used to deploy vulnerable drivers for terminating security processes, was also deployed on the target's network", the team noted. "RDP was also enabled on the network, likely to provide the attackers with remote access."

## Note
### BYOVD (Bring Your Own Vulnerable Driver)
BYOVD is an exploitation technique where attackers install a legitimate, digitally signed driver containing known vulnerabilities onto a target system. Since the OS trusts the driver's signature, it is allowed to run with kernel-level privileges. Attackers then exploit the driver's flaws to execute malicious code in the kernel, bypassing standard security restrictions.

### POORTRY
POORTRY is a bespoke malicious driver designed to disable endpoint security software. In the context of the Osiris attack, it is deployed via the BYOVD technique to operate within the kernel. From this high-privilege position, it forcefully terminates antivirus and EDR processes, ensuring the subsequent ransomware payload can encrypt data without being blocked.

## Tag
\# Ransomware \# New \# Emerges \# Osiris \# Variant \# Strain

## Reference
https://thehackernews.com/2026/01/new-osiris-ransomware-emerges-as-new.html