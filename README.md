Guidewire_Team_W

GigPhare - AI-Powered Parametric Income Protection for Gig Workers

Inspired by Guidewire, we wanted a name that conveys care, guidance, and reliability for gig workers. We chose "GigPhare" -from French "phare" meaning lighthouse - symbolizing a guiding light in difficult times, providing quick, fair, and life-saving support for gig workers. Short, memorable, and meaningful.


The Problem :
India's gig workforce exceeds 15 million workers. Delivery partners on platforms like Swiggy and Zomato work 8–10 hours outdoors daily, with earnings directly tied to road conditions.
A rain spell, AQI spike, or local curfew can wipe out an entire day's income within hours.

External disruptions reduce daily income by 20–30% on average (NITI Aayog, 2022)
Over 59% of delivery workers struggle to meet basic needs during disruption periods
No minimum wage protection, no sick leave, no short-term income safety net exists for platform workers
India's Code on Social Security (2020) recognizes gig workers — but no real-time compensation mechanism exists


What GigPhare Does?
GigPhare is a parametric micro-insurance platform that protects gig workers from income loss caused by external disruptions. Instead of manual claims:

+ Monitors real-world conditions (weather, AQI, curfews, traffic)
+ Detects income impact using platform activity signals
+ Automatically triggers compensation — no claim filing, no waiting

Persona Scenarios:
Rajan, 28 - Full-time delivery partner, Chennai
Heavy rain (65mm/hr) hits his zone. He earns Rs. 140 against his Rs. 550 baseline. GigPhare's rain trigger fires, income impact scores at 75% drop (High Impact), and Rs. 380 is credited to his UPI within the end of the day. His weekly premium: Rs. 500.
Meena, 34 - Part-time partner, Bengaluru
AQI crosses 350 + two-wheeler movement restriction issued. Her GPS activity shows zero deliveries in that window. Fraud check passes. Partial compensation of Rs. 120 auto-credited. Her weekly premium: Rs. 250.
Fraud attempt - Coordinated group claim
12 workers submit claims simultaneously in a zone with no active trigger. Hard check fails immediately. Synchronized timing (< 4 min window) and GPS–IP mismatch flag the cluster. 9 rejected outright, 3 routed to manual review.
The gig worker can also pay on daily basis with certain percentage.
(the amount mentioned here is just for the understanding purpose)

Weekly Premium Model:
Premiums are auto-deducted every Monday from the worker's UPI or platform wallet. Risk tier is recalculated weekly based on zone disruption history, work hours, and operating area.
Risk Tier Weekly Premium Profile Low Rs.50 Part-time, suburban, stable weather history Medium Rs.50 Full-time, urban, moderate disruption history High Rs.100 Full-time, flood-prone or
high-AQI zone
Premium adjust dynamically. a worker shifting to a safer zone sees a lower tier within 1–2 weeks.

Insurance Claim Rules & Minimum Balance

Minimum Balance Requirement:
Users must maintain a minimum weekly balance of ₹700 to be eligible for any compensation under the insurance system.

Flexible Contribution:
Users can contribute more than the minimum (e.g., ₹1000, ₹1500) if they wish, but ₹700 is mandatory to qualify for claims.

Contribution Frequency:
Contributions can be collected daily or weekly, based on the user’s preference.

Cancellation & Withdrawal:
Users can cancel or withdraw their contributions at any time. However, compensation is only available if the minimum balance requirement is met.

Compensation Conditions:
If the user’s balance is below the minimum, or if they cancel contributions before a claim, no compensation will be provided, even if they face a negative event.

Purpose & Rationale:

Ensures sustainability: Setting a minimum balance guarantees that funds are available for compensation when needed, preventing system overload or failure.

User-friendly design: Users are not locked in—they can withdraw anytime, so contributions aren’t a burden.

Fairness & transparency: Only users who maintain the minimum balance can claim compensation, making the system predictable and trustworthy.

Financial flexibility: While ₹700 is the minimum, users can contribute more if they want additional coverage, accommodating different income levels without causing frustration.


Parametric Triggers:
Triggers are evaluated on three dimensions: threshold crossed, duration sustained (typically 2+ hrs), and worker GPS matches the affected zone.
Trigger Threshold Source Min Duration Heavy Rain > 55 mm/hr IMD/OpenWeatherMap2 hours Extreme Heat> 42°CWeather API3 hours Air Pollution AQI > 300 (PM2.5)CPCB / IQAir2 hours Curfew / Restriction Binary authority order News API + manual flag Any Traffic Disruption Zone speed < 5 km/hr Google Maps API90 minutes
A trigger opens a compensation evaluation window — payout is not automatic until income impact is scored.

Compensation Logic:
Impact Score Classification Payout ≥ 75% income dropHigh ImpactUp to 80% of daily baseline gap 40–74% dropMedium Impact Proportional to score < 40% dropLow Impact No payout
The 80% cap is intentional, it prevents a scenario where workers are better off not working during disruptions.

AI/ML Integration:
Module Model Why Key Inputs Risk ClassificationRandom Forest ClassifierHandles non-linear interactions; robust to missing dataGPS zone, work hours, disruption history, platform typeIncome PredictionRandom Forest RegressorCaptures time-of-day and zone-density interactions wellDay, hour, zone, weather forecast, order densityPremium OptimizationGradient Boosting RegressorIteratively corrects pricing based on regional risk patternsZone risk score, disruption frequency, activity indexFraud DetectionIsolation ForestUnsupervised anomaly detection, no labeled fraud data needed at launchGPS patterns, claim timing, sensor signals, IP data

Fraud validation runs in three layers:

Hard checks - no active trigger in zone, GPS mismatch, claim filed too late → instant rejection
Behavioral scoring - GPS movement consistency, order activity correlation, sensor continuity
Anomaly detection - Isolation Forest flags outliers; synchronized claims across users detected at network level

