# 📶 BIGST4CK Wi‑Fi Hotspot Billing System

## 🎯 Overview

BIGST4CK is a complete, turnkey solution for selling **time‑based Wi‑Fi access** in small businesses, cafes, hotels, and public spaces. Customers connect to Wi‑Fi, authenticate via OTP, select a package, pay through SonicPesa, and get instant internet access – **all without typing a username or password.**

---

## 🧠 The Problem We Solve

| Issue | Our Solution |
|-------|--------------|
| ❌ Password sharing (one person pays, 10 people use it) | ✅ Unique credentials per customer |
| ❌ Manual user management | ✅ Fully automated (MikroTik + backend) |
| ❌ No expiry tracking | ✅ Automatic disconnection when time expires |
| ❌ Hard to scale | ✅ Built for 10 to 10,000 users |
| ❌ Complicated for customers | ✅ Just phone number + OTP + payment |

---

## 🏗️ System Architecture
```

┌─────────────────────────────────────────────────────────────────────────────┐
│                           BIGST4CK SYSTEM                                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ┌─────────────┐     ┌─────────────┐     ┌─────────────┐                  │
│  │   Customer  │────▶│  MikroTik   │────▶│   Portal    │                  │
│  │   (Phone)   │     │   Router    │     │  (Website)  │                  │
│  └─────────────┘     └─────────────┘     └─────────────┘                  │
│                           │                      │                         │
│                           ▼                      ▼                         │
│                    ┌─────────────┐     ┌─────────────┐                     │
│                    │  Backend    │◀────│   Payment   │                     │
│                    │  (Node.js)  │     │  SonicPesa  │                     │
│                    └─────────────┘     └─────────────┘                     │
│                           │                      │                         │
│                           ▼                      │                         │
│                    ┌─────────────┐               │                         │
│                    │  Database   │               │                         │
│                    │ PostgreSQL  │               │                         │
│                    └─────────────┘               │                         │
│                                                  │                         │
│                    ┌─────────────┐               │                         │
│                    │  WhatsApp   │               │                         │
│                    │  Bot (OTP)  │               │                         │
│                    └─────────────┘               │                         │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

```

---

## 🔧 Technology Stack

| Layer | Technology | Purpose |
|-------|------------|---------|
| **Frontend** | HTML5, CSS3, Vanilla JS | Captive Portal pages |
| **Backend** | Node.js + Express.js | API, OTP, payment, MikroTik logic |
| **Database** | PostgreSQL | Stores customers, sessions, payments |
| **Router** | MikroTik (hAP ac2) | Wi‑Fi, HotSpot, user management |
| **Payment** | SonicPesa | USSD payment processing |
| **OTP Delivery** | WhatsApp Bot | Send verification codes |
| **Hosting** | Render.com | Cloud hosting (free tier available) |

---

## 📱 Customer Journey (Full Flow)

### Step 1: Connect to Wi‑Fi
Customer opens Wi‑Fi settings → selects **"BIGST4CK WiFi"** → connects.

### Step 2: Captive Portal Opens
Phone automatically opens the portal page asking for a phone number.

### Step 3: Enter Phone Number
Customer types their number (e.g., `255705517165`) and taps **"Send Code"**.

### Step 4: Receive OTP
WhatsApp bot sends a 6‑digit code: `4821` (valid for 5 minutes).

### Step 5: Enter OTP
Customer enters the code on the portal and taps **"Verify"**.

### Step 6: Select Package
Customer chooses a package:

| Package | Price (TZS) |
|---------|-------------|
| 1 Hour  | 500 |
| 3 Hours | 1,000 |
| 6 Hours | 1,500 |
| 12 Hours| 2,500 |
| 24 Hours| 4,000 |

### Step 7: Pay via SonicPesa
Customer receives a USSD prompt on their phone and enters their PIN to complete payment.

### Step 8: Internet Access (Instant!)
Backend creates a unique user on MikroTik with the purchased time limit – **internet works immediately!**

### Step 9: Session Expires
When time runs out, MikroTik automatically disconnects the customer. They can buy more time by repeating the process.

