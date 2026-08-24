# 📶 BIGST4CK Wi‑Fi Hotspot Billing System – Requirements Document

---

## 📌 Document Information

| Item | Details |
|------|---------|
| **Project Name** | BIGST4CK Wi‑Fi Hotspot Billing System |
| **Version** | 1.0.1 |
| **Date** | August 2026 |
| **Author** | bigmanjtech™ |
| **Status** | Draft / Planning |
| **Purpose** | Define all requirements for building and deploying the Wi‑Fi hotspot billing system |

---

## 🎯 1. Project Overview

### 1.1 Objective
To build a fully automated, time‑based Wi‑Fi hotspot billing system that allows customers to purchase internet access by the hour, pay via SonicPesa, and get instant activation – all without manual intervention.

### 1.2 Scope
| In Scope | Out of Scope |
|----------|--------------|
| Single‑location hotspot (pilot) | Multi‑location management |
| Time‑based billing (hours) | Data‑based billing (MB/GB) |
| OTP authentication via WhatsApp | SMS authentication |
| SonicPesa payment integration | Other payment gateways (for now) |
| Automated MikroTik user management | Manual voucher generation |
| Captive Portal (custom website) | Default MikroTik login page |
| PostgreSQL database | Other database types |
| Render.com deployment | On‑premise server deployment |
| **Wi‑Fi range extension (5m → 100m)** | **Beyond 100m (for now)** |

### 1.3 Business Goals
- ✅ Sell internet access by the hour
- ✅ Fully automated – no manual intervention
- ✅ Secure – no password sharing
- ✅ Scalable – from 10 to 10,000 users
- ✅ Profitable – low startup cost, fast ROI
- ✅ **Cover a 100m radius outdoor area** (yard, parking lot, etc.)

---

## 👥 2. Stakeholders

| Stakeholder | Role | Responsibility |
|-------------|------|----------------|
| **Owner (You)** | Business Owner | Overall system management, marketing, customer support |
| **Customers** | End Users | Purchase and use internet access |
| **MikroTik** | Hardware Provider | Router and HotSpot functionality |
| **SonicPesa** | Payment Gateway | Process payments via USSD |
| **Render.com** | Hosting Provider | Host website, backend, and database |
| **Outdoor AP Manufacturer** | Hardware Provider | Provide outdoor Wi‑Fi coverage hardware |

---

## 🧑‍💻 3. User Personas

### 3.1 Customer
| Attribute | Description |
|-----------|-------------|
| **Name** | Typical customer |
| **Age** | 18–45 |
| **Tech Savviness** | Medium – can use WhatsApp and Wi‑Fi settings |
| **Device** | Smartphone (Android/iOS) |
| **Payment Method** | Mobile money (Halopesa, M‑Pesa, Airtel, Tigo) |
| **Goal** | Get fast, affordable internet access |
| **Frustration** | Long registration processes, password sharing, complicated logins |

### 3.2 Admin (You)
| Attribute | Description |
|-----------|-------------|
| **Name** | Business Owner / Admin |
| **Tech Savviness** | High – can configure MikroTik and servers |
| **Device** | PC / Laptop / Smartphone |
| **Goal** | Manage system, monitor revenue, troubleshoot issues |
| **Frustration** | Manual user management, lack of visibility, downtime |

---

## ✅ 4. Functional Requirements

### 4.1 Customer Authentication

| ID | Requirement | Priority |
|----|-------------|----------|
| FR‑A01 | Customer must be able to connect to Wi‑Fi without entering a username or password | High |
| FR‑A02 | Customer must be redirected to a custom Captive Portal | High |
| FR‑A03 | Customer must enter their phone number to start the process | High |
| FR‑A04 | System must send a 6‑digit OTP via WhatsApp | High |
| FR‑A05 | OTP must expire after 5 minutes | High |
| FR‑A06 | OTP must be one‑time use only | High |
| FR‑A07 | Customer must enter the OTP to proceed | High |
| FR‑A08 | System must verify the OTP before allowing package selection | High |

### 4.2 Package Selection

| ID | Requirement | Priority |
|----|-------------|----------|
| FR‑P01 | Customer must see a list of available packages | High |
| FR‑P02 | Packages must be time‑based: 1h, 3h, 6h, 12h, 24h | High |
| FR‑P03 | Each package must display price in TZS | High |
| FR‑P04 | Customer must be able to select a package | High |
| FR‑P05 | System must calculate the expiry time based on the selected package | High |

