# 🛡️ GigShield — AI-Powered Parametric Income Insurance for Food Delivery Partners

> **Guidewire DEVTrails 2026 | University Hackathon Submission**
> Protecting the livelihoods of Zomato & Swiggy delivery partners from uncontrollable external disruptions.

---

## 📌 The Problem

India's food delivery partners (Zomato, Swiggy) earn ₹15,000–₹25,000/month working outdoors on two-wheelers. When external disruptions like heavy rain, dense fog, or civil unrest hit, platforms reduce order availability or workers are forced to stop — causing **20–30% income loss in a single week** with zero financial safety net.

**GigShield** solves this with a parametric insurance model: no claim forms, no waiting — just automatic payouts when verified disruptions cross defined thresholds.

---

## 👤 Persona: Food Delivery Partner (Zomato / Swiggy)

### User Profile
- **Name:** Raju, 26 | Operates in Chennai (Anna Nagar + Velachery Zone)
- **Avg weekly earnings:** ₹4,000–₹6,000
- **Working hours:** 10 AM – 10 PM, ~6 days/week
- **Tech comfort:** Moderate — uses smartphone daily for delivery app
- **Pain point:** No savings buffer; one bad week = skipped EMI or missed rent

### Persona-Based Scenarios

| Scenario | Disruption | Impact | GigShield Response |
|---|---|---|---|
| Mumbai monsoon week | Rainfall > 50mm/day for 3+ hours | Orders drop 70%, can't ride safely | Auto-trigger: ₹500–₹1,200 payout |
| Delhi winter fog | Visibility < 50m for 4+ hours | Night deliveries impossible | Auto-trigger: ₹300–₹800 payout |
| City bandh / protest | Verified civil disruption in worker's zone | Pickup/drop zones blocked | Auto-trigger: ₹400–₹1,000 payout |

---

## ⚙️ Application Workflow

```
[Worker Onboarding]
        │
        ▼
[Risk Profile Created] ← City, Zone, Avg. Weekly Earnings, Work Hours
        │
        ▼
[Weekly Policy Purchased] ← Dynamic premium shown, UPI payment
        │
        ▼
[Real-Time Monitoring] ← Weather API + News/Alert API polling every 30 min
        │
        ▼
[Disruption Detected] ← Threshold crossed in worker's registered zone
        │
        ▼
[Fraud Check] ← Location validation + anomaly scoring
        │
        ▼
[Claim Auto-Approved] ← Zero manual steps for worker
        │
        ▼
[Instant Payout] ← UPI / wallet transfer within minutes
        │
        ▼
[Worker Dashboard Updated] ← Earnings protected, claim history shown
```

---

## 🌧️ Parametric Triggers

GigShield covers **income loss only** — no health, vehicle, or accident coverage.

### Trigger 1: Heavy Rain / Floods
- **Data Source:** OpenWeatherMap API (free tier)
- **Threshold:** Rainfall ≥ 40mm in a 3-hour window OR IMD red/orange alert in worker's city
- **Payout Logic:** ₹500 base + ₹100 per additional disrupted hour (capped at ₹1,200/day)

### Trigger 2: Extreme Heat
- **Data Source:** OpenWeatherMap temperature field
- **Threshold:** Temperature > 42°C sustained for ≥ 3 hours between 10 AM–4 PM
- **Payout Logic:** ₹300 base + ₹75 per disrupted hour (capped at ₹800/day)

### Trigger 3: Civil Disruption (Protest / Bandh / Curfew)
- **Data Source:** GDELT Project API + NewsAPI + Twitter/X disaster monitoring feeds
- **Threshold:** Verified bandh/curfew notice OR 3+ credible news sources reporting civil disruption in worker's registered zone within 1 hour
- **Payout Logic:** ₹400 flat per disrupted half-day (max ₹1,000/day)

> ⚠️ **Note:** All triggers are verified against the worker's **registered GPS zone** at policy activation time. Claims filed outside the zone are flagged for review.

---

## 💰 Weekly Premium Model

Gig workers operate and earn on a **week-to-week cycle**, so GigShield is priced weekly — not monthly or annually.

### Base Weekly Premium Tiers

> **Pricing Rationale:** An average Chennai food delivery partner earns ₹4,000–₹6,000/week. Industry best practice keeps insurance premium under 1–1.5% of insured income — making ₹29–₹79/week both affordable and actuarially viable.

