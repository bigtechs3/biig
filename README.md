# 📱 BIGST4CK WiFi – Customer Journey

This document explains the complete experience of a customer using the **BIGST4CK WiFi Hotspot** system.

---

## 🔄 Overview

The customer connects to Wi-Fi, verifies their identity via OTP, selects a package, pays via SonicPesa, and gets instant internet access – all without typing any username or password.

---

## 📋 Step-by-Step Customer Journey

### Step 1: Connect to Wi-Fi

| Action | What the Customer Sees |
|--------|------------------------|
| Opens Wi-Fi settings on phone | Sees available networks |
| Selects **"BIGST4CK WiFi"** | Taps **"Connect"** |
| (If password is set) Enters Wi-Fi password | `BIGST4CK@2026` |

> ✅ **Connected to Wi-Fi, but NO internet access yet.**

---

### Step 2: Captive Portal Opens Automatically

| Action | What the Customer Sees |
|--------|------------------------|
| Phone detects no internet | Browser opens automatically |
| Redirected to the portal page | Welcome screen appears |

```
┌─────────────────────────────────┐
│  📶 BIGST4CK WiFi               │
│                                 │
│  Karibu! Weka namba yako ya     │
│  simu kuanza.                   │
│                                 │
│  ┌──────────────────────────┐  │
│  │ 255_______________       │  │
│  └──────────────────────────┘  │
│                                 │
│  [ 🔐 Tuma Msimbo ]             │
└─────────────────────────────────┘
```

---

### Step 3: Enter Phone Number

| Action | What the Customer Sees |
|--------|------------------------|
| Types phone number | `255705517165` |
| Taps **"Tuma Msimbo"** | "Sending code..." message appears |

> ✅ **OTP request sent to the backend.**

---

### Step 4: Receive OTP via WhatsApp

| Action | What the Customer Sees |
|--------|------------------------|
| Check WhatsApp | Receives message from BIGST4CK bot |

```
🔐 *BIGST4CK WiFi*

Msimbo wako wa kuthibitisha:

*4821*

Msimbo huu ni halali kwa dakika 5 tu.
Usimshirikishe mtu yeyote.

© BIGST4CK
```

> ✅ **OTP delivered within 2–5 seconds.**

---

### Step 5: Enter OTP

| Action | What the Customer Sees |
|--------|------------------------|
| Enters 6‑digit code | `4 8 2 1 _ _` |
| Taps **"Thibitisha"** | Code is verified |

```
┌─────────────────────────────────┐
│  📶 BIGST4CK WiFi               │
│                                 │
│  Weka msimbo wa tarakimu 6:     │
│                                 │
│  ┌──────────────────────────┐  │
│  │ 4 8 2 1 3 7              │  │
│  └──────────────────────────┘  │
│                                 │
│  [ ✅ Thibitisha ]               │
└─────────────────────────────────┘
```

> ✅ **OTP verified – customer moves to package selection.**

---

### Step 6: Select Package

| Action | What the Customer Sees |
|--------|------------------------|
| Views available packages | List of plans with prices |
| Selects desired package | Taps on the chosen plan |

```
┌─────────────────────────────────┐
│  📶 BIGST4CK WiFi               │
│                                 │
│  Chagua pakiti yako:            │
│                                 │
│  ┌──────────────────────────┐  │
│  │ 🕐 Saa 1   – 500 TZS     │  │
│  ├──────────────────────────┤  │
│  │ 🕒 Saa 3   – 1,000 TZS   │  │
│  ├──────────────────────────┤  │
│  │ 🕕 Saa 6   – 1,500 TZS   │  │
│  ├──────────────────────────┤  │
│  │ 🕛 Saa 12  – 2,500 TZS   │  │
│  ├──────────────────────────┤  │
│  │ 🕐 Saa 24  – 4,000 TZS   │  │
│  └──────────────────────────┘  │
└─────────────────────────────────┘
```

> ✅ **Package selected – payment process begins.**

---

### Step 7: Pay via SonicPesa

| Action | What the Customer Sees |
|--------|------------------------|
| Payment is initiated | "Processing payment..." message |
| Phone receives USSD prompt | USSD screen opens automatically |
| Enters PIN to confirm | Authorizes the payment |

```
┌─────────────────────────────────┐
│  📶 BIGST4CK WiFi               │
│                                 │
│  ⏳ Inachakata malipo yako...   │
│                                 │
│  Tafadhali angalia simu yako.   │
│  Utapokea taarifa ya USSD.      │
│                                 │
│  Ingiza PIN yako kuthibitisha.  │
└─────────────────────────────────┘
```

> ✅ **Payment processed within 10–25 seconds.**

---

### Step 8: Internet Access Granted

| Action | What the Customer Sees |
|--------|------------------------|
| Payment is confirmed | Success screen appears |
| Internet is activated | Browsing works immediately |

```
┌─────────────────────────────────┐
│  📶 BIGST4CK WiFi               │
│                                 │
│  🎉 *UMEFANIKIWA!* 🎉           │
│                                 │
│  Umeunganishwa kwenye intaneti!  │
│                                 │
│  ⏱️ Muda: Saa 6                 │
│  ⏳ Inaisha: 20:00              │
│                                 │
│  🌐 Furahia kutumia intaneti!    │
└─────────────────────────────────┘
```

> ✅ **Customer can now browse, stream, and download.**

---

### Step 9: Session Expiry (Automatic)

| Action | What the Customer Sees |
|--------|------------------------|
| Time purchased expires | MikroTik automatically disconnects |
| Customer tries to browse | Redirected to Captive Portal |

```
┌─────────────────────────────────┐
│  📶 BIGST4CK WiFi               │
│                                 │
│  ⏰ Muda wako umekwisha!         │
│                                 │
│  Nunua pakiti tena kuendelea.   │
│                                 │
│  [ 🛒 Nunua Sasa ]               │
└─────────────────────────────────┘
```

> ✅ **Customer can purchase another package to continue.**

---

## 📊 Summary Table

| Step | Customer Action | System Action | Time |
|------|-----------------|---------------|------|
| 1 | Connects to Wi-Fi | Grants Wi-Fi connection | < 5s |
| 2 | Sees Captive Portal | Redirects to portal | < 2s |
| 3 | Enters phone number | Sends OTP request | < 2s |
| 4 | Receives OTP | Sends WhatsApp message | 2–5s |
| 5 | Enters OTP | Verifies and authenticates | < 2s |
| 6 | Selects package | Prepares payment | < 2s |
| 7 | Pays via USSD | Processes payment | 10–25s |
| 8 | Gets internet access | Creates MikroTik user | < 2s |
| 9 | Session expires | Disconnects automatically | On expiry |

---

## 🎯 Key Points

| Question | Answer |
|----------|--------|
| **Does customer need a username/password?** | ❌ **NO** – only phone number and OTP |
| **Does internet work immediately after payment?** | ✅ **YES** – within 2–5 seconds |
| **Is the customer disconnected automatically?** | ✅ **YES** – when time expires |
| **Can the customer reuse the same OTP?** | ❌ **NO** – OTP is one‑time and expires in 5 minutes |
| **Does the customer need to reconnect to Wi-Fi?** | ❌ **NO** – stays connected, just loses internet access |

---

## 📌 Legend

| Icon | Meaning |
|------|---------|
| 📶 | Wi‑Fi connection |
| 🔐 | Security / Authentication |
| 💳 | Payment |
| ✅ | Success |
| ⏰ | Time / Expiry |
| 🌐 | Internet access |

---

**© 2026 BIGST4CK by bigmanjtech™**