---

## 🔄 Technical Flow (Behind the Scenes)

| Step | Action | Who Does It |
|------|--------|-------------|
| 1 | Customer connects to Wi‑Fi | Customer |
| 2 | MikroTik redirects to portal | MikroTik |
| 3 | Customer enters phone number | Customer |
| 4 | Backend generates OTP and sends via WhatsApp | Backend + WhatsApp Bot |
| 5 | Customer enters OTP | Customer |
| 6 | Backend verifies OTP | Backend |
| 7 | Customer selects package | Customer |
| 8 | Customer pays via USSD | Customer + SonicPesa |
| 9 | SonicPesa sends webhook | SonicPesa |
| 10 | Backend creates MikroTik user | Backend + MikroTik API |
| 11 | MikroTik grants internet access | MikroTik |
| 12 | MikroTik disconnects after time expires | MikroTik |

---

## 🔐 Security Features

| Feature | How It Works |
|---------|--------------|
| **OTP** | 6‑digit code, expires in 5 minutes, one‑time use |
| **Unique Credentials** | Each payment creates a unique MikroTik user |
| **No Sharing** | Credentials are tied to the customer's phone number |
| **Automatic Expiry** | MikroTik's `limit-uptime` disconnects automatically |
| **No MAC Address Dependency** | Uses phone number as primary identifier (handles MAC randomization) |

---

## 📁 Database Schema

### `customers`
| Column | Type | Description |
|--------|------|-------------|
| `id` | SERIAL | Primary key |
| `phone` | VARCHAR(15) | Unique phone number |
| `created_at` | TIMESTAMP | Registration time |

### `otps`
| Column | Type | Description |
|--------|------|-------------|
| `id` | SERIAL | Primary key |
| `phone` | VARCHAR(15) | Phone number linked to this OTP |
| `code` | VARCHAR(6) | 6‑digit code |
| `expires_at` | TIMESTAMP | Expiry time (5 minutes) |
| `used` | BOOLEAN | Whether the code has been used |

### `packages`
| Column | Type | Description |
|--------|------|-------------|
| `id` | SERIAL | Primary key |
| `name` | VARCHAR(50) | e.g., "1 Hour" |
| `duration_hours` | INTEGER | 1, 3, 6, 12, 24 |
| `price` | DECIMAL(10,2) | Price in TZS |

### `sessions`
| Column | Type | Description |
|--------|------|-------------|
| `id` | SERIAL | Primary key |
| `customer_id` | INTEGER | Foreign key to customers |
| `package_id` | INTEGER | Foreign key to packages |
| `start_time` | TIMESTAMP | When the session started |
| `end_time` | TIMESTAMP | When the session expires |
| `active` | BOOLEAN | Whether the session is active |
| `mikrotik_username` | VARCHAR(50) | Username created on MikroTik |
| `mikrotik_password` | VARCHAR(50) | Password for logging |

### `payments`
| Column | Type | Description |
|--------|------|-------------|
| `id` | SERIAL | Primary key |
| `session_id` | INTEGER | Foreign key to sessions |
| `amount` | DECIMAL(10,2) | Amount paid |
| `status` | VARCHAR(20) | `PENDING`, `SUCCESS`, `FAILED` |
| `transaction_id` | VARCHAR(100) | SonicPesa transaction reference |
| `created_at` | TIMESTAMP | Payment initiation time |
| `confirmed_at` | TIMESTAMP | When payment was confirmed |

---

## 🛠️ MikroTik Setup (Quick Reference)

```bash
# Enable HotSpot
/ip hotspot setup

# Create HotSpot user (done automatically by backend)
/ip hotspot user add name=customer_255705517165 password=X9kL2mPq limit-uptime=6h

# Set HotSpot profile to redirect to external portal
/ip hotspot profile set [find] login-by=http-chap

# Enable API
/ip service enable api
/ip service set api port=8728

# Add portal URL to walled garden
/ip hotspot walled-garden ip add dst-address=YOUR_RENDER_IP