| Plan | Weekly Premium | Max Weekly Payout | Best For |
|---|---|---|---|
| **Basic Shield** | ₹29/week | ₹1,500 | Part-time workers (<30 hrs/week) |
| **Standard Shield** | ₹49/week | ₹3,000 | Full-time workers |
| **Pro Shield** | ₹79/week | ₹5,000 | High-earning / peak-season workers |

### AI-Driven Dynamic Pricing Adjustments

The base premium is adjusted weekly using ML risk factors:

| Risk Factor | Adjustment |
|---|---|
| Zone historically flood-prone (e.g., low-lying areas) | +₹5–₹15/week |
| Worker's city has IMD pre-season warning | +₹10/week |
| Worker's zone historically low disruption | −₹5/week |
| Worker has 0 claims in last 4 weeks | −₹3/week (loyalty discount) |
| Predicted rain probability next 7 days > 70% | +₹8/week |

> Premium is recalculated and shown to the worker every Sunday before the new week begins. Worker must actively renew — no auto-debit surprise charges.

---

## 🤖 AI/ML Integration Plan

### 1. Dynamic Premium Calculation (Risk Scoring Engine)
- **Model:** Gradient Boosted Trees (XGBoost / LightGBM)
- **Inputs:** Zone flood history, AQI trends, seasonal weather patterns, worker's claim history, city-level disruption frequency
- **Output:** Risk score (0–100) → maps to weekly premium adjustment
- **Phase 1:** Rule-based mock; Phase 2: trained on synthetic + public weather data

### 2. Fraud Detection Engine
- **Anomaly Detection:** Isolation Forest model
- **Signals monitored:**
  - GPS location mismatch (worker not in registered zone during claimed disruption)
  - Claim filed despite active delivery records on platform (simulated Swiggy/Zomato activity feed — if worker is actively completing orders, disruption claim is flagged)
  - Multiple claims in rapid succession
  - Device fingerprint inconsistency
- **Output:** Fraud risk score → Auto-approve (low), Flag for review (medium), Reject (high)

### 3. Predictive Disruption Alerts
- **Model:** Time-series forecasting (Prophet / LSTM) on weather data
- **Use:** Pre-warn workers of likely disruption next day; allow insurers to provision payout reserves
- **Phase 3 feature**

### 4. AI Risk Map (Visual Analytics Dashboard)
- **What it shows:** Chennai zone-level risk heatmap
  - 🔴 High flood/heat risk zones (e.g., Velachery, Tambaram)
  - 🟡 Moderate risk zones
  - 🟢 Low risk / safe zones
- **Benefits:** Drives hyper-local premium pricing; gives insurers real-time portfolio risk view
- **Tech:** Google Maps SDK + historical weather + claim data overlay

---

## 🛠️ Tech Stack

### Mobile App (Frontend)
- **Framework:** React Native (Expo) — cross-platform iOS + Android
- **UI Library:** React Native Paper / NativeWind (Tailwind for RN)
- **State Management:** Zustand
- **Maps:** React Native Maps (Google Maps SDK)

### Backend
- **Runtime:** Node.js + Express.js
- **Database:** PostgreSQL (user profiles, policies, claims) + Redis (real-time trigger cache)
- **Auth:** Firebase Auth (phone number OTP — familiar to gig workers)
- **Job Scheduler:** Bull Queue (for periodic weather API polling)

### AI/ML
- **Language:** Python (FastAPI microservice)
- **Libraries:** Scikit-learn, XGBoost, Prophet
- **Serving:** REST API called by Node backend

### Integrations
| Integration | Provider | Mode |
|---|---|---|
| Weather data | OpenWeatherMap API | Real (free tier) |
| Civil disruption alerts | Google Alerts RSS + admin panel | Mock (Phase 1-2) |
| Payment gateway | Razorpay Test Mode | Sandbox |
| Platform activity (Zomato/Swiggy) | Simulated delivery data | Mock |

### Infrastructure
- **Hosting:** Railway.app / Render (backend) + Expo EAS (mobile builds)
- **CI/CD:** GitHub Actions
- **Version Control:** GitHub (this repo)


## 🏗️ Repository Structure (Planned)

```
gigshield/
├── mobile/               # React Native app
│   ├── screens/
│   ├── components/
│   └── navigation/
├── backend/              # Node.js + Express API
│   ├── routes/
│   ├── services/
│   │   ├── weatherService.js
│   │   ├── triggerEngine.js
│   │   └── fraudService.js
│   └── models/
├── ml/                   # Python FastAPI ML service
│   ├── premium_model/
│   └── fraud_model/
├── docs/                 # Architecture diagrams, wireframes
└── README.md
```

---
