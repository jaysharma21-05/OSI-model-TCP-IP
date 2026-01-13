# Ports, Protocols & Nmap – Hinglish Notes

## 1️⃣ PORTS KYA HAIN?

### Definition

Port ek **logical** address hai jo computer pe specific service/application ko identify karta hai.  
Har network connection me IP address + port number use hota hai data transfer ke liye.

**Analogy:** Socho IP address ek building ka address hai, aur port number individual apartment numbers hain.  
Har apartment (port) me alag service rehti hai (web server, email, etc).

### Port Range

Total 65,535 ports hote hain (0–65535), jo 3 categories me divided hain:

| Port Range   | Category           | Purpose                                      |
|-------------|--------------------|----------------------------------------------|
| 0–1023      | Well-Known Ports   | Standard services (HTTP, FTP, SSH, etc)     |
| 1024–49151  | Registered Ports   | User/Application-specific services          |
| 49152–65535 | Dynamic/Private    | Client-side temporary (ephemeral) ports     |

---

## 2️⃣ TCP vs UDP – Protocol Difference

### TCP (Transmission Control Protocol)

- **Connection-oriented:** Data send karne se pehle 3-way handshake (SYN → SYN-ACK → ACK).
- **Reliable:** Lost packets re-transmit hote hain, delivery guarantee hai.
- **Ordered:** Data sequence maintain hota hai (packets sahi order me receive honge).
- **Slow:** Overhead zyada (acknowledgments, error checking).
- **Use cases:** Web browsing (HTTP/HTTPS), Email (SMTP/POP3/IMAP), File Transfer (FTP).

### UDP (User Datagram Protocol)

- **Connectionless:** Seedha data send kar deta hai, no handshake.
- **Unreliable:** No delivery guarantee, lost packets resend nahi hote.
- **Fast:** Minimal overhead, no acknowledgments.
- **Use cases:** Streaming (video/audio), VoIP, DNS, Online Gaming.

**Interview Tip:**  
UDP speed ke liye sacrifice karta hai reliability, isliye real-time applications jahan thodi data loss acceptable hai (gaming, video call), wahan UDP use hota hai.  
TCP jahan accuracy zaroori hai (banking, email), wahan use hota hai.

---
## 3️⃣ COMMON PORTS & PROTOCOLS (Must Learn!)

### A. File Transfer Protocols

#### FTP (File Transfer Protocol)

- **Port:** 20 (data), 21 (control)  
- **Protocol:** TCP  
- **Purpose:** Files transfer karna server ↔ client ke beech.  
- **Security:** ❌ Insecure – Plain text me data transfer (credentials bhi visible).  
- **Attack Risk:** Credentials sniffing, FTP bounce attacks, Man-in-the-Middle.

#### SFTP (SSH File Transfer Protocol)

- **Port:** 22 (same as SSH)  
- **Protocol:** TCP over SSH  
- **Purpose:** Secure file transfer.  
- **Security:** ✅ Secure – Sabkuch encrypted (authentication + data), uses SSH.  
- **Key Feature:** Single port use karta hai, firewall friendly.

---

### B. Remote Access Protocols

#### Telnet (Telecommunication Network)

- **Port:** 23  
- **Protocol:** TCP  
- **Purpose:** Remote device ko command line access dena.  
- **Security:** ❌ Highly Insecure – Sab plain text (password bhi!).  
- **Use Case:** Sirf trusted LAN me debugging ke liye, Internet pe NEVER.

##### Telnet vs SSH – Analogy (Loudspeaker vs Secret Line)

- **Telnet (Loudspeaker):**  
  Aap door baithe naukar (server) ko chillakar order de rahe ho, mohalla ka har banda (hacker) sun sakta hai – tijori ka password bhi.

- **SSH (Secret Phone Line):**  
  Sirf aap aur server ek encrypted line pe baat kar rahe ho, bahar wala sirf noise sunega.

#### SSH (Secure Shell)

- **Port:** 22  
- **Protocol:** TCP  
- **Purpose:** Secure remote login, file transfer (SFTP/SCP), port forwarding.  
- **Security:** ✅ Highly Secure – Public key encryption, data encryption, integrity checking.  
- **Authentication:** Password ya Public Key (keys zyada secure).

