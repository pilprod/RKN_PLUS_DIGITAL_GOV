# Analysis of the "CAPTCHA + DPI + Whitelist" Scheme in Mobile Networks

[Source: "Russia has developed a technical scheme for access to mass services under restrictions", Interfax](https://www.interfax.ru/russia/1040184)

---

## 📌 Introduction
The "CAPTCHA + DPI + Whitelist" scheme is a method of managing internet access under restrictions.  
**Officially stated goal:** to ensure access to "important" services (banks, government services, delivery) even during blockages.  
**Reality:** technical vulnerabilities, possibilities for circumvention, and significant degradation of internet quality.

---

## 1. The Attack Vector Changes but Does Not Disappear

**How it works:**  
- Upon network entry, some SIM cards (e.g., foreign ones) experience a delay ("cooldown") and are required to pass a CAPTCHA.
- Exceptions: corporate channels (APN/MPLS), M2M devices (ATMs, terminals).

**Vulnerabilities:**

- **Whitelisted services as transport (main vector):** encrypted connections (TLS/QUIC) and functionalities of large platforms (CDN, marketplaces, taxi services) allow data transmission inside permitted traffic (JSON/media/WebSocket/edge functions).

- **External (offshore) exits:** proxies/servers outside the jurisdiction and networks of Russian operators are not subject to local whitelisting/CAPTCHA policies.

- **Private corporate APN/L3VPN:** with different operator-level policies (softer, without general whitelisting) allow clients to bypass retail restrictions. Not universal — depends on configurations.

- **Resold retail SIMs:** used as "foreign hands" to access without personal restrictions; detected by behavioral patterns and can be disabled.

- **M2M/IoT profiles:** often exempted to maintain continuity of ATMs/terminals; useful only where access is not strictly segmented to specific nodes.

**Conclusion:** restrictions are easily bypassed, preserving channels for attacks (DDoS, botnet or drone control).

---

## 2. The "Whitelist" is a Leaky Filter

**What it is:** a list of allowed domains and services.

**Vulnerabilities:**
- **TLS/QUIC:** traffic is encrypted, DPI sees only the domain (SNI), not the data.
- **CDN:** one allowed CDN domain equals thousands of paths for data transfer.
- **DoH/DoT:** DNS queries can be hidden inside allowed domains.
- **Semantic tunneling:** data transfer inside images, videos, texts.

**Example:** a botnet receives commands through the "comment" field in an allowed taxi service.

---

## 3. CAPTCHA — Control, Not Protection

**What it is:** a blocking/unblocking mechanism implemented via a captive portal that requires user interaction to gain internet access. Unlike traditional CAPTCHA puzzles, this system controls access by presenting a verification page that must be completed to unlock connectivity.

**Vulnerabilities:**
- **ML solvers:** automatic recognition and solving of CAPTCHA challenges.
- **Token reuse:** with weak binding, tokens can be reused on different devices or sessions.
- **Privileged service accounts:** bots and applications that bypass CAPTCHA by design.
- **Protocol knowledge exploitation:** if the unlocking protocol is known, it can be automated and replayed to bypass restrictions.
- **Automated replay attacks:** repeated submission of unlock requests can circumvent the blocking mechanism without user interaction.

**Conclusion:** protection is weak against automated systems and protocol-aware attackers, rendering the mechanism ineffective as a robust barrier.

---

## 4. Consequences for Users and Business

**Technical effects:**
- Increased latency (ping +50–200 ms).
- Jitter — unstable packet delay.
- Speed drop due to protocol downgrades (HTTP/3 → HTTP/1.1).
- Loading errors due to incomplete whitelist.

**For business:**
- Inaccessibility of Git, CI/CD, cloud IDEs if they are outside the whitelist.
- Release failures, downtime.
- Problems with VoIP, VPN, and online conferences.

---

## 5. Why This Does Not Protect Against Drones and DDoS

**Drones:**
- Use satellite channels, radio links, autonomous scenarios.

**DDoS:**
- Mitigated at the perimeter: scrubbing centers, Anycast, provider filtering.
- Mass user restrictions do not reduce bot traffic.

---

## 📉 Key Issue

The internet in the 21st century is strategic infrastructure.  
This scheme:
- Does not solve the declared security tasks.
- Degrades communication quality.
- Creates prerequisites for full control and segmentation of the Runet.
- Leads to turning mobile internet into a slow and unstable channel, reducing the efficiency of the economy, government, and communications.