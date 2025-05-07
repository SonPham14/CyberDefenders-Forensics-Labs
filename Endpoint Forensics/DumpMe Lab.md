## Scenario

A SOC analyst took a memory dump from a machine infected with a meterpreter malware. As a Digital Forensicators, your job is to analyze the dump, extract the available indicators of compromise (IOCs) and answer the provided questions.

## Tool used

- Volatility2


## MITRE ATT&CK and MITRE D3FEND

### MITRE ATT&CK


### MITRE D3FEND


## Question

### Q1. What is the SHA1 hash of Triage-Memory.mem (memory dump)?

Using sha1sum or any HASH calculating tool.

**Answer: C95E8CC8C946F95A109EA8E47A6800DE10A27ABD**

### Q2. What volatility profile is the most appropriate for this machine? (ex: Win10x86_14393)

Using the `imageinfo` plugin in Volatility2 to determine the appropriate profile.

![{18F8C6A1-3100-43CB-B5B7-457553C2921F}](https://github.com/user-attachments/assets/9fe1a390-88e8-4edc-9a2d-c9624100c250)

**Answer: Win7SP1x64**

### Q3. What was the process ID of notepad.exe?

Using the `pslist` plugin in Volatility2 to list all processes and their IDs.

![{9C0382A1-4EEE-424F-B221-653AC30042BE}](https://github.com/user-attachments/assets/5eaea51b-c5b3-453a-ae9f-aea6f0b7808f)

**Answer: 3032**

### Q4. Name the child process of wscript.exe.

Using `pstree` plugin in Volatility2 to visualize the parent-child relationships between processes.

![image](https://github.com/user-attachments/assets/a6d2e2b1-8ce6-43a7-abb9-da45046e3561)

**Answer: UWkpjFjDzM.exe**

### Q5. What was the IP address of the machine at the time the RAM dump was created?

Using the `netscan` plugin in Volatility2 to enumerate the active network connections, including the machine’s IP address.

![{831633A6-79F4-4953-8327-87944DD3E3A3}](https://github.com/user-attachments/assets/0cab04f1-ad47-489b-99c7-fe0fd8b37afd)

The machine’s IP address is under the Local Address column.

**Answer: 10.0.0.101**

### Q6. Based on the answer regarding the infected PID, can you determine the IP of the attacker?

In the pstree result, the process with PID 3496 named UwKpjFjDzM.exe is suspicious due to its unusual name. Its child process is `cmd.exe`, and its parent process is `wscript.exe` — the Windows Script Host (WSH) executable, is a crucial component of the Windows operating system that allows the execution of scripts written in various scripting languages, most commonly VBScript (.vbs) and JScript (.js). Cross-referencing with the netscan table, the corresponding PID shows that the victim machine is establishing a connection to another system with IP and port 10.0.0.106:4444 — port 4444 is commonly used by the Metasploit framework for exploitation, possibly a reverse_tcp shell attack.

**Answer: 10.0.0.106**

### Q7. How many processes are associated with VCRUNTIME140.dll?

Using `dlllist` plugin in Volatility2 and grep `VCRUNTIME140.dll` to know how many processes there are.

I do not know why there are only 1 process when I use volatility2 (also volatility3).

![{67FFEA95-E366-4AAD-A0B5-F98F30BCC6BC}](https://github.com/user-attachments/assets/fb0db771-8a62-412b-bb52-013858cfd30b)


**Answer: 5**

### Q8. After dumping the infected process, what is its md5 hash?

Using `procdump` plugin in Volatility2 to dump VCRUNTIME140.dll.
**Answer: 690ea20bc3bdfb328e23005d9a80c290**

### Q9. What is the LM hash of Bob's account?

Using `hashdump` plugin in Volatility2 to retrieve LM password hashes on Windows. The LM (LAN Manager) hash was one of the first password hashing algorithms to be used by Windows operating systems, and the only version to be supported up until the advent of NTLM used in Windows 2000, XP, Vista, and 7.

![{59CCD6AE-EF0B-43E9-A683-1424CF8731F1}](https://github.com/user-attachments/assets/7a97047a-bb6f-4f34-9e28-1cadd1e9c5a5)

LM hash format: `<User_name>:<User_ID>:<LM_hash>:<NTLM hash>:<Comment>:<Home Dir>:`

The string "aad3b435b51404eeaad3b435b51404ee" is the LM hash for an empty password, and "31d6cfe0d16ae931b73c59d7e0c089c0" is the NTLM hash for an empty password as well.

**Answer: aad3b435b51404eeaad3b435b51404ee**

### Q10. What memory protection constants does the VAD node at 0xfffffa800577ba10 have?

**Answer: PAGE_READONLY**

### Q11. What memory protection did the VAD starting at 0x00000000033c0000 and ending at 0x00000000033dffff have?

**Answer: PAGE_NOACCESS**

### Q12. There was a VBS script that ran on the machine. What is the name of the script? (submit without file extension)

**Answer: vhjReUDEuumrX**

### Q13. An application was run at 2019-03-07 23:06:58 UTC. What is the name of the program? (Include extension)

**Answer: Skype.exe**

### Q14. What was written in notepad.exe at the time when the memory dump was captured?

**Answer: flag<REDBULL_IS_LIFE>**

### Q15. What is the short name of the file at file record 59045?

**Answer: EMPLOY~1.XLS**

### Q16. This box was exploited and is running meterpreter. What was the infected PID?

**Answer: 3496**