**Interview Q:**  
"SSH Telnet se kyun better hai?"  
**Answer:**  
SSH sabkuch encrypt karta hai (commands, passwords, output), public-key authentication use karta hai, aur MITM attacks se protect karta hai.  
Telnet plain text me sab send karta hai, koi encryption nahi. SSH port 22, Telnet port 23 use karta hai.

---
### C. Web Protocols

#### HTTP (Hypertext Transfer Protocol)

- **Port:** 80  
- **Protocol:** TCP  
- **Purpose:** Web pages transfer (client ↔ server).  
- **Security:** ❌ Insecure – Plain text, data sniffing possible.  
- **Attack Risk:** Session hijacking, MITM, data interception.

#### HTTPS (HTTP Secure)

- **Port:** 443  
- **Protocol:** HTTP + TLS/SSL  
- **Purpose:** Secure web browsing.  
- **Security:** ✅ Secure – End-to-end encryption, certificate-based authentication.  
- **SSL/TLS:** Encryption layer jo data ko scramble kar deta hai.  
- **Practical Example:** Banking sites pe `https://` + browser lock icon.

**Interview Q:**  
"HTTP aur HTTPS me kya difference hai?"  
**Answer:**  
HTTP port 80 pe plain text me data send karta hai, insecure hai.  
HTTPS port 443 pe TLS/SSL encryption use karke data encrypt karta hai, certificates se authentication deta hai, MITM attacks se protect karta hai.

##### Simple Analogy

- **HTTP – Open Postcard:**  
  Raste me koi bhi postcard padh sakta hai (plain text data).

- **HTTPS – Locked Box:**  
  Data ek locked box me hai, key sirf client aur server ke paas, beech ka attacker sirf jumbled code dekhega (encrypted data).

---

### D. Email Protocols

#### SMTP (Simple Mail Transfer Protocol)

- **Ports:** 25 (standard), 587 (submission), 465 (SMTPS/secure).  
- **Protocol:** TCP.  
- **Purpose:** Email **send** karna (client → server → server).  
- **Security Risks:** Open relay misconfiguration, spam, phishing, SMTP smuggling.  
- **Modern Security:** SPF, DKIM, DMARC authentication use karo.

##### SMTP Analogy – Courier Boy

- Sirf **bhejna** (sending).  
- Flow: Sender ka computer → Sender mail server → Receiver mail server.  
- Courier letter le jata hai, wapas laane ka kaam nahi karta.

---
#### POP3 (Post Office Protocol v3)

- **Ports:** 110 (plain), 995 (SSL/TLS).  
- **Protocol:** TCP.  
- **Purpose:** Email **download** karna server se, phir server se delete kar dena.  
- **Limitation:** Single device use ke liye best, emails local ho jate hain.

##### POP3 Analogy – Old Style Post Box

- Post office se saare letters ek bag me bhar ke ghar le aana.  
- Server (post office) ka box almost khali ho jata hai.  
- Laptop pe download hua mail phone pe nahi dikhega (kyunki server se delete).

---

#### IMAP (Internet Message Access Protocol)

- **Ports:** 143 (plain), 993 (SSL/TLS).  
- **Protocol:** TCP.  
- **Purpose:** Email server pe hi store rehte, multiple devices se sync.  
- **Advantage:** Email organization server pe hi, har device se access.

##### IMAP Analogy – Cloud Storage / Mirror

- Ek "Jaadu ka Sheesha" (Mirror) post office me.  
- Aap ghar baithe mirror me dekh sakte ho kaunsa letter aaya hai.  
- Asli letter post office me hi rehta hai, har device (phone/laptop) se same view.

**Interview Q:**  
"SMTP, POP3, aur IMAP me kya difference hai?"  
**Answer:**  
SMTP outgoing protocol hai (email send karne ke liye), port 25/587 use karta hai.  
POP3 aur IMAP dono incoming protocols hain.  
POP3 (port 110/995) emails download karke server se delete kar deta hai, single device ke liye.  
IMAP (port 143/993) emails server pe store karta hai aur multiple devices se sync karta hai.

---

### E. DNS (Domain Name System)

- **Port:** 53 (TCP + UDP dono)  
- **Protocol:** UDP (queries), TCP (zone transfers)  
- **Purpose:** Domain names (example.com) ko IP addresses me convert karna.

#### Security Attacks

