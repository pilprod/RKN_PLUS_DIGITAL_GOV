# Analysis of the "CAPTCHA + DPI + Whitelist" Scheme in Mobile Networks

## 1. Attack vector changes but does not disappear
- Restricting access to "foreign" SIM cards via a 5-hour wait is easy to bypass via:
  - "Dead souls" — SIM cards registered to people who do not use them.
  - SIM cards of Russians living abroad.
  - Corporate APN/MPLS channels.
  - M2M devices with permanent connectivity.
- Infrastructure attacks (DDoS, botnets, drone control) can still be carried out via **legitimate channels**, including whitelisted services.

## 2. "Whitelist" = porous filter
- To bypass, you only need **one allowed service** capable of tunneling traffic (API, uploaded content).
- Known examples:
  - CDN.
  - Marketplaces.
  - Maps and taxi services.
- These platforms have already shown they can be used as data transport channels.

## 3. CAPTCHA as authentication
- CAPTCHA in mobile networks ≈ extra step in **captive portal** access.
- Useful **for controlling the user**, but **not for stopping automation**.
- For a DDoS bot or automated system, it is enough to:
  - Pass the CAPTCHA manually once.
  - Solve it automatically (modern ML models can solve most CAPTCHAs).

## 4. Real consequences for citizens
- Reduced speed and increased latency due to multi-layer DPI/firewall filtering.
- In regions: "internet like via satellite in the 90s":
  - High ping.
  - Connection drops.
  - Unstable VoIP and VPN.
- Work tools and services outside the whitelist become unavailable:
  - Freelancers.
  - Remote workers.
  - Developers.
  - System administrators.

## 5. Zero value for drone defense
- Drone control can be done via:
  - Satellite link.
  - Whitelisted services.
  - M2M.
  - Preloaded scripts.
- DDoS protection should be handled:
  - At the network perimeter (scrubbing centers).
  - Not via mass user restrictions.

---

# Possible reasons for implementation (even knowing it won't stop drones/DDoS)

## 1. Centralized traffic control
- DPI and whitelisting allow the entire country to be switched to "restricted mode" **in one click**.
- Operators will already have ready configs and filters.

## 2. Total identification
- Every internet access:
  - Via SIM tied to passport.
  - Via CAPTCHA authentication (potentially linked to government services).
- Removes "anonymous" users from the mobile network.

## 3. Political tool
- In case of:
  - Protests.
  - Rallies.
  - Mass actions.
- Can leave access only to "approved" resources:
  - Marketplaces.
  - Taxi.
  - Government services.
- Social networks, messengers, VPNs — blocked instantly.

## 4. Financial interest
- Possibility to sell access to "full internet":
  - Via "approved" VPNs or proxies.
- Operators can optimize networks for lower traffic volumes.

## 5. Preparation for Runet segmentation
- Foundation for an isolated mode where all external traffic goes only through **government gateways**.
- "Training" users to live in partial-block mode.