### 4.3 Payment Processing

| ID | Requirement | Priority |
|----|-------------|----------|
| FR‑PM01 | System must initiate payment via SonicPesa | High |
| FR‑PM02 | Customer must receive a USSD prompt on their phone | High |
| FR‑PM03 | System must receive a webhook from SonicPesa when payment is confirmed | High |
| FR‑PM04 | System must verify the webhook signature for security | High |
| FR‑PM05 | Payment status must be stored in the database | High |
| FR‑PM06 | Customer must see a processing screen while waiting for payment confirmation | Medium |

### 4.4 Internet Activation

| ID | Requirement | Priority |
|----|-------------|----------|
| FR‑I01 | System must create a unique user on MikroTik after successful payment | High |
| FR‑I02 | MikroTik user must have a time limit matching the purchased package | High |
| FR‑I03 | Internet access must be granted immediately (within seconds) | High |
| FR‑I04 | MikroTik must automatically disconnect the user when time expires | High |
| FR‑I05 | Customer must see a success page when internet is activated | High |

### 4.5 Session Management

| ID | Requirement | Priority |
|----|-------------|----------|
| FR‑S01 | System must track active sessions | High |
| FR‑S02 | System must track session start and end times | High |
| FR‑S03 | System must store the MikroTik username and password for each session | Medium |
| FR‑S04 | System must allow customers to purchase additional time after expiry | High |
| FR‑S05 | Expired sessions must be automatically closed | High |

### 4.6 Admin Features

| ID | Requirement | Priority |
|----|-------------|----------|
| FR‑AD01 | Admin must be able to view active sessions | Medium |
| FR‑AD02 | Admin must be able to view revenue reports | Medium |
| FR‑AD03 | Admin must be able to manually disconnect a user | Low |
| FR‑AD04 | Admin must be able to view customer history | Low |
| FR‑AD05 | Admin must receive alerts for system errors | Medium |

---

## 🛠️ 5. Technical Requirements

### 5.1 Hardware Requirements

| ID | Requirement | Specification |
|----|-------------|---------------|
| TR‑H01 | Router | MikroTik hAP ac2 (RB962UiGS-5HacT2HnT) |
| TR‑H02 | Router CPU | Dual‑core 720 MHz |
| TR‑H03 | Router RAM | 256 MB |
| TR‑H04 | Router Storage | 128 MB flash |
| TR‑H05 | Wi‑Fi Standard | 802.11ac (2.4GHz + 5GHz) |
| TR‑H06 | Concurrent Users | Minimum 15 users |
| TR‑H07 | Power Supply | 12V 1.5A DC adapter |

### 5.2 Wi‑Fi Range Extension (Outdoor AP)

| ID | Requirement | Specification |
|----|-------------|---------------|
| TR‑WE01 | Outdoor Access Point | Must extend Wi‑Fi coverage from 5m to at least 100m |
| TR‑WE02 | Outdoor AP Weatherproof Rating | IP65 or higher (rain, dust, sun protection) |
| TR‑WE03 | Outdoor AP Standard | 802.11n or 802.11ac (2.4GHz or dual‑band) |
| TR‑WE04 | Ethernet Cable | Cat5e or Cat6, minimum 100m length |
| TR‑WE05 | Power Over Ethernet (PoE) | PoE injector included with AP (or purchased separately) |
| TR‑WE06 | Mounting | Must be mountable on a pole, wall, or roof |
| TR‑WE07 | Cable Protection | Cable must be protected from weather and physical damage |
| TR‑WE08 | Outdoor AP Speed | Minimum 300 Mbps (2.4GHz) |
| TR‑WE09 | Outdoor AP Range | Minimum 100m in open area |
| TR‑WE10 | Customer Devices Supported | Minimum 15 concurrent users on outdoor AP |

**Recommended Outdoor AP Models:**

| Model | Price (TZS) | Features |
|-------|-------------|----------|
| WAVLINK AC1200 Outdoor AP | ~170,000 | IP67, AC1200, PoE, 100m+ range |
| TP‑Link EAP211‑Bridge KIT | ~250,000 | Complete kit, weatherproof, 100m+ range |
| Comfast CF‑EW74 | ~150,000 | High power, IP65, 100m+ range |
| Ubiquiti NanoStation M2 | ~350,000 | Professional grade, 200m+ range |
| MikroTik SXT Lite2 | ~180,000 | MikroTik compatible, 100m+ range |

