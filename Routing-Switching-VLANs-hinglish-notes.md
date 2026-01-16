# 🔗 Routing, Switching & VLANs (Simple Hinglish Notes)

Networking ke teen important pillars hain: Routing, Switching, aur VLANs. Ye notes exams, interviews, aur practical implementation ke liye easy Hinglish mein breakdown kiya gaya hai.

---

# 📡 1. Routing – Path Selection Ka Master

## 1. What is Routing?

Routing ka simple matlab hai "Best Path Selection". Jab data ek network se nikal kar doosre network mein jaana chahta hai, toh Router decide karta hai ki sabse sahi raasta kaunsa hai.

### Router ke Core Concepts:

• **Router Role**: Ye Layer 3 (Network Layer) device hai. Iska kaam do ya do se zyada alag IP networks ko connect karna hai.

• **Path Selection**: Router apni "Routing Table" check karta hai aur dekhta hai ki destination tak pahunchne ke liye sabse fast ya sasta raasta kaunsa hai.

• **Next-Hop Concept**: Router poora rasta ek baar mein nahi tay karta. Woh bas data ko "Agli Gali" ya Next-Hop (agla router) ki taraf dhakel deta hai.
  - **Analogy**: Jaise aap bus conductor se puchte ho "Delhi jaana hai", woh kehta hai "Agli bus pakdo jo Jaipur ja rahi hai". Jaipur wala router agla decision lega.

---

## 2. Types of Routes

Router ko rasta batane ke teen tarike hote hain:

| Route Type | Meaning (Hinglish) | Best Use Case |
|------------|--------------------|--------------|
| **Static Route** | Admin manually rasta enter karta hai. "Bhai, isi raste se jaana." | Small networks jahan raste change nahi hote. |
| **Dynamic Route** | Routers aapas mein protocols (OSPF, RIP) ke zariye baat karke khud rasta dhundte hain. | Bade networks jahan koi link down ho toh rasta khud badal jaye. |
| **Default Route** | "Agar tumhe rasta nahi pata, toh saara traffic is router ko bhej do." | Ghar ke router se Internet ki taraf jaane ke liye. |

---

## 3. Routing Table Basics

Router ke andar ek table hoti hai jise dekh kar woh decision leta hai. Isme main char cheezein hoti hain:

• **Destination Network**: Woh network jahan data jaana chahta hai (e.g., 192.168.2.0).

• **Subnet Mask**: Network ka size batata hai.

• **Next Hop**: Agle router ka IP address jahan packet bhejna hai.

• **Metric**: Ye ek "Score" hai. Agar ek jagah jaane ke do raste hain, toh jis raste ka Metric kam hoga, router wahi rasta chunega.

---

## 4. Routing Protocols Overview (Intro Level)

Dynamic routing ke liye routers protocols ka use karte hain:

• **RIP (Routing Information Protocol)**: Sabse purana aur simple. Ye sirf Hops ginta hai (kitne routers beech mein hain). Iski limit 15 hops tak hoti hai.

• **OSPF (Open Shortest Path First)**: Sabse zyada use hone wala protocol. Ye Speed (Bandwidth) dekhta hai. Agar ek rasta lamba hai par super-fast hai, toh OSPF use chunega.

• **EIGRP**: Cisco ka apna fast protocol. Ye speed aur delay dono ko mix karke best path nikalta hai.

• **BGP (Border Gateway Protocol)**: Isse "Internet ka Protocol" kehte hain. Ye badi companies (like Google, Airtel) aur ISPs ke beech traffic handle karta hai.

---

# 🔌 2. Switching – Smart Connection Manager

## 1. What is a Switch? (The Intelligent Device)

Switch ek Layer 2 (Data Link Layer) device hai jo devices ko LAN mein connect karta hai. Ye Hub se zyada smart hota hai kyunki ye MAC Addresses ko pehchanta hai.

• **MAC Address Table**: Switch ke dimaag mein ek list hoti hai jise CAM Table (Content Addressable Memory) kehte hain. Isme likha hota hai ki kaunsa MAC address kis Port se juda hai.

• **Frame Forwarding**: Jab koi data (Frame) switch ke paas aata hai, switch uske "Destination MAC" ko dekhta hai aur sirf usi port par data bhejta hai jahan wo device connected hai.

---

## 2. Domains & Differences (Hub vs Switch vs Router)

### Collision vs Broadcast Domain

• **Collision Domain**: Wo area jahan do devices agar ek saath data bhejein toh "takkar" (collision) ho jaye. Switch ke har port ka apna alag collision domain hota hai (No collisions!).

• **Broadcast Domain**: Wo area jahan tak ek "Broadcast" message pahunchta hai. Switch ke saare ports milkar ek hi broadcast domain banate hain. Isko todne ke liye Router ki zaroorat padti hai.

### Comparison Table

| Feature | Hub | Switch | Router |
|---------|-----|--------|--------|
| **Layer** | Layer 1 (Physical) | Layer 2 (Data Link) | Layer 3 (Network) |
| **Address Type** | Kuch nahi (Dumb) | MAC Address | IP Address |
| **Data Unit** | Bits | Frames | Packets |
| **Intelligence** | Sabko data bhejta hai (Broadcast) | Sirf sahi device ko bhejta hai (Unicast) | Alag networks ko connect karta hai |

---

## 3. Switching Methods: Kaam Karne ka Tareeka

Jab switch ke paas frame aata hai, toh wo use aage bhejne ke liye do main methods use karta hai:

