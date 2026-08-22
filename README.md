# biig



# 📁 Wi-Fi Hotspot Billing System – Project Structure

```
wifi-billing-system/
│
├── 📂 src/
│   ├── 📂 config/
│   │   └── database.js          # Database connection (PostgreSQL/MySQL)
│   │
│   ├── 📂 controllers/
│   │   ├── portalController.js  # Captive Portal – show packages, handle selection
│   │   ├── paymentController.js # Payment webhook – verify & process payments
│   │   └── mikrotikController.js# MikroTik API – add/remove hotspot users
│   │
│   ├── 📂 models/
│   │   ├── Package.js           # Package schema (name, duration, price)
│   │   ├── Customer.js          # Customer schema (MAC, phone, email)
│   │   ├── Session.js           # Session schema (start, end, status)
│   │   └── Payment.js           # Payment schema (amount, status, reference)
│   │
│   ├── 📂 routes/
│   │   ├── api.js               # API routes (/api/payment-webhook, /api/session-status)
│   │   └── web.js               # Web routes (/portal, /success, /expired)
│   │
│   ├── 📂 services/
│   │   └── mikrotikService.js   # MikroTik API communication logic
│   │
│   ├── 📂 views/                # EJS/Handlebars templates
│   │   ├── portal.ejs           # Captive Portal page (packages + payment)
│   │   ├── success.ejs          # Payment success page
│   │   └── expired.ejs          # Session expired page
│   │
│   ├── 📂 public/               # Static assets
│   │   ├── 📂 css/
│   │   │   └── style.css        # Main stylesheet
│   │   └── 📂 js/
│   │       └── main.js          # Frontend JavaScript
│   │
│   ├── 📂 utils/
│   │   ├── logger.js            # Logging utility
│   │   └── helpers.js           # Helper functions (time calculation, etc.)
│   │
│   └── app.js                   # Express app entry point
│
├── 📂 database/                 # SQL migrations / seeders
│   └── schema.sql               # Database schema
│
├── 📄 .env                      # Environment variables (NOT committed)
├── 📄 .gitignore                # Git ignore file
├── 📄 package.json              # Node.js dependencies & scripts
├── 📄 README.md                 # Project documentation
└── 📄 render.yaml               # Render.com deployment config (optional)
```



# 🧩 Wi-Fi Hotspot Billing System – Components List

## 🔢 5 MAIN LAYERS

---

### ✅ 1. LOCAL HARDWARE (Mbeya – Physical)

| # | Component | Description |
|---|-----------|-------------|
| 1 | Internet Provider Router/Modem | Brings internet connection into the building. |
| 2 | MikroTik Router (hAP ac2) | The brain of the system. Provides Wi‑Fi, captive portal, user sessions, and automatic disconnection. |
| 3 | Access Point (Optional) | For wider Wi‑Fi coverage. For pilot (10‑15 users), built‑in Wi‑Fi is enough. |
| 4 | Customer Devices | Smartphones, laptops, tablets connecting to the Wi‑Fi. |

---

### ✅ 2. LOCAL NETWORK (Mbeya – MikroTik)

| # | Component | Description |
|---|-----------|-------------|
| 5 | Wi‑Fi SSID | Network name customers see (e.g., "MAC WiFi"). |
| 6 | HotSpot Service | Intercepts unauthenticated users and forces captive portal. |
| 7 | Captive Portal (Redirect) | Redirects users to your external cloud website. |
| 8 | Walled Garden | Allows access to your cloud portal URL before authentication. |
| 9 | HotSpot User Database | Local list of active users with time limits. |

---

### ✅ 3. CLOUD INFRASTRUCTURE (Render.com – Global)

| # | Component | Description |
|---|-----------|-------------|
| 10 | Render Web Service | Hosts your Node.js/PHP application. Provides public URL. |
| 11 | PostgreSQL / MySQL Database | Stores customers, packages, sessions, payments, logs. |
| 12 | Environment Variables (.env) | Stores secrets: MikroTik IP, password, API keys, database URL. |
| 13 | SSL Certificate (HTTPS) | Encrypts all traffic. Provided automatically by Render. |
| 14 | Public URL | The link customers use to access the captive portal. |

---

### ✅ 4. APPLICATION SOFTWARE (Cloud – Your Code)

| # | Component | Description |
|---|-----------|-------------|
| 15 | Captive Portal (Web Page) | Displays time packages (1h, 3h, 6h, 12h, 24h). |
| 16 | Backend API Server | Processes payment confirmations, calculates expiry times. |
| 17 | Payment Webhook Handler | Receives "success" signal from your payment system. |
| 18 | MikroTik API Client | Sends commands to MikroTik (add user, set time limit). |
| 19 | Session Timer / Expiry Logic | Calculates exact end time (e.g., 14:00 + 6h = 20:00). |
| 20 | Admin Dashboard (Optional) | View active sessions, manually manage users. |
| 21 | Logging & Monitoring | Records all transactions, errors, and events. |

---

### ✅ 5. EXTERNAL INTEGRATIONS (Global)

| # | Component | Description |
|---|-----------|-------------|
| 22 | Your Existing Payment System | Sends webhook to your backend when payment succeeds. |
| 23 | Payment Gateway (e.g., SonicPesa) | Processes the customer's money. |
| 24 | Admin Access (Anywhere) | You can manage the system from Dodoma, Mbeya, or abroad. |
| 25 | GitHub Repository | Stores all code. Auto‑deploys to Render. |
| 26 | ISP Internet Connection | Provides internet to the MikroTik. Must allow hotspot/resale for commercial use. |

---

## ✅ TOTAL: 26 COMPONENTS

| Layer | Count |
|-------|-------|
| 1. Local Hardware | 4 |
| 2. Local Network | 5 |
| 3. Cloud Infrastructure | 5 |
| 4. Application Software | 7 |
| 5. External Integrations | 5 |
| **TOTAL** | **26** |

---

## 📌 KEY INTEGRATION POINTS

1. **MikroTik ↔ Cloud Backend** – via RouterOS API (port 8728)
2. **Customer ↔ Captive Portal** – via HTTPS (Render URL)
3. **Payment System ↔ Backend** – via Webhook (POST request)
4. **Backend ↔ Database** – via SQL (PostgreSQL/MySQL)
5. **Admin ↔ Render Dashboard** – via Browser (Anywhere)

---

## 🚀 DEPLOYMENT SUMMARY

| Step | Action |
|------|--------|
| 1 | Push code to GitHub |
| 2 | Connect GitHub to Render.com |
| 3 | Set environment variables |
| 4 | Deploy web service |
| 5 | Configure MikroTik to redirect to Render URL |
| 6 | Test with real customer device |