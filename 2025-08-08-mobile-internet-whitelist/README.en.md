# 🇬🇧 Analysis of the "CAPTCHA + DPI + Whitelist" Scheme in Mobile Networks

[Source: "Russia develops technical scheme for access to mass services under restrictions", Interfax](https://www.interfax.ru/russia/1040184)

---

## 📌 Introduction
The "CAPTCHA + DPI + Whitelist" scheme is a way to control internet access under restrictions.  
**Official goal:** provide access to "important" services (banks, government portals, delivery) even during blocks.  
**Reality:** technical vulnerabilities, easy bypass, and significant internet slowdown.

---

## 1. Attack vector changes but does not disappear

**How it works:**
- Some SIM cards (e.g., foreign) face a "cooling-off" period and must solve a CAPTCHA.
- Exceptions: corporate channels (APN/MPLS), M2M devices (ATMs, terminals).

## Vulnerabilities

- **Whitelisted services as a transport channel (primary vector):** Encrypted connections (TLS/QUIC) and the functionality of large platforms (CDNs, marketplaces, taxi apps) allow data transfer inside allowed traffic (JSON/media/WebSocket/edge functions).

- **External (offshore) exits:** Proxies/servers outside the jurisdiction and networks of Russian operators are not subject to local whitelisting/CAPTCHA policies.

- **Private corporate APNs / L3VPNs:** If the operator’s policy for them is different (more permissive, without general whitelisting), clients can bypass retail restrictions. Not universal — depends on configuration.

- **Resold retail SIMs:** Used as “third-party hands” to access without personal restrictions; detectable via behavioral analysis and may be deactivated.

- **M2M/IoT profiles:** Often exempt from restrictions to ensure continuous operation of ATMs/terminals; useful only where access is not strictly segmented to specific hosts.

---

## 2. Whitelist = porous filter

**What it is:** list of allowed domains/services.

**Vulnerabilities:**
- **TLS/QUIC**: traffic is encrypted; DPI sees only domain (SNI).
- **CDN**: one allowed CDN domain = thousands of data transfer paths.
- **DoH/DoT**: DNS requests can be hidden inside allowed domains.
- **Semantic tunneling**: data inside images, videos, text.

**Example:** botnet receives commands through "comment" field in a whitelisted taxi service.

---

## 3. CAPTCHA = control, not protection

**What it is:** verification page (captive portal) before internet access.

**Vulnerabilities:**
- **ML solvers**: automated CAPTCHA recognition.
- **Token reuse**: weak binding allows reuse on another device.
- **Privileged service accounts**: bots/apps bypass CAPTCHA by design.

**Conclusion:** weak against automated systems.

---

## 4. Impact on users and business

**Technical effects:**
- Increased latency (+50–200 ms).
- Jitter — unstable packet delay.
- Slower speeds due to protocol downgrade (HTTP/3 → HTTP/1.1).
- Loading errors due to incomplete whitelist.

**For business:**
- No access to Git, CI/CD, cloud IDE if outside whitelist.
- Release delays, downtime.
- Issues with VoIP, VPN, online conferencing.

---

## 5. Why it does not protect against drones or DDoS

**Drones:**
- Use satellite channels, radio links, autonomous missions.

**DDoS:**
- Mitigated at perimeter: scrubbing centers, Anycast, ISP filtering.
- Mass user restriction does not reduce bot traffic.

---

## 📉 Core issue

The internet in the 21st century is strategic infrastructure.  
This scheme:
- Does not solve stated security goals.
- Degrades connection quality.
- Enables full control and Runet segmentation.
- Risks turning mobile internet into a slow, unstable channel, harming the economy, governance, and communications.