- **DNS Cache Poisoning/Spoofing:** Attacker fake DNS response inject karta hai, traffic malicious site pe redirect ho jati hai.
- **DNS Hijacking:** DNS server compromise karke sabhi queries hijack.

#### Prevention

- **DNSSEC** enable karo (authentication + integrity checking).
- Random source ports use karo jisse attacker guess na kar sake.
- DNS software regularly update karo patches ke liye.

**Interview Q:**  
"DNS attacks se kaise protect kare?"  
**Answer:**  
DNS cache poisoning se bachne ke liye DNSSEC enable karo (authentication + integrity checking), queries me random source ports use karo jisse attacker guess na kar sake, aur DNS software regularly update karo patches ke liye.

---
## 4️⃣ PORT STATES (Nmap Perspective)

Jab tu Nmap se scan karega, port ki 6 states ho sakti hain:

| State            | Meaning                                                    |
|------------------|---------------------------------------------------------|
| **Open**         | Port open hai, service listen kar rahi hai (connection accept karega) |
| **Closed**       | Port accessible hai but koi service nahi chal rahi      |
| **Filtered**     | Firewall/filter block kar raha hai, Nmap decide nahi kar sakta open/closed |
| **Unfiltered**   | Port accessible hai but open/closed confirm nahi        |
| **Open\|Filtered** | Open ya filtered - confirm nahi kar paya              |
| **Closed\|Filtered** | Closed ya filtered - confirm nahi kar paya          |

---

## 5️⃣ NMAP PRACTICAL COMMANDS (Lab ke liye)

### Basic Syntax

```bash
nmap [scan_type] [options] [target]
```

### Common Scans

#### 1. Default Scan (Top 1000 ports)

```bash
nmap 192.168.1.10
```

Sirf top 1000 most common ports scan karega.

#### 2. Specific Port Scan

```bash
nmap -p 80 192.168.1.10           # Single port
nmap -p 22,80,443 192.168.1.10    # Multiple ports
nmap -p 1-200 192.168.1.10        # Port range
```

#### 3. All Ports Scan

```bash
nmap -p- 192.168.1.10
```

Sabhi 65,535 ports scan karega (time zyada lagega).

#### 4. Fast Scan (Top 100 ports)

```bash
nmap -F 192.168.1.10
```

Sirf 100 most common ports.

#### 5. Service Version Detection

```bash
nmap -sV 192.168.1.10
```

Kon si service kaunse version me chal rahi hai, ye detect karega:

```text
22/tcp   open  ssh     OpenSSH 7.9p1
80/tcp   open  http    Apache 2.4.41
```

#### 6. SYN Stealth Scan (Most popular)

```bash
sudo nmap -sS 192.168.1.10
```

Half-open scan, faster aur stealthy (full TCP handshake complete nahi karta). Root privileges chahiye.

#### 7. TCP Connect Scan

```bash
nmap -sT 192.168.1.10
```

Full TCP handshake, no root needed, but logs me detect ho sakta hai.

#### 8. UDP Scan

```bash
sudo nmap -sU 192.168.1.10
```

UDP ports scan karne ke liye (DNS, DHCP, TFTP check karne ke liye).

### Output Example

```text
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
443/tcp  open  https
3306/tcp open  mysql
```

### Lab Exercise

Apne Kali VM se Metasploitable VM scan karo:

```bash
nmap -sV -p 1-1000 <metasploitable-ip>
```

---
## 6️⃣ SECURITY MINDSET (Attack Surface)

### Insecure Protocols (NEVER use on Internet)

- ❌ **FTP (port 21)** → Credentials plain text, can be corrupted by user
- ❌ **Telnet (port 23)** → Everything plain text
- ❌ **HTTP (port 80)** → No encryption
- ❌ **TFTP (port 69)** → No authentication

### Secure Alternatives

- ✅ **SFTP (port 22)** instead of FTP
- ✅ **SSH (port 22)** instead of Telnet
- ✅ **HTTPS (port 443)** instead of HTTP

### Common Attack Vectors

| Protocol | Attack Type                                  |
|----------|---------------------------------------------|
| HTTP     | Session hijacking, XSS, SQL Injection       |
| DNS      | Cache poisoning, spoofing                   |
| SMTP     | Spam relay, phishing, SMTP smuggling        |
| FTP/Telnet | Credential sniffing (Wireshark se easily visible) |

### Hardening Tips