### 5.3 Software Requirements

| ID | Requirement | Specification |
|----|-------------|---------------|
| TR‑S01 | Operating System | RouterOS v7.x (on MikroTik) |
| TR‑S02 | Backend | Node.js v18+ or v20+ |
| TR‑S03 | Backend Framework | Express.js |
| TR‑S04 | Database | PostgreSQL v14+ or MySQL v8+ |
| TR‑S05 | ORM (Optional) | Prisma, Sequelize, or Knex |
| TR‑S06 | Frontend | HTML5, CSS3, Vanilla JavaScript |
| TR‑S07 | Deployment Platform | Render.com (or Vercel, Heroku) |
| TR‑S08 | Version Control | GitHub |
| TR‑S09 | Package Manager | npm or yarn |

### 5.4 Network Requirements

| ID | Requirement | Specification |
|----|-------------|---------------|
| TR‑N01 | Internet Connection | Stable broadband (minimum 10 Mbps) |
| TR‑N02 | LAN IP Range | 192.168.88.0/24 (default MikroTik) |
| TR‑N03 | Public IP | Dynamic or static (for webhook callbacks) |
| TR‑N04 | DNS | Stable DNS (Google: 8.8.8.8) |
| TR‑N05 | Port Forwarding | Port 80/443 for web server, port 8728 for MikroTik API |
| TR‑N06 | Outdoor AP Connection | Connected via Ethernet cable to MikroTik or main router |

---

## 🏗️ 6. Wi‑Fi Range Extension Setup Requirements

### 6.1 Physical Installation

| ID | Requirement | Priority |
|----|-------------|----------|
| WR‑01 | Outdoor AP must be mounted at least 3–5 meters high | High |
| WR‑02 | Outdoor AP must be pointed toward the customer area | High |
| WR‑03 | Ethernet cable must be secured with cable clips or ties | High |
| WR‑04 | Cable must be protected from sharp edges and weather | High |
| WR‑05 | Outdoor AP must be installed away from obstructions (trees, walls, metal) | High |
| WR‑06 | Outdoor AP must have line‑of‑sight to the customer area | Medium |

### 6.2 Configuration Requirements

| ID | Requirement | Priority |
|----|-------------|----------|
| WR‑C01 | Outdoor AP must be set to Access Point (AP) mode | High |
| WR‑C02 | SSID must match the main network or be a dedicated outdoor network | High |
| WR‑C03 | Wi‑Fi password must be set (WPA2‑PSK) | High |
| WR‑C04 | Channel must be set to 1, 6, or 11 (2.4GHz) to avoid interference | High |
| WR‑C05 | Country must be set to Tanzania (for regulatory compliance) | Medium |
| WR‑C06 | Firmware must be updated to the latest version | Medium |

### 6.3 Performance Requirements

| ID | Requirement | Target |
|----|-------------|--------|
| WR‑P01 | Minimum signal strength at 100m | -70 dBm or higher |
| WR‑P02 | Minimum internet speed at 100m | 10 Mbps download |
| WR‑P03 | Ping latency at 100m | < 50ms |
| WR‑P04 | Concurrent users on outdoor AP | 15–30 users |
| WR‑P05 | Uptime | 99.9% |

---

## 🔐 7. Security Requirements

| ID | Requirement | Priority |
|----|-------------|----------|
| SR‑01 | All sensitive credentials must be stored in environment variables (`.env`) | High |
| SR‑02 | MikroTik API credentials must never be exposed in frontend code | High |
| SR‑03 | SonicPesa webhook must verify the signature (HMAC) | High |
| SR‑04 | All communication must use HTTPS (SSL/TLS) | High |
| SR‑05 | OTP must be one‑time use and expire after 5 minutes | High |
| SR‑06 | Rate limiting must be applied to OTP requests (prevent abuse) | Medium |
| SR‑07 | Session data must be validated server‑side (never trust client) | High |
| SR‑08 | Database queries must be parameterized (prevent SQL injection) | High |
| SR‑09 | Admin endpoints (if any) must be password‑protected | Medium |
| SR‑10 | MikroTik API should be accessible only from the backend server IP | Medium |
| SR‑11 | Outdoor AP Wi‑Fi password must be strong (minimum 8 characters) | High |
| SR‑12 | Guest network should be isolated from internal network | High |

---

