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

**Vulnerabilities:**
- **Dead SIMs**: registered but unused SIMs can be handed over.
- **Expat SIMs**: VPN/proxy from abroad.
- **Corporate APN/MPLS**: separate routing without DPI filtering.
- **M2M**: long-lived sessions without restrictions.

**Conclusion:** easy to bypass while keeping channels open for DDoS, botnet or drone control.

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