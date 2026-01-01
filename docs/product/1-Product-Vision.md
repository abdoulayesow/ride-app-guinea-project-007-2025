# Product Vision Document
## Guinea Ride-Hailing & Delivery Application

**Version:** 1.0  
**Date:** December 2025  
**Product Name:** Pssst

---

## Executive Summary

We are building **Pssst**, Guinea's first app-based ride-hailing and delivery platform, addressing a critical gap in the transportation market. Currently, residents of Conakry and other Guinean cities rely exclusively on informal cash-based taxi services or personal connections to secure transportation. Our platform will provide instant access to vetted drivers, transparent pricing in Guinean Francs, and flexible payment options adapted to local infrastructure.

---

## Vision Statement

**To become West Africa's most trusted mobility platform by building technology that works in real-world conditions, not just ideal ones.**

We envision a future where every person in Guinea can access safe, reliable transportation at the tap of a button—whether they have a street address, reliable internet connectivity, or a bank account.

---

## Mission Statement

**To provide safe, reliable, and affordable on-demand transportation and delivery services to every resident of Guinea through technology that works in local conditions.**

We will achieve this by:
- Building offline-first technology that functions with intermittent connectivity
- Supporting cash and mobile money payments that match how people actually transact
- Creating navigation systems that work without formal addresses
- Offering daily driver payouts that align with Guinea's cash-flow economy
- Partnering with local communities rather than extracting from them

---

## Core Values

### 1. Local-First Technology
We don't force Western assumptions onto African markets. We build for the conditions that exist, not the ones we wish existed.

### 2. Economic Empowerment
Drivers are partners, not gig workers. We offer fair commissions (10-15% vs 20-25% industry standard), daily payouts, and pathways to vehicle ownership.

### 3. Radical Reliability
In a market where infrastructure is unreliable, our app must be the most reliable thing in a user's day. Offline-first architecture, pre-downloaded maps, and degraded-mode functionality are non-negotiable.

### 4. Safety Without Compromise
Every feature prioritizes rider and driver safety: trip sharing, SOS buttons, driver verification, and 24/7 support in local languages.

### 5. Community Partnership
We succeed when our communities succeed. This means partnering with taxi fleet owners for driver onboarding, working with mapping communities to improve OpenStreetMap data, and supporting local mobile money infrastructure.

---

## Problem Statement

### Current State
Guinea's transportation market is fragmented and inefficient:

**For Riders:**
- No way to request a ride on-demand without personal connections
- Unpredictable pricing with frequent overcharging
- Safety concerns, especially for women traveling alone at night
- Long wait times at taxi stands during peak hours
- No recourse for poor service or safety incidents

**For Drivers:**
- Unpredictable income requiring hours of idle waiting
- Fuel waste driving around looking for passengers
- Difficulty finding passengers during off-peak hours
- No protection from passengers who refuse to pay
- Inability to access capital for vehicle purchases or maintenance

**Market Gap:**
Zero app-based transportation platforms operate in Guinea despite:
- 2+ million population in Conakry alone
- 3.2 million mobile money users nationwide
- Growing smartphone penetration (Android dominant)
- Successful ride-hailing adoption in neighboring countries

---

## Target Market

### Primary Market: Conakry, Guinea
- **Population:** 2+ million (capital city)
- **Geography:** Coastal city with mixture of urban density and suburban sprawl
- **Infrastructure:** Limited road mapping, no formal address system, intermittent internet connectivity
- **Payment Systems:** Cash dominant, Orange Money and MTN Mobile Money available
- **Competition:** Informal taxi stands, personal vehicles, no app-based services

### Secondary Markets (12-18 Months Post-Launch)
- Kankan (population ~200,000)
- Nzérékoré (population ~200,000)
- Kindia (population ~150,000)

### User Segments

**Riders (Demand Side):**
1. **Students & Young Professionals (Ages 18-35)**
   - University students needing reliable transport to campus
   - Young workers commuting to jobs in business districts
   - Tech-savvy, comfortable with mobile apps
   - Price-sensitive, prefer Orange Money over cash

2. **Business Professionals (Ages 30-50)**
   - Corporate employees needing punctual airport/meeting transport
   - Expense-conscious, need digital receipts for reimbursement
   - Value time over price
   - Willing to pay premium for reliability

3. **Families & Occasional Users (All Ages)**
   - Weekend errands, medical appointments, social visits
   - Safety-conscious, especially for children/elderly
   - Mixed payment preferences (cash and mobile money)

**Drivers (Supply Side):**
1. **Full-Time Taxi Drivers**
   - Experienced drivers seeking steady income
   - Own or lease vehicles
   - Need to maximize daily trips to cover vehicle payments
   - Prefer daily cash payouts

2. **Part-Time Drivers**
   - Supplement primary income (teachers, office workers)
   - Own personal vehicles
   - Want flexible hours (evenings, weekends)
   - More tech-savvy than full-time drivers

