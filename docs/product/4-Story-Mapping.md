# User Story Mapping
## Pssst - Guinea Ride-Hailing & Delivery Application

**Version:** 1.0  
**Date:** December 2025

---

## Table of Contents
1. [What is Story Mapping?](#what-is-story-mapping)
2. [Pssst User Journeys](#pssst-user-journeys)
3. [MVP Story Map (Phase 1)](#mvp-story-map-phase-1)
4. [Phase 2 Story Map](#phase-2-story-map)
5. [Sprint Planning](#sprint-planning)
6. [Acceptance Criteria](#acceptance-criteria)

---

## What is Story Mapping?

Story mapping is a collaborative planning technique that organizes user stories along two dimensions:

### Horizontal Axis: User Activities
High-level tasks users perform to accomplish their goals (e.g., "Book a Ride", "Complete Trip", "Get Paid")

### Vertical Axis: Priority & Releases
User stories organized by implementation priority, with the most critical features at the top. Horizontal lines represent release boundaries (MVP, Phase 2, Future).

### Benefits for Pssst
- **Shared understanding** - Entire team visualizes the user journey
- **Priority clarity** - What's essential vs. nice-to-have becomes obvious
- **Release planning** - Natural slicing into MVP and future phases
- **Gap identification** - Missing steps in user journey become visible
- **Scope management** - Easy to see what can be deferred to Phase 2

---

## Pssst User Journeys

### Rider Journey: From Discovery to Repeat Usage

```
Discovery → Download → Onboard → Request Ride → Wait & Track → Complete Trip → Rate & Pay → Repeat
```

**Journey Details:**

1. **Discovery** - How riders learn about Pssst
   - Friend referral (target: 30% of signups)
   - Social media advertising
   - University partnerships
   - Orange Money co-marketing

2. **Download & Setup** - First-time setup experience
   - Install app from Play Store / App Store
   - Phone number verification (SMS OTP)
   - Basic profile creation (name only)
   - Payment method selection (cash default, Orange Money optional)

3. **Request Ride** - Booking a trip
   - Pin-drop pickup location on map
   - Enter destination (pin-drop or search)
   - See upfront price estimate
   - Confirm booking
   - Match with nearest available driver

4. **Wait & Track** - Between booking and pickup
   - View driver approaching in real-time
   - See driver photo, name, vehicle details, rating
   - Contact driver via in-app chat or call
   - Share trip details with family/friends
   - Estimate time of arrival (ETA)

5. **Complete Trip** - During and after the ride
   - Navigate to destination
   - Pay via cash or Orange Money
   - Rate driver (1-5 stars)
   - Provide feedback (optional)
   - Receive digital receipt

6. **Repeat** - Becoming a regular user
   - Quick rebooking to favorite locations
   - Referral rewards for inviting friends
   - Trip history review
   - Loyalty benefits

### Driver Journey: From Signup to Earning

```
Learn About Pssst → Sign Up → Onboarding → Go Online → Accept Rides → Navigate → Complete Trips → Get Paid → Repeat
```

**Journey Details:**

1. **Learn About Pssst** - Discovery channels
   - Fleet owner partnerships (target: 50% of drivers)
   - Driver referrals (existing drivers recruit friends)
   - Taxi stand recruitment
   - Social media targeting

2. **Sign Up** - Initial registration
   - Phone number registration
   - Submit required documents (ID, license, insurance, vehicle registration)
   - Upload vehicle photos
   - Background check initiated

3. **Onboarding** - Training and approval
   - In-person orientation session
   - Vehicle inspection
   - App tutorial and test drives
   - Receive driver kit (phone holder, charger, branding materials)
   - Account activation

4. **Go Online** - Start accepting trips
   - Toggle availability status (online/offline)
   - Set preferences (areas, trip distance limits)
   - View demand heat map
   - See current queue position

5. **Accept & Navigate** - Handling ride requests
   - Receive ride request notification
   - View fare estimate and trip details
   - Accept or reject (15-second window)
   - Navigate to pickup using offline maps
   - Contact rider if needed
   - Confirm pickup
   - Navigate to destination
   - Confirm dropoff

6. **Get Paid** - Earnings and payouts
   - View trip earnings in real-time
   - Track daily, weekly, monthly totals
   - Automatic daily payout to Orange Money (6 PM)
   - View earnings breakdown (fare, tips, bonuses, commission)
   - Access digital receipts for all trips

---

## MVP Story Map (Phase 1: Months 1-3)

**Goal:** Launch core ride-hailing functionality in Conakry  
**Success Metrics:** 500 drivers, 10,000 riders, <5min wait time, >4.5 rating

### User Activity 1: User Onboarding

#### Epic: Rider Registration
**Priority: CRITICAL**

**User Stories:**
- As a new rider, I want to sign up with my phone number so I can quickly create an account
  - *Acceptance:* SMS OTP verification completes in <60 seconds
  - *Effort:* 3 points

- As a rider, I want to enter minimal information (name only) so onboarding is fast
  - *Acceptance:* Onboarding completes in <2 minutes
  - *Effort:* 2 points

- As a rider, I want to select my payment method (cash/Orange Money) so I can pay how I prefer
  - *Acceptance:* Payment methods clearly displayed, selection saved
  - *Effort:* 3 points

#### Epic: Driver Registration
**Priority: CRITICAL**

**User Stories:**
- As a driver, I want to register with my phone number and ID so I can start the approval process
  - *Acceptance:* Registration form validates ID format, sends confirmation SMS
  - *Effort:* 5 points

- As a driver, I want to upload photos of my license, vehicle, and insurance so Pssst can verify my eligibility
  - *Acceptance:* Photo upload works on 2G/3G, compresses large images automatically
  - *Effort:* 5 points

- As a driver, I want to schedule an in-person orientation so I can complete onboarding
  - *Acceptance:* 3 onboarding centers available in Conakry, scheduling within 48 hours
  - *Effort:* 8 points

---

### User Activity 2: Request Ride

#### Epic: Ride Booking
**Priority: CRITICAL**

**User Stories:**
- As a rider, I want to drop a pin on the map for my pickup location so I don't need a street address
  - *Acceptance:* Pin-drop accurate to 10 meters, What3Words address displayed
  - *Effort:* 5 points

- As a rider, I want to see my pickup location confirmed with What3Words so the driver can find me easily
  - *Acceptance:* What3Words address visible on booking screen, copyable to clipboard
  - *Effort:* 3 points

- As a rider, I want to set my destination by pin-drop or search so I can specify where I'm going
  - *Acceptance:* Both methods work, autocomplete for popular locations
  - *Effort:* 5 points

- As a rider, I want to see the upfront price before confirming so I know exactly what I'll pay
  - *Acceptance:* Price calculation shown within 2 seconds, displayed in GNF
  - *Effort:* 8 points

- As a rider, I want to confirm my booking and be matched with a nearby driver so I get picked up quickly
  - *Acceptance:* Matching completes within 30 seconds, rider sees "Searching for driver" status
  - *Effort:* 13 points (ride matching algorithm)

#### Epic: Ride Matching (Backend)
**Priority: CRITICAL**

**User Stories:**
- As the system, I need to match riders with the nearest available driver based on time-to-pickup
  - *Acceptance:* Algorithm considers distance, traffic, driver rating; matches within 30 seconds
  - *Effort:* 13 points

- As the system, I need to send the ride request to the driver with all trip details
  - *Acceptance:* Push notification + in-app alert, 15-second response window
  - *Effort:* 8 points

---

### User Activity 3: Complete Trip

#### Epic: Real-Time Tracking
**Priority: CRITICAL**

**User Stories:**
- As a rider, I want to see my driver's location in real-time so I know when they'll arrive
  - *Acceptance:* GPS updates every 5 seconds, ETA displayed and updates dynamically
  - *Effort:* 8 points

- As a rider, I want to see my driver's photo, name, vehicle details, and rating so I can identify them
  - *Acceptance:* All details visible on tracking screen, photo loads even on slow connection
  - *Effort:* 3 points

- As a rider, I want to contact my driver via in-app chat or call if I need to give directions
  - *Acceptance:* Masked phone numbers protect privacy, chat messages delivered within 3 seconds
  - *Effort:* 8 points

- As a rider, I want to share my trip details with family/friends so they can track my safety
  - *Acceptance:* Share link via WhatsApp/SMS, live tracking visible without app install
  - *Effort:* 5 points

#### Epic: Payment Processing
**Priority: CRITICAL**

**User Stories:**
- As a rider, I want to pay with cash so I don't need Orange Money if I prefer cash
  - *Acceptance:* Cash selection works, driver confirms payment received
  - *Effort:* 3 points

- As a rider, I want to pay with Orange Money so I don't have to carry cash
  - *Acceptance:* Orange Money Web Payment API integration, payment completes within 30 seconds
  - *Effort:* 13 points

- As a rider, I want a digital receipt sent to my phone so I have proof of payment
  - *Acceptance:* Receipt includes date, time, route, price; sent via SMS and in-app
  - *Effort:* 5 points

#### Epic: Rating & Feedback
**Priority: HIGH**

**User Stories:**
- As a rider, I want to rate my driver (1-5 stars) so good drivers are recognized
  - *Acceptance:* Rating prompt appears immediately after trip, skippable but encouraged
  - *Effort:* 3 points

- As a rider, I want to provide written feedback about my experience (optional)
  - *Acceptance:* Text field for comments, pre-defined tags (clean car, polite, good driving)
  - *Effort:* 3 points

---

### User Activity 4: Driver Operations

#### Epic: Driver Trip Management
**Priority: CRITICAL**

**User Stories:**
- As a driver, I want to see incoming ride requests with fare and destination so I can decide whether to accept
  - *Acceptance:* Request shows pickup location, destination, estimated fare, estimated time
  - *Effort:* 5 points

- As a driver, I want to accept or reject ride requests within 15 seconds
  - *Acceptance:* Accept/reject buttons prominent, countdown timer visible
  - *Effort:* 3 points

- As a driver, I want turn-by-turn navigation to the pickup location so I don't get lost
  - *Acceptance:* Mapbox navigation with offline maps, voice guidance in French
  - *Effort:* 13 points

- As a driver, I want to contact the rider if I can't find the pickup location
  - *Acceptance:* In-app chat and masked call, rider can send location photo
  - *Effort:* 5 points

- As a driver, I want to navigate to the destination using offline maps
  - *Acceptance:* Navigation works without internet, pre-downloaded Conakry maps
  - *Effort:* 8 points

- As a driver, I want to confirm trip completion and see my earnings immediately
  - *Acceptance:* One-tap completion, earnings shown within 2 seconds
  - *Effort:* 5 points

#### Epic: Driver Earnings & Payouts
**Priority: CRITICAL**

**User Stories:**
- As a driver, I want to see my real-time earnings dashboard (daily, weekly, monthly)
  - *Acceptance:* Dashboard shows gross, commission, net earnings; updates in real-time
  - *Effort:* 8 points

- As a driver, I want automatic daily payouts to my Orange Money account so I get cash flow
  - *Acceptance:* Payout processes at 6 PM daily, funds arrive within 1 hour
  - *Effort:* 13 points

- As a driver, I want to view my trip history with earnings breakdown
  - *Acceptance:* List view of all trips, tap for details (route, fare, commission, net)
  - *Effort:* 5 points

#### Epic: Safety Features
**Priority: CRITICAL**

**User Stories:**
- As a rider, I want an emergency SOS button that alerts police and shares my GPS location
  - *Acceptance:* SOS button accessible on tracking screen, triggers SMS to emergency contacts
  - *Effort:* 8 points

- As a rider, I want to share my trip in real-time with family so they can track my location
  - *Acceptance:* Share link via WhatsApp/SMS, updates every 10 seconds
  - *Effort:* 5 points

- As a driver, I want to report safety concerns about passengers
  - *Acceptance:* In-app incident report form, submitted to support team
  - *Effort:* 5 points

---

### Technical Infrastructure Stories
**Priority: CRITICAL (enablers for all features)**

- Set up AWS infrastructure (EC2, RDS, S3, CloudFront)
  - *Effort:* 13 points

- Implement REST API with Node.js/Express
  - *Effort:* 13 points

- Set up PostgreSQL database with PostGIS for location queries
  - *Effort:* 8 points

- Implement real-time WebSocket connections for live tracking
  - *Effort:* 13 points

- Integrate Mapbox SDK for maps and navigation
  - *Effort:* 8 points

- Implement offline map pre-download and storage
  - *Effort:* 13 points

- Orange Money Web Payment API integration
  - *Effort:* 13 points

- SMS notification service (Twilio or Africa's Talking)
  - *Effort:* 5 points

- Push notification system (Firebase Cloud Messaging)
  - *Effort:* 5 points

**Total MVP Story Points: ~280 points**  
**Estimated Velocity: 40-50 points per 2-week sprint**  
**Estimated Duration: 6 sprints (12 weeks / 3 months)**

---

## Phase 2 Story Map (Months 4-6)

**Goal:** Enhance core experience, expand payment options, improve navigation  
**Success Metrics:** 1,000 drivers, 25,000 riders, 30% digital payment adoption

### User Activity 5: Advanced Payments

#### Epic: Multi-Provider Mobile Money
**Priority: HIGH**

**User Stories:**
- As a rider, I want to pay with MTN MoMo so I have an alternative to Orange Money
  - *Acceptance:* MTN MoMo integration works smoothly, <1% failure rate
  - *Effort:* 13 points

- As a rider, I want an in-app wallet where I can store funds for faster checkout
  - *Acceptance:* Wallet can be funded via Orange/MTN, balance shown on home screen
  - *Effort:* 13 points

- As a rider, I want to deposit and withdraw from my wallet using mobile money
  - *Acceptance:* Deposits instant, withdrawals within 1 hour
  - *Effort:* 8 points

#### Epic: Digital Receipts & Expense Tracking
**Priority: MEDIUM**

**User Stories:**
- As a business rider, I want detailed digital receipts for every trip for expense reimbursement
  - *Acceptance:* Receipt includes company tax ID, all required fields, sent via email
  - *Effort:* 5 points

- As a business rider, I want to export my trip history as CSV for expense reports
  - *Acceptance:* One-click export, includes all trips in date range
  - *Effort:* 3 points

---

### User Activity 6: Better Navigation

#### Epic: Landmark Database
**Priority: HIGH**

**User Stories:**
- As a rider, I want to select pickup/dropoff from a list of landmarks (mosques, markets, schools)
  - *Acceptance:* 500+ landmarks in database, searchable, categories
  - *Effort:* 8 points

- As a rider, I want to describe my location with a photo so the driver can see my surroundings
  - *Acceptance:* Photo upload <5MB, visible to driver immediately
  - *Effort:* 5 points

- As a rider, I want to send a voice note describing where I am
  - *Acceptance:* 30-second voice note, auto-transcribed for driver
  - *Effort:* 8 points

#### Epic: Driver Map Improvements
**Priority: MEDIUM**

**User Stories:**
- As a driver, I want to report missing roads or incorrect map data
  - *Acceptance:* Simple form, submitted to OSM community
  - *Effort:* 5 points

- As a driver, I want to mark frequent pickup spots (hotels, universities, markets)
  - *Acceptance:* Personal saved locations, shareable with other drivers
  - *Effort:* 3 points

---

### User Activity 7: Enhanced Experience

#### Epic: Scheduled Rides
**Priority: HIGH**

**User Stories:**
- As a rider, I want to schedule a ride up to 24 hours in advance for airport trips
  - *Acceptance:* Scheduled rides guaranteed, driver assigned 30 min before pickup
  - *Effort:* 13 points

- As a rider, I want to set up recurring rides (e.g., Monday 7 AM to university)
  - *Acceptance:* Weekly schedule saved, auto-books rides
  - *Effort:* 8 points

#### Epic: Referral Program
**Priority: HIGH**

**User Stories:**
- As a rider, I want to refer friends and get discounts for each successful referral
  - *Acceptance:* Referral code in app, 20% off next 3 rides for referrer
  - *Effort:* 8 points

- As a new rider, I want to use a referral code for 50% off my first ride
  - *Acceptance:* Code validation, discount auto-applied
  - *Effort:* 5 points

#### Epic: Favorite Locations & Drivers
**Priority: MEDIUM**

**User Stories:**
- As a rider, I want to save favorite locations (home, work) for quick booking
  - *Acceptance:* Up to 5 saved locations, one-tap selection
  - *Effort:* 3 points

- As a rider, I want to request my favorite driver for important trips
  - *Acceptance:* Driver favoriting works, priority matching when available
  - *Effort:* 8 points

**Total Phase 2 Story Points: ~120 points**  
**Estimated Duration: 3 sprints (6 weeks / 1.5 months)**

---

## Sprint Planning

### Sprint Structure
- **Duration:** 2 weeks per sprint
- **Ceremonies:** Daily standup, sprint planning, sprint review, retrospective
- **Team:** 2 mobile developers, 1 backend developer, 1 QA, 1 designer, 1 PM
- **Velocity Target:** 40-50 story points per sprint

---

### Sprint 1: Foundation (Weeks 1-2)

**Goal:** Project setup, authentication, basic UI

**Stories:**
- AWS infrastructure setup (13 pts)
- API foundation with Node.js/Express (13 pts)
- PostgreSQL + PostGIS setup (8 pts)
- Rider phone verification (3 pts)
- Driver registration form (5 pts)
- Basic UI scaffolding (React Native) (8 pts)

**Total: 50 points**

**Deliverables:**
- Working development environment
- Rider can register and verify phone
- Driver can submit registration
- Basic navigation structure in apps

---

### Sprint 2: Mapping & Matching (Weeks 3-4)

**Goal:** Core mapping and ride matching functionality

**Stories:**
- Mapbox SDK integration (8 pts)
- Pin-drop pickup implementation (5 pts)
- What3Words integration (3 pts)
- Destination selection (5 pts)
- Ride matching algorithm (13 pts)
- Real-time WebSocket setup (13 pts)

**Total: 47 points**

**Deliverables:**
- Riders can set pickup/dropoff via pin-drop
- System matches riders with nearest drivers
- Real-time connection established

---

### Sprint 3: Rider Booking Flow (Weeks 5-6)

**Goal:** Complete rider booking experience

**Stories:**
- Price calculation engine (8 pts)
- Ride confirmation UI (3 pts)
- Driver profile display (3 pts)
- Real-time driver tracking (8 pts)
- In-app chat (8 pts)
- Trip sharing (5 pts)
- Emergency SOS button (8 pts)

**Total: 43 points**

**Deliverables:**
- Riders can book rides end-to-end
- Real-time tracking works
- Safety features functional

---

### Sprint 4: Driver App Core (Weeks 7-8)

**Goal:** Driver can accept rides and navigate

**Stories:**
- Driver onboarding flow (8 pts)
- Ride request notification (5 pts)
- Accept/reject functionality (3 pts)
- Navigation to pickup (13 pts)
- Offline map download (13 pts)
- Trip completion (5 pts)

**Total: 47 points**

**Deliverables:**
- Drivers can receive and accept trips
- Navigation works offline
- Trip lifecycle complete

---

### Sprint 5: Payments & Earnings (Weeks 9-10)

**Goal:** Payment processing and driver payouts

**Stories:**
- Cash payment confirmation (3 pts)
- Orange Money integration (13 pts)
- Digital receipt generation (5 pts)
- Driver earnings dashboard (8 pts)
- Daily payout automation (13 pts)

**Total: 42 points**

**Deliverables:**
- Both payment methods work
- Drivers receive daily payouts
- Receipts sent automatically

---

### Sprint 6: Polish & Launch Prep (Weeks 11-12)

**Goal:** Bug fixes, testing, pilot preparation

**Stories:**
- Rating system (rider + driver) (3 pts + 3 pts)
- SMS notifications (5 pts)
- Push notifications (5 pts)
- Trip history view (5 pts)
- Performance optimization (8 pts)
- Bug fixes from testing (13 pts)
- Pilot program setup (5 pts)

**Total: 47 points**

**Deliverables:**
- All MVP features working smoothly
- Performance optimized for low-end devices
- 50-driver pilot program ready to launch

---

## Acceptance Criteria

### Definition of Ready (Before Sprint Planning)
- User story clearly written with "As a [role], I want [feature] so that [benefit]"
- Acceptance criteria defined
- Story estimated (story points assigned)
- Dependencies identified
- Designs completed (if UI-related)
- Technical approach discussed

### Definition of Done (Before Story Closes)
- Code written and peer-reviewed
- Unit tests written (>80% coverage for backend)
- Integration tests pass
- Manually tested on Android and iOS
- Works on low-end devices (2GB RAM, slow connection)
- Works offline (if applicable)
- No critical or high-severity bugs
- Deployed to staging environment
- Product owner approval received
- Documentation updated (if needed)

### User Acceptance Testing (UAT)
- **Beta Testing:** 20 riders, 10 drivers (2 weeks before public launch)
- **Pilot Program:** 100 riders, 50 drivers (final month of development)
- **Success Criteria for UAT:**
  - >90% can complete booking flow without help
  - >80% successfully complete first trip
  - <5% technical issue rate
  - >4.0 average satisfaction rating

---

## Risk Management

### Technical Risks

**Risk:** Offline maps too large for low-storage devices  
**Mitigation:** Progressive download (download only areas driver frequents), compress map tiles

**Risk:** Orange Money API downtime causes payment failures  
**Mitigation:** Redundancy (MTN MoMo backup), cash always available, retry logic

**Risk:** GPS inaccurate in urban canyon areas  
**Mitigation:** Fused location provider (GPS + WiFi + cell tower), Kalman filtering

### Product Risks

**Risk:** Insufficient driver supply causes long wait times  
**Mitigation:** Aggressive driver recruitment, fleet partnerships, referral bonuses

**Risk:** Riders don't trust new platform  
**Mitigation:** First-ride discounts, safety features prominent, testimonials from pilot users

**Risk:** Competitors launch before us  
**Mitigation:** Fast MVP timeline (3 months), focus on local partnerships they can't replicate

---

## Conclusion

This story map provides a clear path from user goals to specific features across two development phases:

- **Phase 1 (Months 1-3):** MVP launch with core ride-hailing functionality
- **Phase 2 (Months 4-6):** Enhanced experience with better payments, navigation, and features

Every story ties back to a user journey step and includes clear acceptance criteria. The sprint plan provides a realistic timeline with team capacity considerations.

**Next Steps:**
1. Refine story estimates with development team
2. Begin Sprint 1 with foundation work
3. Weekly sprint reviews to validate progress
4. Monthly stakeholder demos
5. Continuous user testing throughout development
