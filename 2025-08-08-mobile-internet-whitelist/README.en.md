# Analysis of the "CAPTCHA + DPI + Whitelist" Scheme in Mobile Networks

[Source: «В России разработали техническую схему доступа к массовым сервисам при ограничениях», Интерфакс](https://www.interfax.ru/russia/1040184)


## 1. Attack vector changes but does not disappear
- **Dead SIMs** — SIMs registered to inactive people can be handed over.
- **Expat SIMs** — VPN/proxy back into the country.
- **Corporate APN/MPLS** — separate routing, no retail whitelist.
- **M2M devices** — kept online for ATMs, POS terminals; can be abused.
- **Legit C2** — commands hidden in marketplace API or taxi chat.

*Example:* encode commands in `order_comment` field of taxi API.

---

## 2. Whitelist = porous filter
- **Semantic tunneling** — data inside images/videos.
- **CDN blind spots** — thousands of allowed URIs.
- **DoH/DoT inside domain** — DNS over HTTPS hidden in app traffic.
- **Edge computing** — JS/Worker redirect.
- **Sharding** — dynamic subdomains.

*Example:* encrypted `.zip` disguised as `.png` on marketplace CDN.

---

## 3. CAPTCHA as authentication
- **Captive portal** — redirect, token, IMSI in allowed list.
- **Automation** — OCR+ML solvers, token reuse.
- **Privileged bots** — bypass CAPTCHA.
- **UX cost** — false positives.

*Example:* headless browser + 2Captcha solving.

---

## 4. Real consequences for citizens
- **Latency** — +50–200 ms.
- **HTTP/3 issues** — downgraded to HTTP/1.1.
- **False blocks** — apps break.
- **MTU/MSS** — timeouts.
- **Work tool outages** — GitLab, Jira.

*Example:* regional devs lose GitHub Actions access.

---

## 5. Zero value against drones/DDoS
- **Drones** — satellite, radio links, autonomous.
- **DDoS** — handled at perimeter.
- **Botnets** — commands via comments/media.

*Example:* botnet C2 via product comments on whitelisted marketplace.

---

## Motives
1. **Centralized control** — one flag toggles restricted mode.
2. **Total identification** — SIM+ID+fingerprint.
3. **Political tool** — protest-time cutoffs.
4. **Financial** — sell full internet.
5. **Runet segmentation** — user conditioning.