---

## Product Goals

### 6-Month Goals (MVP Launch)
1. **Supply:** Onboard 500 active drivers in Conakry completing 5+ trips/week
2. **Demand:** Achieve 10,000 monthly active riders with 25%+ repeat rate
3. **Quality:** Maintain average wait time <5 minutes in Conakry
4. **Satisfaction:** Average rider rating >4.5/5 stars
5. **Reliability:** App crash rate <1%, transaction success rate >95%
6. **Growth:** Month-over-month trip volume growth >20%

### 12-Month Goals (Post-MVP)
1. **Geographic:** Expand to 2 additional cities (Kankan, Nzérékoré)
2. **Supply:** Scale to 1,500 active drivers across 3 cities
3. **Demand:** Reach 50,000 monthly active riders
4. **Diversification:** Launch delivery services (packages, food)
5. **Financial:** Achieve positive unit economics in Conakry
6. **Driver Retention:** Maintain 6-month driver retention >40%

### 24-Month Goals (Scale)
1. **Market Position:** Become #1 mobility platform in Guinea
2. **Coverage:** Operate in 5+ cities covering 60% of urban population
3. **Services:** Full super-app (rides, delivery, mobile money, microfinancing)
4. **Profitability:** Achieve operational breakeven
5. **Social Impact:** Facilitate 10,000+ driver vehicle purchases through financing partnerships

---

## Key Differentiators

### 1. Built for Guinea's Infrastructure Reality
**Challenge:** No formal address system in most of Conakry  
**Our Solution:** Pin-drop pickup + What3Words + landmark database + photo/voice location sharing

**Challenge:** Intermittent internet connectivity  
**Our Solution:** Offline-first architecture with pre-downloaded maps (Mapbox/OpenStreetMap)

**Challenge:** Limited Google Maps coverage  
**Our Solution:** Community-driven mapping with driver feedback loops, partnership with HOT West Africa

### 2. Payment Flexibility
**Challenge:** Low bank account penetration, cash-dominated economy  
**Our Solution:** 
- Cash payments (driver handles reconciliation)
- Orange Money Web Payment API integration
- MTN MoMo support (Phase 2)
- In-app wallet for both riders and drivers
- Digital receipts for all transactions

### 3. Driver-Centric Economics
**Challenge:** Uber/Bolt commission rates (20-25%) unsustainable for developing markets  
**Our Solution:**
- Lower commission: 10-15% vs 20-25%
- Daily payouts to mobile money (not weekly)
- Transparent earnings dashboard
- No hidden fees or surge pricing confusion
- Driver-initiated bonuses for high trip volumes

### 4. Localized Safety Features
**Challenge:** Safety concerns specific to Guinea context  
**Our Solution:**
- Emergency SOS button with GPS sharing
- Trip sharing to family/friends contacts
- Driver verification (photo, license, vehicle inspection)
- 24/7 support in French, Susu, Pular, Malinké
- In-app masked phone calls (privacy protection)
- Female driver option for female passengers

### 5. Community Partnership Model
**Challenge:** International platforms struggle with local market knowledge  
**Our Solution:**
- Partner with existing taxi fleet owners for driver recruitment
- Work with Orange Money agents for cash-to-digital onboarding
- Collaborate with FreeLocalMappers (Guinea OSM community)
- Support local vehicle financing through partnerships

---

## Product Strategy

### Phase 1: Foundation (Months 1-3)
**Focus:** Launch core ride-hailing in Conakry with essential features

**Key Deliverables:**
- Rider app (Android + iOS)
- Driver app (Android + iOS)
- Backend infrastructure
- Payment integration (Cash + Orange Money)
- Offline mapping with Mapbox
- Basic safety features (SOS, trip sharing)

**Success Metrics:**
- 500 drivers onboarded
- 10,000 riders registered
- 50,000 total trips completed
- <5min average wait time
- >4.5 average rider rating

### Phase 2: Enhancement (Months 4-6)
**Focus:** Improve core experience and expand payment options

**Key Deliverables:**
- MTN MoMo integration
- In-app wallet system
- Landmark database (500+ POIs)
- Advanced navigation (photo/voice sharing)
- Trip scheduling
- Referral program

**Success Metrics:**
- 1,000 drivers active
- 25,000 monthly riders
- 150,000 total trips
- 30% digital payment adoption
- 40% driver 3-month retention

### Phase 3: Scale (Months 7-12)
**Focus:** Geographic expansion and service diversification

**Key Deliverables:**
- Launch in Kankan and Nzérékoré
- Delivery services (packages, food)
- Driver financing program
- Local language voice navigation
- Mapillary street imagery collection
- Corporate accounts

**Success Metrics:**
- 1,500 drivers across 3 cities
- 50,000 monthly riders
- 500,000 total trips
- Positive unit economics in Conakry
- 40% driver 6-month retention

---

## Success Criteria

