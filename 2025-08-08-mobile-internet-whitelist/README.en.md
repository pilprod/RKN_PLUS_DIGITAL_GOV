# Analysis of the "CAPTCHA + DPI + Whitelist" Scheme in Mobile Networks

[Source: "Russia has developed a technical scheme for access to mass services under restrictions", Interfax](https://www.interfax.ru/russia/1040184)

---

## 📌 Introduction
The "CAPTCHA + DPI + Whitelist" scheme is a method for managing internet access under restrictions.  
**Officially stated goal:** to ensure access to "important" services (banks, government services, delivery) even during blockages.  
**Reality:** technical vulnerabilities, circumvention possibilities, and significant degradation of internet quality.

---

## 1. The Attack Vector Changes but Does Not Disappear

**How it works:**  
- Upon network entry, some SIM cards (e.g., foreign ones) experience a delay ("cooldown") and must pass a CAPTCHA.  
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

**Real-world story:**  
A company’s developer tried to push code via Git over HTTPS but faced repeated timeouts. The CI/CD pipeline failed, delaying releases. Switching to VPN was impossible due to whitelist restrictions, causing significant productivity loss.

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

---

## ⚠️ Network Degradation and Barriers to Import Substitution

The scheme further complicates the implementation of import substitution and digital sovereignty policies by:

- Limiting access to foreign cloud services and tools essential for development.
- Forcing reliance on a narrow set of "approved" providers, often less efficient or innovative.
- Increasing operational costs due to degraded network quality and additional administrative overhead.

This approach risks isolating the Russian segment of the internet and hindering technological progress rather than securing it.
# How the new internet blocking system affects users in Russia

Although the scheme is being rolled out by mobile operators first, similar approaches and consequences are possible in fixed (wired, fiber, corporate) networks as well, affecting internet access across the country.

[Source: "Russia has developed a technical scheme for access to mass services under restrictions", Interfax](https://www.interfax.ru/russia/1040184)

---

## Introduction
The "CAPTCHA + DPI + Whitelist" scheme is a way to manage internet access under restrictions.  
**Officially stated goal:** ensure access to "important" services (banks, government services, delivery) even during blocks.  
**Reality:** technical vulnerabilities, circumvention possibilities, and a significant drop in internet quality.

---

## ⚠️ Network Degradation and Barriers to Import Substitution

Multi-layer DPI, whitelisting, and mandatory authorization introduce constant additional latency and single points of failure, reduce throughput, increase network OPEX for operators, and severely constrain the flexibility of infrastructure upgrades.

- Dependence on foreign DPI/filtering vendors, which contradicts import substitution goals.
- Integration challenges with domestic software/hardware because DPI and captive-portal protocols are often proprietary.
- Rising costs of maintenance and modernization, diverting resources away from network development and new technologies (5G, edge computing).
- Slower innovation in the telecom sector and reduced competitiveness of Russian solutions in global markets.

In the long term, these constraints lead to technological lag and reduced cyber-resilience.

---

## 1. The Attack Vector Changes but Does Not Disappear

**How it works:**  
- Upon network entry, some SIM cards (e.g., foreign ones) face a delay (a "cooldown") and must pass a CAPTCHA.  
- Exceptions: corporate channels (APN/MPLS), M2M devices (ATMs, terminals).

**Vulnerabilities:**

1. **Whitelisted services as transport (primary vector):** encrypted connections (TLS/QUIC) and the functionality of large platforms (CDN, marketplaces, taxi services) allow data exchange inside permitted traffic (JSON/media/WebSocket/edge functions).

2. **External (offshore) exits:** proxies/servers outside the jurisdiction and networks of Russian operators are not subject to local whitelisting/CAPTCHA policies.

3. **Private corporate APN/L3VPN:** if operator-level policy differs (more permissive, without the general whitelist), clients can bypass retail restrictions. Not universal — depends on configuration.

4. **Resold retail SIMs:** used as “third-party hands” to access without personal restrictions; detectable via behavioral patterns and can be disabled.

- **M2M/IoT profiles:** often carved out as exceptions to keep ATMs/terminals running; useful only where access is not tightly segmented to specific hosts.

- **Conclusion:** restrictions are easy to bypass, keeping channels open for attacks (DDoS, botnet control, drone control).

- **Attacks via whitelisted channels:** gRPC/HTTP/2 multiplexing lets command/control data hide inside permitted flows, complicating filtering and detection.

---

## 2. The "Whitelist" is a Leaky Filter

**What it is:** a list of allowed domains and services.

**Vulnerabilities:**
- **TLS/QUIC:** traffic is encrypted; DPI sees only the domain (SNI), not the payload.
- **CDN:** one allowed CDN domain equals thousands of paths/endpoints for data transfer.
- **DoH/DoT:** DNS queries can be hidden inside allowed domains.
- **Semantic tunneling:** data inside images, videos, text.
- **Steganography and push notifications:** data can be covertly transmitted inside multimedia content or via push mechanisms, bypassing basic filters and DPI.

**Example:** a botnet receives commands through a “comment” field in an allowed taxi service.

---

## 3. CAPTCHA — Control, Not Protection

**What it is:** in this context, “CAPTCHA” is the name of the blocking/unblocking mechanism implemented via an authorization page (a *captive portal*), not necessarily a traditional visual puzzle.

**Vulnerabilities:**
- Ability to automate challenge-solving using modern ML models and public APIs of CAPTCHA providers.
- Reuse of sessions/tokens, which reduces the effectiveness of control.
- Bypass via privileged service accounts and integrations that are designed to skip CAPTCHA.
- If the portal interaction protocol is known, the unlocking flow can be fully automated.

**Conclusion:** the control is weak against automated systems.

---

## 4. Consequences for Users and Business

**What this looks like in practice for an “approved” business:**
- On paper it’s simple — you’re told that if your business is on the whitelist, you’ll operate without issues. 

- In reality, the path looks different: at first everything seems fine, then developers can’t ship because Git or CI/CD is unreachable; dependent APIs and third-party libraries fail; video calls show latency and dropouts. Even if your services are whitelisted, they depend on others that aren’t — every day brings new, unpredictable failures. It’s like having a city pass, but at every intersection someone decides whether to let you through, and sometimes “forgets” you have the pass.

- In addition, small IT businesses face a further setback because they can’t afford or obtain domestic software as replacements for foreign tools. They face a double bind: foreign tools and cloud services become restricted or unstable, while domestic “import-substitution” solutions are often too expensive, incompatible, or lack critical features. The result is a technological gap that reduces competitiveness, limits innovation, and can push them out of key markets.

**Startups, unlike large incumbents, are more sensitive to platform choice. They won’t adopt mandated services for several reasons:**
- Lack of trust in data security and confidentiality.
- **Concerns about hidden surveillance or censorship tooling:** this is not about “having nothing to hide” — it’s about the risk of leakage of trade secrets, source code, client databases, and confidential business data. Even if nothing is “illegal,” competitor or agency access can cause real damage, up to lost contracts and technological setbacks.
- **Limited functionality and weak integration with modern global tech ecosystems:** missing APIs/protocols/cloud integrations break automation, CI/CD, analytics and other core business tooling.
- **Reputational risks in foreign markets when using politically-mandated tools:** partners and investors may avoid products associated with censorship or control, fearing sanctions, blocks, or reputational harm. Even if the product is technically solid, its origin alone can close doors internationally.

### ❌ As a result, such companies will either search for ways to retain access to familiar foreign services or move core infrastructure abroad — further reducing domestic technological sovereignty.

---

**Technical effects:**
- **Higher latency (ping +50–200 ms):** multi-layer DPI processing, additional captive-portal checks, and routing through filtering nodes increase response time for all connections — critical for gaming, e‑commerce, and financial transactions.
- **Jitter — unstable packet delay:** dynamic rule application and session revalidation cause variable inter-packet arrival, breaking real-time audio/video and control systems.
- **Throughput drops:** protocol downgrades (e.g., forced fallback from HTTP/3 or HTTP/2 to HTTP/1.1) and inability to use optimized CDN paths significantly cut effective bandwidth.
- **Content loading errors:** incomplete/inaccurate whitelists block required resources (JS, CSS, API calls), causing partial or total web-app failure.
- **Developer/automation tool outages:** if Git repos, CI/CD systems, or cloud IDEs are outside the whitelist, development and delivery can grind to a halt.
- **Release slippage and downtime:** instability across infrastructure, APIs, and dependencies breaks SLAs and jeopardizes change windows.
- **VoIP, VPN, and online meetings degrade:** unstable links, added latency, and blocked ports cause dropouts and artifacts; some VPN protocols stop working entirely.

---

## 5. Why This Does Not Protect Against Drones and DDoS

**Drones:**
- Use satellite channels, private radio links, and autonomous missions.

**DDoS:**
- Mitigated at the perimeter: scrubbing centers, Anycast, upstream filtering by providers.
- Mass user restrictions do not reduce bot traffic.

---

## 📉 Key Issue

The internet in the 21st century is strategic infrastructure.  
This scheme:
- Does not solve the stated security goals.
- Degrades quality of service.
- Creates prerequisites for full control and segmentation of the Russian internet (Runet).
- Turns mobile internet into a slow and unstable channel, reducing the efficiency of the economy, public administration, and communications.