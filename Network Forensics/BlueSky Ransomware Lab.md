## Scenario

A high-profile corporation that manages critical data and services across diverse industries has reported a significant security incident. Recently, their network has been impacted by a suspected ransomware attack. Key files have been encrypted, causing disruptions and raising concerns about potential data compromise. Early signs point to the involvement of a sophisticated threat actor. Your task is to analyze the evidence provided to uncover the attacker’s methods, assess the extent of the breach, and aid in containing the threat to restore the network’s integrity.

## Tools used
- Wireshark
- Tshark
- NetworkMiner
- CyberChef


## Question

First, we should know how many endpoints were conversation. There are 2 endpoints, `87.96.21.81` and `87.96.21.84`, were conversation. Anothers are gateway and broadcast IP.

![{04CC375E-7949-488F-A582-32553D7D689A}](https://github.com/user-attachments/assets/c58bbdcb-3e16-445c-8b23-125b018793cb)

Q1. Knowing the source IP of the attack allows security teams to respond to potential threats quickly. Can you identify the source IP responsible for potential port scanning activity?

Based on the information above,  we need to identify the source IP responsible for potential port scanning activity.

In Session tab of NetworkMiner, we can see 

![{0861A75A-3CA2-43F0-A708-696B2739D10A}](https://github.com/user-attachments/assets/75d49f1d-7a12-4dd4-b5ff-9b5cd3832a23)

Just by looking, it is clear that 87.96.21.84 is the IP performing the port scanning.

**Answer: 87.96.21.84**

Q2. During the investigation, it's essential to determine the account targeted by the attacker. Can you identify the targeted account username?

In the Credentials tab of NetworkMiner, there is only one account targeted by the attacker.

<img src=https://github.com/user-attachments/assets/fd1bc7ce-fbc8-4828-b211-256cd58bbc7c width=100%>
<p></p>

Filtering the TDS protocol in Wireshark, there are two login sessions from the attacker, both using the account `sa:cyb3rd3f3nd3r$`.

![{D7111D07-2747-4542-AB46-E80746D2849A}](https://github.com/user-attachments/assets/a008e7fb-9368-48c7-ac0b-6c5140283114)

<img src=https://github.com/user-attachments/assets/8dae2362-8beb-41ba-bb3e-f9c21daa4b92 width=100%>
<p></p>

**Answer: sa**

Q3. We need to determine if the attacker succeeded in gaining access. Can you provide the correct password discovered by the attacker?

Check Q2.

**Answer: cyb3rd3f3nd3r$**

Q4. Attackers often change some settings to facilitate lateral movement within a network. What setting did the attacker enable to control the target host further and execute further commands?

Attacker enabled xp_cmdshell in Microsoft SQL Server, allowing them to execute system commands directly from SQL queries. This technique is commonly used when exploiting SQL Server via TDS protocol.

![{D81E3F30-B8A5-45B3-A306-FA1C831C0BD9}](https://github.com/user-attachments/assets/acc0aebb-bc6a-49b4-aeb2-eef49fcbf0bf)


**Answer: xp_cmdshell**

Q5. Process injection is often used by attackers to escalate privileges within a system. What process did the attacker inject the C2 into to gain administrative privileges?




Q6. Following privilege escalation, the attacker attempted to download a file. Can you identify the URL of this file downloaded?



Q7. Understanding which group Security Identifier (SID) the malicious script checks to verify the current user's privileges can provide insights into the attacker's intentions. Can you provide the specific Group SID that is being checked?




Q8. Windows Defender plays a critical role in defending against cyber threats. If an attacker disables it, the system becomes more vulnerable to further attacks. What are the registry keys used by the attacker to disable Windows Defender functionalities? Provide them in the same order found.




Q9. Can you determine the URL of the second file downloaded by the attacker?





Q10. Identifying malicious tasks and understanding how they were used for persistence helps in fortifying defenses against future attacks. What's the full name of the task created by the attacker to maintain persistence?




Q11. Based on your analysis of the second malicious file, What is the MITRE ID of the main tactic the second file tries to accomplish?



Q12. What's the invoked PowerShell script used by the attacker for dumping credentials?



Q13. Understanding which credentials have been compromised is essential for assessing the extent of the data breach. What's the name of the saved text file containing the dumped credentials?




Q14. Knowing the hosts targeted during the attacker's reconnaissance phase, the security team can prioritize their remediation efforts on these specific hosts. What's the name of the text file containing the discovered hosts?




Q15. After hash dumping, the attacker attempted to deploy ransomware on the compromised host, spreading it to the rest of the network through previous lateral movement activities using SMB. You’re provided with the ransomware sample for further analysis. By performing behavioral analysis, what’s the name of the ransom note file?




Q16. In some cases, decryption tools are available for specific ransomware families. Identifying the family name can lead to a potential decryption solution. What's the name of this ransomware family?



## References
- [1] xp_cmdshell: https://learn.microsoft.com/vi-vn/sql/database-engine/configure-windows/xp-cmdshell-server-configuration-option?view=sql-server-2017