Trust Score > 80 → instant payout. Score 50–80 → partial + 24hr review. Below 50 → manual review (worker can submit photo proof).

Platform Choice - Mobile First (Flutter)

We chose Flutter over a web app for concrete reasons:

Delivery partners operate entirely from smartphones - desktop access is minimal
GPS, gyroscope, and accelerometer access for fraud detection are native mobile capabilities
Push notifications for triggers and payouts work naturally on mobile
Single Flutter codebase covers both Android and iOS
A lightweight web dashboard exists for admin/partners only

Tech Stack:
Frontend (User + Admin)
Mobile App: Flutter (Dart)
-User onboarding
-Live trigger alerts
-Earnings dashboard
-Claim transparency
-Admin Dashboard: React.js
-Monitor triggers
-View claims & fraud alerts
-Manual review panel

2. Backend (Core System)
-Node.js + Express
-API Gateway
-Authentication (JWT)
-Business logic
-Service orchestration

3. ML Microservice
+Python + FastAPI
+Model inference APIs
+Fraud detection
+Risk scoring
+Income prediction

4. Database

MongoDB Collections:
(Users, Activity Logs, Claims, Risk Profiles, Trigger Events

5. External APIs
-Weather → OpenWeatherMap / IMD
-Air Quality Index → CPCB / IQAir
-Traffic → Google Maps API
-Payments → Razorpay

6. DevOps
-Docker (containerization)
-AWS / GCP
-EC2 (backend)
-S3 (logs)
-Lambda (trigger checks)
-CI/CD → GitHub Actions

OVERALL ML PIPELINE 
Raw Data → Feature Engineering → Model Prediction → Decision Engine

Data Sources:
GPS (lat, lon, movement)
Time (hour, weekday)
Weather (rain, temp)
AQI
Platform activity (orders, earnings)

 1. RISK CLASSIFICATION MODEL (Random Forest Classifier)
 to assign each worker a risk tier: [Low, medium, high]
This directly affects:
+Premium pricing
+Mathematical Intuition
Random Forest is  ensembling of decision trees
Each tree - Splits data based on features
Features Used
Feature with Meaning
avg_daily_hours - Worker effort
zone_type - urban / rural
disruption_frequency - how often disruptions occur
avg_income_variance - income stability
weather_volatility - unpredictability
Training Process
Collect historical data:
[hours, zone, disruptions, income_var] → risk_label
Bootstrap sampling:
Random subsets of data used to build trees
Feature randomness:
Each split considers random features
Build ~100 trees

2. INCOME PREDICTION MODEL (Random Forest Regressor)

- Mathematical Intuition
Instead of classification → regression
Each tree predicts a number:
Tree 1 → ₹500  
Tree 2 → ₹540  
Tree 3 → ₹520  
Final output:
👉 Average = ₹520

+Features Used - (hour_of_day, day_of_week, zone_density, weather, historical earnings, order volume)
+Training Process
Collect historical logs:
[time, zone, weather, orders] → income
+Train model to learn:
Peak hours, Zone demand, Weather effects

Why Random Forest?

+ Captures time + location interactions
+ No strict assumptions (unlike linear regression)
+ Works well with tabular data

 3. PREMIUM OPTIMIZATION MODEL(Gradient Boosting Regressor)
+Mathematical Intuition
+Gradient Boosting: Builds trees sequentially
Each tree corrects previous error
Model 1 → error
Model 2 → fixes error
Model 3 → refines further
+Features
Features: zone_risk_score, claim_frequency avg_payout, work_hours
Training
Loss function: Minimize pricing error
Iterative learning: Focus on high-error cases

4. FRAUD DETECTION MODEL (Isolation Forest)
+Mathematical Intuition
Isolation Forest works on: “Anomalies are easier to isolate”
Normal behavior: 
Dense cluster
Hard to isolate
Fraud:
Rare / unusual
Isolated quickly

+Features:  
gps_variance, claim_time_gap, ip_location, activity_level, sensor data
Training

No labels required

Random splits:

Feature selection

Random thresholds

Build trees:

Measure path length


COMBINED MODEL DECISION LOGIC
Step-by-step:
1. Trigger Detected ----> Rain / AQI / Traffic
2. Income Model------>Predict expected income
3. Compare Actual vs Predicted------>Calculate drop %
4. Fraud Model------->Check anomaly score
5. Risk Model------>Determine user tier
6. Final Decision
Condition	                   Action
High drop + low fraud	   Full payout
Medium drop	                   Partial payout
High fraud	                   Reject

Development Plan:
PhaseTimelineFocusFoundationWeeks 1–3Onboarding, risk profiling, premium modelCore EngineWeeks 4–6Live triggers, income scoring, hard fraud checksML IntegrationWeeks 7–9RF models, Isolation Forest, model API layerPaymentsWeeks 10–11Razorpay UPI flows, payout audit trailMVPWeek 12End-to-end testing, admin dashboard, partner mock

What Makes GigPhare Different...

No claims process - triggers fire automatically, workers never file anything
Proportional payouts - 30% income loss gets proportional compensation, not binary all-or-nothing
Fraud resistance by design - gaming the system requires faking external conditions AND behavior signals simultaneously
Dynamic pricing - premiums adjust to actual zone risk, not static actuarial tables
Platform-agnostic - integrates with any gig platform via API


Next Steps:

Integrate live IMD, CPCB, and Google Maps APIs (replacing mocks)
Pilot with 50–100 delivery partners in Chennai or Bengaluru
Partner with one gig platform for wallet integration and activity data API
Explore IRDAI regulatory sandbox participation


Built with Node.js · Flutter · Python (ML) · MongoDB