## 📦 8. Integration Requirements

### 8.1 MikroTik API

| ID | Requirement | Priority |
|----|-------------|----------|
| IR‑M01 | Backend must connect to MikroTik via RouterOS API (port 8728) | High |
| IR‑M02 | API must support adding a HotSpot user | High |
| IR‑M03 | API must support setting `limit-uptime` for a user | High |
| IR‑M04 | API must support enabling/disabling a user | High |
| IR‑M05 | API must support getting a list of active users | Medium |
| IR‑M06 | API must support removing a user | Medium |

### 8.2 SonicPesa Payment Gateway

| ID | Requirement | Priority |
|----|-------------|----------|
| IR‑S01 | Backend must initiate payment via SonicPesa API | High |
| IR‑S02 | Backend must receive webhook from SonicPesa | High |
| IR‑S03 | Backend must verify webhook signature (HMAC) | High |
| IR‑S04 | Backend must handle payment success and failure gracefully | High |
| IR‑S05 | Backend must store transaction ID for reference | High |
| IR‑S06 | Backend must retry on failed webhook delivery | Medium |

### 8.3 WhatsApp Bot

| ID | Requirement | Priority |
|----|-------------|----------|
| IR‑W01 | System must send OTP via WhatsApp | High |
| IR‑W02 | WhatsApp message must include the 6‑digit OTP | High |
| IR‑W03 | WhatsApp message must include expiry warning (5 minutes) | High |
| IR‑W04 | WhatsApp message must include a disclaimer not to share the code | High |
| IR‑W05 | Backend must handle WhatsApp API failures gracefully | Medium |

### 8.4 Database

| ID | Requirement | Priority |
|----|-------------|----------|
| IR‑D01 | Database must store customer records | High |
| IR‑D02 | Database must store OTP records (phone, code, expires_at, used) | High |
| IR‑D03 | Database must store package definitions | High |
| IR‑D04 | Database must store session records (customer_id, package_id, start, end, active) | High |
| IR‑D05 | Database must store payment records (session_id, amount, status, transaction_id) | High |
| IR‑D06 | Database must support migrations | Medium |

---

## 🎨 9. User Interface Requirements

### 9.1 Captive Portal Pages

| ID | Requirement | Priority |
|----|-------------|----------|
| UI‑01 | Page must be mobile‑responsive | High |
| UI‑02 | Page must match the BIGST4CK brand (dark theme, neon/Matrix styling) | High |
| UI‑03 | Phone input page must be simple (one field + button) | High |
| UI‑04 | OTP input page must be simple (one field + button) | High |
| UI‑05 | Package selection page must display all packages clearly | High |
| UI‑06 | Payment processing page must show a loading spinner | High |
| UI‑07 | Success page must show package details and expiry time | High |
| UI‑08 | Expired page must include a "Buy Again" button | High |
| UI‑09 | All pages must include a footer with the copyright notice | Medium |

### 9.2 Admin Dashboard (Future Enhancement)

| ID | Requirement | Priority |
|----|-------------|----------|
| UI‑A01 | Dashboard must show active sessions count | Low |
| UI‑A02 | Dashboard must show total revenue today/this week/this month | Low |
| UI‑A03 | Dashboard must allow manual user management | Low |
| UI‑A04 | Dashboard must show transaction history | Low |

---

## 📊 10. Performance Requirements

| ID | Requirement | Target |
|----|-------------|--------|
| PR‑01 | OTP delivery time | < 5 seconds |
| PR‑02 | Payment webhook processing | < 2 seconds |
| PR‑03 | MikroTik user creation | < 1 second |
| PR‑04 | Captive Portal page load | < 2 seconds |
| PR‑05 | Concurrent users supported | Minimum 15, scalable to 100+ |
| PR‑06 | Database query response time | < 100ms |
| PR‑07 | Outdoor AP signal strength at 100m | -70 dBm or higher |
| PR‑08 | Outdoor AP speed at 100m | Minimum 10 Mbps |

---

## ⏰ 11. Business Requirements

### 11.1 Pricing Model

| Package | Duration | Price (TZS) | Price (USD) |
|---------|----------|-------------|-------------|
| Bronze | 1 Hour | 500 | ~$0.20 |
| Silver | 3 Hours | 1,000 | ~$0.40 |
| Gold | 6 Hours | 1,500 | ~$0.60 |
| Platinum | 12 Hours | 2,500 | ~$1.00 |
| Diamond | 24 Hours | 4,000 | ~$1.60 |

