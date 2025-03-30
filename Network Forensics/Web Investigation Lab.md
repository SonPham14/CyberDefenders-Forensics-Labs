## Scenario

You are a cybersecurity analyst working in the Security Operations Center (SOC) of BookWorld, an expansive online bookstore renowned for its vast selection of literature. BookWorld prides itself on providing a seamless and secure shopping experience for book enthusiasts around the globe. Recently, you've been tasked with reinforcing the company's cybersecurity posture, monitoring network traffic, and ensuring that the digital environment remains safe from threats.
Late one evening, an automated alert is triggered by an unusual spike in database queries and server resource usage, indicating potential malicious activity. This anomaly raises concerns about the integrity of BookWorld's customer data and internal systems, prompting an immediate and thorough investigation.
As the lead analyst in this case, you are required to analyze the network traffic to uncover the nature of the suspicious activity. Your objectives include identifying the attack vector, assessing the scope of any potential data breach, and determining if the attacker gained further access to BookWorld's internal systems.

## Tools used

- Wireshark
- NetworkMiner

## Questions

### Q1. By knowing the attacker's IP, we can analyze all logs and actions related to that IP and determine the extent of the attack, the duration of the attack, and the techniques used. Can you provide the attacker's IP?

Filtering the HTTP protocol, it is easy to recognize that this is an SQLi attack and file/directory scanning (using gobuster).

![{B8F758A1-CEC2-4C4B-9DCA-9CCC28A8214B}](https://github.com/user-attachments/assets/d9209497-90d6-454f-8534-0a5d0ee8d757)

<img src=https://github.com/user-attachments/assets/7b047b52-8388-4c79-a8ab-7458a9e7eb58 width=100%>
<p></p>

And some malicious credentials

![{B650928F-FECB-474D-B9E4-A127CEF89C8E}](https://github.com/user-attachments/assets/e8ea804c-d53e-4559-98c0-e0f7702cdc20)

**Answer: 111.224.250.131**

### Q2. If the geographical origin of an IP address is known to be from a region that has no business or expected traffic with our network, this can be an indicator of a targeted attack. Can you determine the origin city of the attacker?

Use online geolocation tools, such as `https://whatismyipaddress.com`, to determine the location of the identified IP address.

**Answer: Shijiazhuang**

### Q3. Identifying the exploited script allows security teams to understand exactly which vulnerability was used in the attack. This knowledge is critical for finding the appropriate patch or workaround to close the security gap and prevent future exploitation. Can you provide the vulnerable PHP script name?

According to images in question 1.

**Answer: search.php**

### Q4. Establishing the timeline of an attack, starting from the initial exploitation attempt, What's the complete request URI of the first SQLi attempt by the attacker?

Filtering with the attacker's IP to identify the first SQLi attempt by the attacker.

Pay attention to packet number 347 and 349, where the request URI is `/search.php?search=book%27`. The `%27` character, when URL-decoded, becomes an apostrophe (`'`). This is a commonly used payload to test for SQL Injection (SQLi) vulnerabilities. Then server responds with a **500 Internal Server Error**, it indicates that the web server may be vulnerable to SQLi.

![{D915E788-C4D0-4A5A-8B6E-C5E2A06437F6}](https://github.com/user-attachments/assets/74b083c3-7418-4274-a0dc-a4619add6955)

So, the complete request URI of the first SQLi attempt by the attacker is `/search.php?search=book%20and%201=1;%20--%20-`

**Answer: /search.php?search=book%20and%201=1;%20--%20-**

### Q5. Can you provide the complete request URI that was used to read the web server's available databases?

- First, "read the web server's available databases" --> that means the server responsed to attacker successfully with status code 200.

- Second, in SQL Injection (SQLi) attacks, attackers often exploit information_schema to gain access to the database structure. (Note: most database types (except Oracle) have a set of views called the information schema. This provides information about the database.

Under the Parameters tab, filter parameters containing `information_schema`, then copy those parameter values that also include `search.php`.

![{04534334-56AC-4782-8438-F5E0AC8C80A3}](https://github.com/user-attachments/assets/9f07c6fb-c350-4991-803b-6ab76b771224)



**Answer: /search.php?search=book%27%20UNION%20ALL%20SELECT%20NULL%2CCONCAT%280x7178766271%2CJSON_ARRAYAGG%28CONCAT_WS%280x7a76676a636b%2Cschema_name%29%29%2C0x7176706a71%29%20FROM%20INFORMATION_SCHEMA.SCHEMATA--%20-**

### Q6. Assessing the impact of the breach and data access is crucial, including the potential harm to the organization's reputation. What's the table name containing the website users data?


**Answer: customers**

### Q7. The website directories hidden from the public could serve as an unauthorized access point or contain sensitive functionalities not intended for public access. Can you provide the name of the directory discovered by the attacker?


**Answer: /admin/**

### Q8. Knowing which credentials were used allows us to determine the extent of account compromise. What are the credentials used by the attacker for logging in?


**Answer: admin:admin123!**

### Q9. We need to determine if the attacker gained further access or control of our web server. What's the name of the malicious script uploaded by the attacker?


**Answer: NVri2vhp.php**


## References

- [1] SQL Injection: https://portswigger.net/web-security/sql-injection
- [2] Python Scapy: https://scapy.readthedocs.io/en/latest/api/scapy.layers.http.html
- [3] 
