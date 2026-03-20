# Guidewire_teamW
Initially using the repository for Phase one submission (Seed)

Guidewire_Team_W

GigPhare — AI-Powered Parametric Income Protection for Gig Workers

Inspired by Guidewire, we wanted a name that conveys care, guidance, and reliability for gig workers. We chose "GigPhare" — from French "phare" meaning lighthouse — symbolizing a guiding light in difficult times, providing quick, fair, and life-saving support for gig workers. Short, memorable, and meaningful.


The Problem
India's gig workforce exceeds 15 million workers. Delivery partners on platforms like Swiggy and Zomato work 8–10 hours outdoors daily, with earnings directly tied to road conditions. A rain spell, AQI spike, or local curfew can wipe out an entire day's income within hours.

External disruptions reduce daily income by 20–30% on average (NITI Aayog, 2022)
Over 59% of delivery workers struggle to meet basic needs during disruption periods
No minimum wage protection, no sick leave, no short-term income safety net exists for platform workers
India's Code on Social Security (2020) recognizes gig workers — but no real-time compensation mechanism exists


What GigPhare Does
GigPhare is a parametric micro-insurance platform that protects gig workers from income loss caused by external disruptions. Instead of manual claims:

Monitors real-world conditions (weather, AQI, curfews, traffic)
Detects income impact using platform activity signals
Automatically triggers compensation — no claim filing, no waiting


Persona Scenarios
Rajan, 28 — Full-time delivery partner, Chennai
Heavy rain (65mm/hr) hits his zone. He earns Rs. 140 against his Rs. 550 baseline. GigPhare's rain trigger fires, income impact scores at 75% drop (High Impact), and Rs. 380 is credited to his UPI within 2 hours. His weekly premium: Rs. 50.
Meena, 34 — Part-time partner, Bengaluru
AQI crosses 350 + two-wheeler movement restriction issued. Her GPS activity shows zero deliveries in that window. Fraud check passes. Partial compensation of Rs. 120 auto-credited. Her weekly premium: Rs. 20.
Fraud attempt — Coordinated group claim
12 workers submit claims simultaneously in a zone with no active trigger. Hard check fails immediately. Synchronized timing (< 4 min window) and GPS–IP mismatch flag the cluster. 9 rejected outright, 3 routed to manual review.

Weekly Premium Model
Premiums are auto-deducted every Monday from the worker's UPI or platform wallet. Risk tier is recalculated weekly based on zone disruption history, work hours, and operating area.
Risk TierWeekly PremiumProfileLowRs. 20Part-time, suburban, stable weather historyMediumRs. 50Full-time, urban, moderate disruption historyHighRs. 100Full-time, flood-prone or high-AQI zone
Premiums adjust dynamically — a worker shifting to a safer zone sees a lower tier within 1–2 weeks.

Parametric Triggers
Triggers are evaluated on three dimensions: threshold crossed, duration sustained (typically 2+ hrs), and worker GPS matches the affected zone.
TriggerThresholdSourceMin DurationHeavy Rain> 55 mm/hrIMD / OpenWeatherMap2 hoursExtreme Heat> 42°CWeather API3 hoursAir PollutionAQI > 300 (PM2.5)CPCB / IQAir2 hoursCurfew / RestrictionBinary authority orderNews API + manual flagAnyTraffic DisruptionZone speed < 5 km/hrGoogle Maps API90 minutes
A trigger opens a compensation evaluation window — payout is not automatic until income impact is scored.
Compensation Logic
Impact ScoreClassificationPayout≥ 75% income dropHigh ImpactUp to 80% of daily baseline gap40–74% dropMedium ImpactProportional to score< 40% dropLow ImpactNo payout
The 80% cap is intentional — it prevents a scenario where workers are better off not working during disruptions.

AI/ML Integration
ModuleModelWhyKey InputsRisk ClassificationRandom Forest ClassifierHandles non-linear interactions; robust to missing dataGPS zone, work hours, disruption history, platform typeIncome PredictionRandom Forest RegressorCaptures time-of-day and zone-density interactions wellDay, hour, zone, weather forecast, order densityPremium OptimizationGradient Boosting RegressorIteratively corrects pricing based on regional risk patternsZone risk score, disruption frequency, activity indexFraud DetectionIsolation ForestUnsupervised anomaly detection — no labeled fraud data needed at launchGPS patterns, claim timing, sensor signals, IP data
Fraud validation runs in three layers:

Hard checks — no active trigger in zone, GPS mismatch, claim filed too late → instant rejection
Behavioral scoring — GPS movement consistency, order activity correlation, sensor continuity
Anomaly detection — Isolation Forest flags outliers; synchronized claims across users detected at network level

Trust Score > 80 → instant payout. Score 50–80 → partial + 24hr review. Below 50 → manual review (worker can submit photo proof).

Platform Choice — Mobile First (Flutter)
We chose Flutter over a web app for concrete reasons:

Delivery partners operate entirely from smartphones — desktop access is minimal
GPS, gyroscope, and accelerometer access for fraud detection are native mobile capabilities
Push notifications for triggers and payouts work naturally on mobile
Single Flutter codebase covers both Android and iOS
A lightweight web dashboard exists for admin/partners only


Tech Stack
LayerTechnologyMobile AppFlutter (Dart)Admin DashboardReact.jsAPI LayerNode.js + ExpressML ServicesPython + FastAPIDatabaseMongoDBML ModelsPython (scikit-learn)Trigger DataOpenWeatherMap, CPCB API, Google MapsPaymentsRazorpay (sandbox)
Backend services: User Service · Trigger Engine · Claim Processing · Payment Service · ML Inference · Notifications

Development Plan
PhaseTimelineFocusFoundationWeeks 1–3Onboarding, risk profiling, premium modelCore EngineWeeks 4–6Live triggers, income scoring, hard fraud checksML IntegrationWeeks 7–9RF models, Isolation Forest, model API layerPaymentsWeeks 10–11Razorpay UPI flows, payout audit trailMVPWeek 12End-to-end testing, admin dashboard, partner mock

What Makes GigPhare Different

No claims process — triggers fire automatically, workers never file anything
Proportional payouts — 30% income loss gets proportional compensation, not binary all-or-nothing
Fraud resistance by design — gaming the system requires faking external conditions AND behavior signals simultaneously
Dynamic pricing — premiums adjust to actual zone risk, not static actuarial tables
Platform-agnostic — integrates with any gig platform via API


Next Steps

Integrate live IMD, CPCB, and Google Maps APIs (replacing mocks)
Pilot with 50–100 delivery partners in Chennai or Bengaluru
Partner with one gig platform for wallet integration and activity data API
Explore IRDAI regulatory sandbox participation


Built with Node.js · Flutter · Python (ML) · MongoDB · React