• **Store-and-Forward**: Switch pehle poora frame receive karega, check karega ki koi error toh nahi hai (CRC check), aur phir aage bhejega.
  - **Fayda**: Bilkul error-free data.
  - **Nuksan**: Thoda slow hota hai.

• **Cut-Through**: Switch sirf frame ka destination MAC address padhta hai (shuruati 6-14 bytes) aur turant forwarding shuru kar deta hai.
  - **Fayda**: Super fast (Low latency).
  - **Nuksan**: Error wala data bhi aage bhej deta hai.

---

## 4. CAM/MAC Table Behavior (Learning, Aging, Flooding)

Switch apni table khud banata hai, usse koi sikhata nahi hai. Iske 3 main steps hain:

• **Learning**: Jab PC-A kisi ko data bhejta hai, switch uska Source MAC address aur Port number apni table mein note kar leta hai.

• **Flooding (Unknown Unicast)**: Agar switch ko destination ka rasta nahi pata, toh wo us frame ki copy saare ports par bhej deta hai (except jahan se wo aaya). Ise "Flooding" kehte hain.

• **Aging**: Agar koi device bahut der tak baat nahi karta, toh switch uska entry table se mita deta hai (default 300 seconds) taaki table kachre se na bhar jaye.

---

# 🏢 3. VLANs – Virtual Network Ka Jaadu

## 1. VLAN Basic Concept: Logical Deewar

Socho ek bada office hai jahan HR, Sales, aur IT departments hain. Sab ek hi switch se jude hain. Agar HR ka koi sensitive data broadcast hota hai, toh woh Sales wale ke PC par bhi jayega.

• **Logical LAN**: VLAN physical wiring badle bina, software ke zariye networks ko alag kar deta hai.

• **Broadcast Domain Separation**: Har VLAN ka apna alag broadcast domain hota hai. VLAN 10 ka "shor" (broadcast) VLAN 20 ko sunayi nahi dega. Isse security badhti hai aur network congestion kam hota hai.

---

## 2. Types of VLANs (Intro)

Switch par alag-alag kaam ke liye alag VLANs banaye jaate hain:

• **Data VLAN**: Sirf user data (emails, web browsing) carry karne ke liye.

• **Voice VLAN**: IP Phones ke liye. Isse "High Priority" di jaati hai taaki call drop na ho.

• **Native VLAN**: Trunk port par jo traffic bina kisi "Tag" (bin-sticker) ke aata hai, use Native VLAN mein daal diya jata hai (Default: VLAN 1).

• **Management VLAN**: Switch ko remotely access (SSH/Telnet) karne ke liye ek alag private VLAN.

---

## 3. Ports: Access vs Trunk & 802.1Q

Jab data ek switch se doosre switch par jata hai, toh switch ko kaise pata chalta hai ki ye data kis VLAN ka hai? Iske liye hum ports ko configure karte hain:

• **Access Port**: Ye sirf ek hi VLAN ka member hota hai. Isme hum PC ya Laptop connect karte hain. Iska traffic "untagged" hota hai.

• **Trunk Port**: Ye do switches ya switch aur router ke beech hota hai. Ye saare VLANs ka traffic ek saath carry kar sakta hai.

• **802.1Q Tagging**: Jab data trunk se guzarta hai, toh switch us par ek "Tag" (chota sa sticker) laga deta hai, jaise "Main VLAN 10 ka hoon". Is standard ko 802.1Q kehte hain.

---

## 4. Inter-VLAN Routing: Baat kaise karwayein?

Agar HR (VLAN 10) ko Sales (VLAN 20) ko koi file bhejni hai, toh wo switch ke andar-andar nahi ja sakti. Hume ek Layer 3 device (Router ya L3 Switch) chahiye.

### Router-on-a-Stick:

• Router aur Switch ke beech sirf ek physical cable hoti hai.

• Router par hum "Sub-interfaces" banate hain (e.g., Gig0/0.10 for VLAN 10).

• Data switch se router tak jata hai, wahan se ghoom kar wapas doosre VLAN mein aata hai.

### Layer 3 Switch (SVI Concept):

• Ye modern tarika hai. Hum switch ke andar hi ek virtual interface bana dete hain jise SVI (Switch Virtual Interface) kehte hain (e.g., interface vlan 10).

• Isme routing switch ke hardware mein hi ho jati hai, jo bahut fast hoti hai.

---

## 📚 Summary Table: Routing vs Switching vs VLANs

| Feature | Routing | Switching | VLANs |
|---------|---------|-----------|-------|
| **Layer** | Layer 3 | Layer 2 | Layer 2 (Logical) |
| **Purpose** | Networks ko connect karna | Devices ko connect karna | Devices ko logically separate karna |
| **Address** | IP Address | MAC Address | VLAN ID |
| **Device** | Router | Switch | Switch (with VLAN config) |
| **Example** | Internet connection | Office LAN | HR aur Sales ko alag karna |

---

## 🎯 Key Takeaways

1. **Routing**: Best path selection karta hai networks ke beech. Routing Table aur Protocols (OSPF, RIP) ka use hota hai.

2. **Switching**: MAC address table use karke frames ko sahi device tak bhejta hai. Hub se smart hai.

3. **VLANs**: Ek switch par multiple logical networks banata hai. Security aur traffic management improve hota hai.

4. **Inter-VLAN**: VLANs ke beech communication ke liye Router ya Layer 3 Switch chahiye.

---

**Happy Networking! 🚀**