### 11.2 Revenue Projection

| Scenario | Daily Revenue | Monthly Revenue |
|----------|---------------|-----------------|
| 10 customers/day (avg 1,500 TZS) | 15,000 TZS | 450,000 TZS (~$180) |
| 20 customers/day (avg 1,500 TZS) | 30,000 TZS | 900,000 TZS (~$360) |
| 30 customers/day (avg 1,500 TZS) | 45,000 TZS | 1,350,000 TZS (~$540) |

### 11.3 Cost Breakdown

#### One‑Time Costs

| Item | Cost (TZS) | Cost (USD) |
|------|------------|------------|
| MikroTik hAP ac2 | 250,000 | ~$100 |
| Outdoor AP (WAVLINK AC1200) | 170,000 | ~$68 |
| 100m Ethernet Cable (Cat5e) | 60,000 | ~$24 |
| Cable Clips / Ties / Conduit | 10,000 | ~$4 |
| Router + Cables | 50,000 | ~$20 |
| **Total** | **~540,000 TZS** | **~$216** |

#### Monthly Costs

| Item | Cost (TZS) | Cost (USD) |
|------|------------|------------|
| Internet Connection | 50,000 | ~$20 |
| Render.com Hosting | 0 (free tier) | $0 |
| SonicPesa Fees | Transaction fee (1–3%) | Variable |
| **Total** | **~50,000–100,000 TZS** | **~$20–40** |

**Payback Period:** 15–20 days (at 20 customers/day)

---

## 🗺️ 12. Project Timeline

| Phase | Duration | Activities |
|-------|----------|------------|
| **Phase 1: Planning** | 1 Week | Requirements finalization, hardware procurement, architecture design |
| **Phase 2: Hardware Setup** | 1 Week | Install MikroTik, install Outdoor AP, run 100m cable |
| **Phase 3: Configuration** | 1 Week | MikroTik configuration, Outdoor AP configuration, network testing |
| **Phase 4: Development** | 2 Weeks | Backend API development, frontend pages, integration with SonicPesa & WhatsApp |
| **Phase 5: Testing** | 1 Week | Unit testing, integration testing, user acceptance testing (UAT), range testing |
| **Phase 6: Deployment** | 3 Days | Deploy to Render, configure MikroTik, go live |
| **Total** | **~7 Weeks** | |

---

## 📝 13. Assumptions

| ID | Assumption |
|----|------------|
| AS‑01 | Customer has a WhatsApp account (for OTP delivery) |
| AS‑02 | Customer has a mobile money account (Halopesa, M‑Pesa, etc.) |
| AS‑03 | SonicPesa integration is available and works as documented |
| AS‑04 | MikroTik router is properly configured and connected to the internet |
| AS‑05 | Render.com free tier is sufficient for the pilot project |
| AS‑06 | The internet connection is stable and meets the minimum speed requirements |
| AS‑07 | Customers are within range of the Wi‑Fi signal (100m) |
| AS‑08 | Outdoor AP has a clear line‑of‑sight to the customer area |
| AS‑09 | The 100m Ethernet cable run is physically possible and safe |
| AS‑10 | Weather conditions allow for outdoor AP installation |

---

## ⚠️ 14. Risks and Mitigation