1. **Close unused ports** – Firewall rules banao
2. **Use encrypted protocols** – HTTPS, SSH, SFTP
3. **Regular updates** – CVEs patch karo
4. **Strong authentication** – Public key > passwords
5. **Monitor logs** – Suspicious port scans detect karo

---

## 7️⃣ INTERVIEW-READY RAPID FIRE

### Top 30 Ports (Must Memorize!)

```text
20/21   - FTP Data/Control
22      - SSH/SFTP
23      - Telnet
25      - SMTP
53      - DNS
69      - TFTP
80      - HTTP
88      - Kerberos
110     - POP3
143     - IMAP
443     - HTTPS
465     - SMTPS
587     - SMTP Submission
993     - IMAPS
995     - POP3S
3306    - MySQL
3389    - RDP
5432    - PostgreSQL
```

### Common Interview Questions

**Q1:** "Port 80 open hai but 443 closed, kya risk hai?"  
**A:** Website HTTP pe serve ho rahi hai (insecure), HTTPS nahi. Data plain text me travel karega, MITM attacks possible hain. User credentials, session tokens sniff ho sakte hain.

**Q2:** "TCP aur UDP me main difference kya hai?"  
**A:** TCP connection-oriented hai, reliable hai, ordered delivery guarantee karta hai, handshake use karta hai – HTTP/SMTP/FTP ke liye. UDP connectionless hai, fast hai but unreliable – DNS/VoIP/Gaming ke liye.

**Q3:** "Nmap -sS vs -sT me kya fark hai?"  
**A:** -sS (SYN scan) half-open connection hai, stealthy hai, root privileges chahiye. -sT (TCP connect) full handshake karta hai, logs me easily detect ho sakta hai, no root needed.

**Q4:** "DNS pe kaun se attacks possible hain?"  
**A:** DNS cache poisoning – attacker fake DNS response inject karta hai, victim malicious IP pe redirect ho jata hai. Prevention: DNSSEC enable karo, random source ports use karo.

**Q5:** "Email protocols ka flow explain karo."  
**A:** Sender SMTP (port 25/587) use karke email send karta hai apne server pe. Receiving server bhi SMTP se email receive karta hai. Phir recipient POP3 (110/995) ya IMAP (143/993) use karke email download/access karta hai. SMTP outgoing hai, POP3/IMAP incoming.

---
## 8️⃣ TODAY'S LAB TASKS (2-3 hours)

### Task 1: TryHackMe – "Protocols and Servers" Room

- Module complete karo, notes banao
- Key concepts document karo

### Task 2: Nmap Practice

VirtualBox me Metasploitable/DVWA setup karke ye commands run karo:

```bash
# Basic scan - Identify ports
nmap <target-ip>

# Specific common ports
nmap -p 21,22,23,80,443,3306 <target-ip>

# Service detection
nmap -sV -p 1-1000 <target-ip>

# Fast scan
nmap -F <target-ip>
```

**Document karo:**

1. Kitne ports open mile?
2. Kaun si services detect hui?
3. Koi insecure protocol (FTP/Telnet/HTTP) hai kya?
4. Service versions note karo

### Task 3: Wireshark Capture (Bonus)

1. Apne browser se HTTP site open karo (http://testphp.vulnweb.com/)
2. Wireshark me capture karo
3. Filter lagao: `http`
4. Plain text data dekho (GET request, headers)
5. Compare karo: HTTPS site (https://google.com) pe same capture karo – encrypted dikhega!

**Key Learning:**

- HTTP me sab plain text visible
- HTTPS me encrypted data
- Credentials kaise sniff ho sakte hain HTTP pe

---

## 📝 Summary

Yeh notes cover karte hain:

- ✅ Ports kya hain (ranges, categories)
- ✅ TCP vs UDP differences
- ✅ Common protocols (FTP, SSH, HTTP/HTTPS, SMTP, POP3, IMAP, DNS)
- ✅ Security implications of each protocol
- ✅ Nmap practical commands
- ✅ Port states aur scanning techniques
- ✅ Interview questions aur answers
- ✅ Hands-on lab exercises

**Next Steps:**

1. Practice Nmap commands daily
2. Try TryHackMe/HackTheBox networking rooms
3. Setup home lab with VMs
4. Document all scans aur findings
5. Review interview questions regularly

---

*Happy Learning! 🚀*