### Product-Market Fit Indicators
- **Organic Growth:** >30% of new riders from referrals (not paid marketing)
- **Engagement:** >60% of riders take 2+ trips per month
- **Driver Satisfaction:** >75% of drivers rate platform 4+ stars
- **Wait Time:** <5 minutes average across Conakry
- **Reliability:** >98% trip completion rate (no cancellations)

### Business Viability Indicators
- **Unit Economics:** Gross margin >30% per trip within 6 months
- **Driver Retention:** >40% of drivers active after 6 months
- **Payment Mix:** >25% digital payments by Month 6
- **Customer Acquisition Cost:** <$5 per rider in paid channels
- **Lifetime Value:** Average rider generates >$50 gross revenue in first year

### Social Impact Indicators
- **Driver Income:** Average driver earns >3,000,000 GNF/month (above taxi stand income)
- **Women Drivers:** >10% of driver base is female by Month 12
- **Accessibility:** Service available in neighborhoods previously underserved
- **Map Improvements:** 1,000+ OSM edits contributed by driver community
- **Vehicle Ownership:** Facilitate 50+ driver vehicle purchases through financing partnerships

---

## Risks & Mitigation

### Market Risks

**Risk:** Low smartphone penetration limits addressable market  
**Mitigation:** Focus on Android (90%+ market share), optimize for low-end devices, offer offline functionality

**Risk:** Riders prefer cash and resist mobile money adoption  
**Mitigation:** Keep cash as primary payment option, offer incentives for digital adoption, educate on mobile money benefits

**Risk:** Incumbent taxi unions oppose platform and organize resistance  
**Mitigation:** Partner with fleet owners for driver recruitment, position as income opportunity (not replacement), work with government on regulatory framework

### Technology Risks

**Risk:** OpenStreetMap data insufficient for reliable navigation  
**Mitigation:** Community mapping partnership, driver feedback loops, fallback to landmark/photo-based navigation

**Risk:** Offline functionality doesn't work reliably in poor connectivity  
**Mitigation:** Extensive field testing, progressive enhancement architecture, SMS fallback for critical notifications

**Risk:** Mobile money API integration failures cause payment issues  
**Mitigation:** Redundant payment providers (Orange + MTN), cash fallback always available, local fintech partnership (Lengo Pay)

### Operational Risks

**Risk:** Insufficient driver supply causes long wait times and user churn  
**Mitigation:** Aggressive driver recruitment, low commission structure, daily payouts, driver referral bonuses

**Risk:** Customer support cannot handle volume in local languages  
**Mitigation:** Hire local support team fluent in French/Susu/Pular/Malinké, build robust in-app help center, automated resolution for common issues

**Risk:** Safety incidents damage brand reputation  
**Mitigation:** Comprehensive driver background checks, 24/7 emergency response, insurance partnerships, proactive safety education

### Financial Risks

**Risk:** Burn rate too high to reach profitability  
**Mitigation:** Lean MVP approach, focus on organic growth, prioritize unit economics over vanity metrics

**Risk:** Cannot raise follow-on funding to scale  
**Mitigation:** Demonstrate strong product-market fit metrics within 6 months, build relationships with Africa-focused VCs early

---

## Measures of Success

### North Star Metric
**Total trips completed per week**

This single metric captures:
- Rider demand and engagement
- Driver supply and activity
- Platform reliability and trust
- Overall market traction

### Supporting Metrics

**Growth:**
- Weekly active riders
- Weekly active drivers
- Month-over-month trip growth %

**Engagement:**
- Trips per rider per month
- Trips per driver per day
- Repeat rider rate (30-day)

**Quality:**
- Average wait time (pickup to arrival)
- Trip completion rate (no cancellations)
- Average rider rating
- Average driver rating

**Economics:**
- Gross margin per trip
- Customer acquisition cost (CAC)
- Lifetime value (LTV)
- LTV:CAC ratio

**Operations:**
- App crash rate
- Payment success rate
- Support ticket resolution time
- Driver 90-day retention rate

---

## Conclusion

This product vision charts a path to building Guinea's first truly local mobility platform—one that works with the country's infrastructure reality rather than against it. Success requires obsessive focus on reliability, community partnership, and economic fairness. 

Our competitive advantage lies not in importing a Silicon Valley playbook, but in building technology grounded in Guinea's actual conditions: offline-first for poor connectivity, mobile money for financial inclusion, landmark-based for missing addresses, and daily payouts for cash-flow economics.

If we execute this vision, we won't just build a successful business—we'll fundamentally improve how millions of people move through their cities, earn their livelihoods, and access economic opportunity.

---

**Next Steps:**
1. Complete technical architecture documentation
2. Register Orange Money merchant account
3. Begin driver recruitment partnerships in Conakry
4. Set up pilot testing program (50 drivers, 2 weeks)
5. Finalize branding and marketing materials for Pssst
6. Prepare for Q2 2026 public launch
