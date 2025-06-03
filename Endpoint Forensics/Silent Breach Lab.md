## Scenario

The IMF is hit by a cyber attack compromising sensitive data. Luther sends Ethan to retrieve crucial information from a compromised server. Despite warnings, Ethan downloads the intel, which later becomes unreadable. To recover it, he creates a forensic image and asks Benji for help in decoding the files.

Resources:
[Windows Mail Artifacts: Microsoft HxStore.hxd (email) Research](https://boncaldoforensics.wordpress.com/2018/12/09/microsoft-hxstore-hxd-email-research/)

## Tools used

- FTK Imager
- CyberChef

## Question

### Q1. What is the MD5 hash of the potentially malicious EXE file the user downloaded?

Using FTK Imager, then go to Downloads directory, we can see an exe file named "IMF-Info.pdf.exe". This file shows clear malicious because its name is intentionally made to look like a regular PDF file in order to deceive users.

**Answer: 336A7CF476EBC7548C93507339196ABB**


### Q2. What is the URL from which the file was downloaded?

If we click to that mentioned file in Evidence tree, we can see a Zone.Identifier in File List. So, what is Zone.Identifier?

Zone.Identifier is a small Alternate Data Stream (ADS) that the Windows system automatically adds to files downloaded from the Internet or from untrusted sources. It contains information about the Security Zone of the file's origin, helping Windows determine the risk level and display security warnings when open the file. [1]

You can 

![{78839CC9-C4A5-482A-BE13-406119E0312C}](https://github.com/user-attachments/assets/01074da4-d7c1-4a06-8bf8-c50e0a911292)


**Answer: http://192.168.16.128:8000/IMF-Info.pdf.exe**


### Q3. What application did the user use to download this file?


**Answer: Microsoft Edge**


### Q4. By examining Windows Mail artifacts, we found an email address mentioning three IP addresses of servers that are at risk or compromised. What are the IP addresses?


**Answer: 145.67.29.88, 212.33.10.112, 192.168.16.128**


### Q5. By examining the malicious executable, we found that it uses an obfuscated PowerShell script to decrypt specific files. What predefined password does the script use for encryption?


**Answer: Imf!nfo#2025Sec$**


### Q6. After identifying how the script works, decrypt the files and submit the secret string.


**Answer: CyberDefenders{N3v3r_eX3cuTe_F!l3$_dOwnL0ded_fr0m_M@lic10u5_$erV3r}**

## References

- [1] Russinovich, Mark E.; Solomon, David A.; Ionescu, Alex (2009). "File Systems". Windows Internals (5th ed.). Microsoft Press. p. 836. ISBN 978-0-7356-2530-3.
- 
