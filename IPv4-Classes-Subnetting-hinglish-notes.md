# IPv4 Classes, Subnetting & IP Addressing (Simple Hinglish Notes)

IPv4 addressing aur subnetting networking ka important concept hai. Ye notes exams, interviews, aur practical implementation ke liye easy Hinglish mein breakdown kiya gaya hai.

---

## 1️⃣ IPv4 Classes – Clean Notes

### Overview
IPv4 addresses 5 classes me divided hote hain: A, B, C, D, E. Think of these like different sizes of housing blocks for devices on the internet. The first number (first octet) batata hai IP ka class.

### Quick Summary Table

| Class | First Octet Range | Best For... | Approx Devices (Hosts) |
|-------|-------------------|-------------|------------------------|
| **A** | 1 to 126 | Huge companies (Apple, Google) | 16 Million+ per network |
| **B** | 128 to 191 | Medium companies/Universities | 65,534 per network |
| **C** | 192 to 223 | Small businesses/Home WiFi | 254 per network |
| **D** | 224 to 239 | Multicasting (Streaming/Video) | N/A (no normal hosts) |
| **E** | 240 to 255 | Research & Experiments | N/A (reserved) |

---

### 1. Class A (The Giants)
- **Range:** 1.x.x.x to 126.x.x.x
- **Structure:** First part (first octet) Network; baaki 3 parts Devices ke liye.
- **Use:** Sirf 126 organizations ke paas Class A ho sakta hai, lekin har ek ke paas millions of devices ka space hota hai.
- **Note:** 127.x.x.x skip hota hai kyunki ye loopback/testing ke liye use hota hai.

### 2. Class B (The Mid-Sized)
- **Range:** 128.x.x.x to 191.x.x.x
- **Structure:** Pehle do parts Network; last do parts Devices ke liye.
- **Use:** Large universities, mid-sized corporations jinko thousands IPs chahiye.

### 3. Class C (The Common One)
- **Range:** 192.x.x.x to 223.x.x.x
- **Structure:** Pehle teen parts Network; sirf last part Devices ke liye.
- **Use:** Home/small office networks. Router ka IP often 192.168.1.1 hota hai. Ye around 254 devices support kar sakta hai.

### 4. Class D & E (Special Cases)
- **Class D:** Reserved for Multicasting – jab ek sender ko ek specific group ko data bhejna ho (live streaming/video etc.).
- **Class E:** Reserved for Experimental use by researchers/engineers; normal daily life me nahi dikhta.

---

### How to Identify IP Class Instantly
Bas first octet (first number) dekho:
- **1–126 ⇒ Class A**
- **128–191 ⇒ Class B**
- **192–223 ⇒ Class C**
- **224–239 ⇒ Class D**
- **240–255 ⇒ Class E**

*(Example style from your note: "Is it 192? It's Class C. Is it 10? It's Class A private IP class range me aata hai.")*

---

## 2️⃣ Public vs Private IP – School Analogy

### 1. Public IP (School ka Address)
- Pure world me agar kisi ko aapke school ko letter bhejna hai, to woh school ke main address (Public IP) par bhejega.
- Ye address city/world me unique hota hai.
- Ye aapke pure network (ghar/school) ki pehchan hai.
- Bahar ki duniya (Internet) sirf isi address ko dekh sakti hai.

### 2. Private IP (Aapka Roll No. / Name)
- School ke andar Principal ko pata hona chahiye ki letter kis student ke paas jana hai. Woh student ka naam ya roll number (Private IP) check karega.
- Ye address sirf school ke andar kaam karta hai.
- Do alag-alag school me same roll number ho sakta hai (Roll No. 1), waise hi do alag-alag gharon me same Private IP (jaise 192.168.1.1) ho sakta hai. Isse problem nahi hoti kyunki woh apne-apne "school" ke andar hain.

### Inka "Teamwork" kaise hota hai?
Jab aap YouTube par video dekhte hain:
1. Aapka phone (Private IP) router ko bolta hai: "Mujhe video chahiye."
2. Router aapki request leta hai aur apna Public IP stamp laga kar Internet ko bhej deta hai.
3. Jab video wapas aata hai, router dekhta hai ki "ye request toh 9/A wale student ne ki thi", aur video seedha aapke phone par bhej deta hai.

### Short Comparison

| Feature | Public IP (School Building) | Private IP (Student Name/ID) |
|---------|----------------------------|------------------------------|
| **Visible to…** | Whole Internet | Only your local network |
| **Who gives it?** | ISP (Airtel/Jio, etc.) | Your Router (DHCP) |
| **Uniqueness** | Unique in the world | Unique only inside your house/network |
| **Example** | 122.161.x.x | 192.168.x.x |

---

## 3️⃣ Special Ranges – Loopback & APIPA

### 1. Loopback Address (127.0.0.0 to 127.255.255.255)
- **Sabse common address:** 127.0.0.1
- **Simple Matlab:** "Self" ya localhost – apne hi system se baat karna.
- **Analogy:** Jaise aap sheeshe (mirror) me khud se baat kar rahe ho.
  
#### Kaam kya hai?
- Agar aapne apne computer par website banayi hai aur check karna hai ki woh chal rahi hai ya nahi (bina Internet ke), to browser me **127.0.0.1** type kar sakte ho.

#### Testing:
- Agar Internet issue hai, `ping 127.0.0.1` likh ke dekhte hain.
- Agar reply aata hai, iska matlab system ka internal networking (NIC card) sahi kaam kar raha hai.

---

