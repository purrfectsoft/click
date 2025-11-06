# **🖱️ Product Requirements Document (PRD) — Project “Click!”**

**Code:** #click  
**Version:** 1.2 (Lean Workflow Update)  
**Prepared by:** Arafat Zahan  
**Planet:** Purrfect Software Limited  
**Status:** Final for Implementation Approval  

---

## **🌌 1. Vision & Philosophy**

**Click!** is the **Purrfect Universe’s open-source alternative** to traditional link-management, QR, and sharing tools — built on the foundation of **privacy, transparency, and empowerment**.  

**Philosophy:** *You shouldn’t have to trade privacy for insight, or simplicity for power.*

Click! enables creators, teams, and communities to share responsibly — without dark patterns, vendor lock-ins, or data harvesting.

---

## **🧩 2. Core Functional Pillars**

| Pillar | Purpose | Example |
|:--|:--|:--|
| **Shorten** | Create privacy-respecting short URLs | `https://click.purrfecthq.com/mm-job` |
| **Track** | Build ethical tracking URLs with clear lineage | Campaign UTM builder (`source=qr`, `origin=poster`, etc.) |
| **Generate** | Create branded, parametric QR codes | For recruitment posters or cards |
| **Share** | Post text or notes (public, private, expirable) | Quick snippets or messages |
| **Send** | Securely transfer files (encrypted & expirable) | “Click to send securely — no trace left behind.” |

---

## **🧱 3. MVP Scope — *Seed 1 (Minimum Lovable Product)***

### **A. Unified App — Expo Universal App Workflow**

**Framework:** [Expo Universal App](https://expo.dev)  
A single codebase for **iOS · Android · Web**, powered by Expo’s new **Router API Routes** for lightweight backend capabilities.  

**UI Framework:** [Tamagui](https://tamagui.dev) (lockdown) — ensures shared design tokens and component parity across mobile and web.

**Seed 1 Features**
- URL Shortener  
- Tracking URL Builder  
- QR Generator (live preview)  
- Text Sharer (public / private / expirable)  
- Secure File Sender (*may extend post-MVP*)  
- No login required (initial release) — Golden Identity (PU SSO) planned for Seed 2

---

### **B. Privacy & Security**

- No cookies or third-party trackers  
- Anonymous analytics only (timestamp + medium)  
- Expirable data with automatic cleanup  
- Client-side AES encryption for file sender  
- Fully auditable and open source  

---

### **C. Branding & Experience**

**Colors**
- 🟠 Purrfect Orange `#d2691e`  
- 🔵 Universe Blue `#1f77b4`  
- 🟢 Motion Green `#228b22`

**Logo:** “CLICK!” wordmark inside the infinity pawprint  
**Mascot:** Curious orange kitten paw tapping a glowing link icon  
**Tone:** Friendly, transparent, empowering  
> “Your link has been Purrfectly shortened 🐾”

---

## **🧠 4. Architecture Overview (Conceptual)**

| Layer | Description |
|:--|:--|
| **App Client** | Built entirely in Expo Universal App with React Native and Tamagui UI. |
| **API Routes** | Lightweight backend powered by [Expo Router API Routes](https://docs.expo.dev/router/reference/api-routes/). Handles link shortening, QR generation, text sharing, and minimal analytics. |
| **Storage** | Temporary in-memory or local persistence (to be finalized in Design Doc). |
| **Infra Notes** | Deployable via Expo Hosting / Vercel. Package manager → **yarn**. |

> *Full backend persistence, database schema, and infra will be defined in the Design Document phase.*

---

## **🚀 5. Roadmap**

| Phase | Focus | Key Deliverables |
|:--|:--|:--|
| **Seed 1** | MVP Launch | Core features + internal PU use |
| **Seed 2** | Expansion | Golden Identity (SSO) · Analytics Dashboard |
| **Seed 3** | Ecosystem | Custom domains · CLI · Browser extension |
| **Seed 4** | Scale | Public open-source community and external adoption |

---

## **📊 6. Metrics of Success**

| Metric | Target |
|:--|:--|
| PU adoption rate | 100% internal usage for QR and tracking |
| Open-source stars | 500 + within 6 months |
| Privacy score | 100% (no personal data retained) |
| Uptime | ≥ 99.9% |
| Average link creation time | < 250 ms |

---

## **🧭 7. Open Questions**

1. Redirect domain — `c.purrfecthq.com/:hash` (API route redirect) vs main Expo web?  
2. Encryption model — full client-side (default) vs server-assisted?  
3. Storage — local vs Supabase / Cloudflare KV?

---

## **🪐 8. Next Steps**

**Immediate**
1. Approve PRD v1.2 (Lean) for implementation  
2. Create GitHub repo → `purrfectsoft/click`  
3. Write public README (*“Hello World of Click!”*)  
4. Initialize Expo Universal App scaffold with Tamagui  

**Parallel**
- Design Figma mockups (UI + logo + brand)  
- Pilot integration → Motion Mechanics QR campaign  

---

## **✨ Summary**

**Click!** will be the **Purrfect Universe’s digital sharing core** — combining link shortening, tracking, QR generation, text sharing, and secure file sending into one ethical and beautiful experience.  

**Shorten. Share. Track. Privately.**