| Risk | Impact | Likelihood | Mitigation |
|------|--------|------------|------------|
| **SonicPesa API downtime** | High | Low | Implement retry logic and fallback manual payment verification |
| **MikroTik failure** | High | Low | Keep a spare MikroTik or have a recovery plan |
| **Internet outage** | High | Medium | Have a backup internet connection (mobile hotspot) |
| **OTP delivery failure** | Medium | Low | Implement SMS fallback (if budget allows) or manual verification |
| **MAC address randomization** | Medium | High | Use phone number + OTP (not MAC address) for authentication |
| **Password sharing** | High | High | Use unique credentials per user (solved by OTP + MikroTik users) |
| **Fraudulent payments** | Medium | Low | Use SonicPesa's secure payment system and verify webhooks |
| **System overload** | Medium | Low | Monitor performance and scale as needed (Render's free tier handles 10–50 users) |
| **Cable damage (weather/physical)** | Medium | Medium | Use protected cable (conduit) and cable clips |
| **Outdoor AP failure** | Medium | Low | Mount AP securely, check weatherproofing, have spare AP on hand |
| **Signal interference** | Medium | Low | Choose proper channel (1, 6, or 11), avoid obstructions |
| **Range not reaching 100m** | Medium | Medium | Test thoroughly, adjust placement, consider higher‑gain AP |

---

## ✅ 15. Success Criteria

| Criterion | Metric |
|-----------|--------|
| **Customer authentication** | 100% of customers can authenticate via OTP |
| **Payment processing** | 100% of payments are processed correctly via SonicPesa |
| **Internet activation** | 100% of successful payments result in internet access within 5 seconds |
| **Automatic expiry** | 100% of sessions expire on time |
| **Customer satisfaction** | 90% of customers can connect without assistance |
| **Revenue** | Revenue exceeds operating costs within the first month |
| **Wi‑Fi range** | Wi‑Fi signal reaches 100m with -70 dBm or higher |
| **Wi‑Fi speed** | Minimum 10 Mbps at 100m distance |
| **Concurrent users** | Supports 15 concurrent users on outdoor AP |

---

## 📦 16. Deliverables

| Deliverable | Format |
|-------------|--------|
| Captive Portal Website | HTML, CSS, JS (deployed on Render) |
| Backend API | Node.js + Express (deployed on Render) |
| Database | PostgreSQL (on Render or Supabase) |
| MikroTik Configuration | RouterOS scripts and configuration |
| Outdoor AP Configuration | AP configuration settings |
| Network Diagram | Physical layout of router, cable, AP |
| Documentation | README.md, API Reference, Deployment Guide, Setup Guide |
| Source Code | GitHub repository |
| Deployment | Render.com live URL |

---

## 🧰 17. Tools and Resources

| Tool | Purpose |
|------|---------|
| **VS Code** | Code editor |
| **Git** | Version control |
| **GitHub** | Repository hosting |
| **Render.com** | Hosting (backend + frontend + database) |
| **Postman** | API testing |
| **MikroTik WinBox** | MikroTik configuration |
| **SonicPesa Dashboard** | Payment configuration and monitoring |
| **WhatsApp Business API** | OTP delivery (via bot) |
| **Wi‑Fi Analyzer** | Check signal strength and channel interference |
| **Cable Tester** | Test Ethernet cable connectivity |
| **Speedtest** | Test internet speed at 100m |

---

## 📌 18. Glossary

| Term | Definition |
|------|------------|
| **OTP** | One‑Time Password – a 6‑digit code sent via WhatsApp for authentication |
| **Captive Portal** | A web page that intercepts unauthenticated users and forces them to authenticate before getting internet access |
| **HotSpot** | A MikroTik feature that provides authentication and accounting for wireless users |
| **MikroTik** | A Latvian company that manufactures routers and wireless equipment with RouterOS |
| **RouterOS** | The operating system running on MikroTik routers |
| **SonicPesa** | A Tanzanian payment gateway that supports mobile money via USSD |
| **USSD** | Unstructured Supplementary Service Data – a protocol used by mobile networks for real‑time communication (e.g., mobile money payments) |
| **Webhook** | An HTTP callback that one system sends to another when an event occurs (e.g., payment confirmation) |
| **RADIUS** | Remote Authentication Dial‑In User Service – a protocol for centralized authentication, authorization, and accounting (not used in this MVP) |
| **limit-uptime** | A MikroTik HotSpot user parameter that defines the maximum time a user can be connected |
| **Access Point (AP)** | A device that creates a Wi‑Fi network |
| **Outdoor AP** | A weatherproof Access Point designed for outdoor use |
| **PoE (Power over Ethernet)** | A technology that sends power and data through the same Ethernet cable |
| **IP65 / IP67** | Ingress Protection ratings – IP65 is dust‑tight and water‑resistant; IP67 is dust‑tight and waterproof (immersion) |
| **SSID** | Service Set Identifier – the name of a Wi‑Fi network |
| **WPA2‑PSK** | Wi‑Fi Protected Access 2 – Pre‑Shared Key – a common Wi‑Fi security standard |

---

## ✅ 19. Approval

| Role | Name | Signature | Date |
|------|------|-----------|------|
| **Owner / Creator** | bigtechs2 (bigmanjtech™) | | |
| **Developer** | bigtechs2 | | |
| **Tester** | bigtechs2 | | |

---

**© 2026 BIGST4CK by bigmanjtech™**

---

*"Code. Build. Inspire."*