### 2. APIPA (169.254.0.0 to 169.254.255.255)
- **APIPA ka full form:** Automatic Private IP Addressing.
- **Simple Matlab:** Ye ek "Emergency IP" hai.
- **Analogy:** School me naye students aaye, lekin Principal (Router/DHCP) chhutti pe hai, kisi ko Roll No. nahi mila. Students temporary ID bana lete hain taaki aapas me baat kar saken.

#### Kab milta hai?
- Jab computer router/DHCP se IP lene ki koshish karta hai lekin router response nahi de pata, to Windows khud se 169.254.x.x range me IP assign kar deta hai.

#### Problem:
- Agar tumhare PC pe **169.254.x.x** dikh raha hai, samajh jao Internet nahi chalega, kyunki router se proper connection nahi bana.

---

### Quick Table Revision

| Type | Range | Purpose |
|------|-------|---------|
| **Loopback** | 127.x.x.x | Apne hi system ko test karne ke liye (self-testing). |
| **APIPA** | 169.254.x.x | Jab router/DHCP IP na de paye (auto-config error). |

---

## 4️⃣ Subnetting – Analogy + Core Ideas

Subnetting thoda technical lag sakta hai, par school analogy yaad rakho to simple ho jata hai.

**Subnetting** = ek bade network (badi class) ko chhote-chhote groups (sections) me todna taaki management easy ho jaye.

---

### 1. Subnet Mask Kya Hota Hai?
Subnet mask ek "filter" jaisa hai jo batata hai IP address ka kaunsa hissa **Network** (School/Class) hai aur kaunsa **Host** (Student).

- **Example mask:** 255.255.255.0 (jise /24 bhi kehte hain)
  - **255 ka matlab:** "ye bits network ke liye locked" (1s in binary).
  - **0 ka matlab:** "ye bits host ke liye free" (0s in binary).
  - Is mask me pehle 3 parts network, sirf last part devices ke liye.

---

### 2. Hosts Calculate Karne Ka Formula
Ek subnet me kitne devices lag sakte hain, iske liye formula:

**Usable Hosts = 2^h − 2**

- **h** = host bits (jitne zeros bache hain mask me).
- **"−2"** isliye kyunki:
  - Pehla address = **Network ID**
  - Aakhri address = **Broadcast ID**
  - Ye dono kisi device ko assign nahi hote.

---

### 3. Network, Broadcast aur Usable Range – Example

**Example:** 192.168.1.0/24

- **Network ID:** 192.168.1.0 – pure group ka naam.
- **Broadcast ID:** 192.168.1.255 – sabko ek saath message bhejna ho to.
- **Usable Range:** 192.168.1.1 – 192.168.1.254 (total 254 devices connect ho sakte hain).

---

### 4. Simple Subnetting Examples (/24, /25, /26, /30)

Jaise-jaise "slash" (/CIDR) ka number badhta hai, network chhota hota jaata hai (hosts kam hote jate).

| CIDR | Subnet Mask | Total Hosts | Usable Hosts (2^h − 2) | Use Case |
|------|-------------|-------------|------------------------|----------|
| **/24** | 255.255.255.0 | 256 | 254 | Standard home/office LAN |
| **/25** | 255.255.255.128 | 128 | 126 | Network ko 2 parts me baantna |
| **/26** | 255.255.255.192 | 64 | 62 | Network ko 4 parts me baantna |
| **/30** | 255.255.255.252 | 4 | 2 | Sirf 2 routers ko jodne ke liye (P2P) |

---

### Short Summary Tip:
- **/24 = 1 room** jisme 254 log baith sakte hain.
- **/25 = us room ke beech me wall**, ab 126–126 ke 2 rooms ban gaye.
- **/30 = chhota cabin** jisme sirf 2 log – point‑to‑point connection between routers.

---

## 5️⃣ CIDR ↔ Subnet Mask Conversion

Isse samajhne ka sabse simple tarika binary hai, par tum table se bhi yaad rakh sakte ho.

Jab hum /24 se aage badhte hain, to hum last octet ke bits "borrow" karte hain.

---

### Mapping Table

| CIDR | Subnet Mask | Logic (Last Octet Binary) |
|------|-------------|---------------------------|
| **/24** | 255.255.255.0 | 00000000 (saare bits free for hosts) |
| **/25** | 255.255.255.128 | 10000000 (1 bit lock: 2^7 = 128) |
| **/26** | 255.255.255.192 | 11000000 (2 bits lock: 128+64=192) |
| **/27** | 255.255.255.224 | 11100000 (3 bits lock: 128+64+32) |
| **/30** | 255.255.255.252 | 11111100 (6 bits lock: 255−3=252) |

---

### CIDR se Addresses/Hosts Nikalna

Total addresses ka formula:

**Total Addresses = 2^(32 − CIDR)**

#### Examples:
- **/24:** 32−24 = 8 bits free ⇒ 2^8 = 256 addresses (254 usable).
- **/25:** 32−25 = 7 bits free ⇒ 2^7 = 128 addresses (126 usable).
- **/26:** 32−26 = 6 bits free ⇒ 2^6 = 64 addresses (62 usable).
- **/30:** 32−30 = 2 bits free ⇒ 2^2 = 4 addresses (2 usable).

---

### Yaad rakhne ki trick:
Har baar jab CIDR number +1 hota hai (jaise /24 → /25), to network ka size **half** ho jata hai:
- /24 = 256
- /25 = 128
- /26 = 64
- /27 = 32 … and so on.

---

## Summary

Sab content tumhare notes ka hi hai, bas headings, tables, aur flow professional style me arrange kiya gaya hai, kuch missing context (ranges, formulas) ko complete karne ke liye 1–2 simple lines add ki gayi hain.

---

**Happy Networking! 🚀**
