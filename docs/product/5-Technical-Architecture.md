# Technical Architecture Documentation
## Pssst - Guinea Ride-Hailing & Delivery Application

**Version:** 1.0  
**Date:** December 2025

---

## Table of Contents
1. [System Architecture Overview](#system-architecture-overview)
2. [Technology Stack](#technology-stack)
3. [Mobile Applications](#mobile-applications)
4. [Backend Services](#backend-services)
5. [Database Design](#database-design)
6. [Payment Integration](#payment-integration)
7. [Mapping & Navigation](#mapping--navigation)
8. [Real-Time Communication](#real-time-communication)
9. [Security & Authentication](#security--authentication)
10. [Infrastructure & DevOps](#infrastructure--devops)
11. [Offline Functionality](#offline-functionality)
12. [Performance Optimization](#performance-optimization)
13. [Monitoring & Analytics](#monitoring--analytics)

---

## System Architecture Overview

### High-Level Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    CLIENT APPLICATIONS                       │
│  ┌──────────────────┐              ┌──────────────────┐    │
│  │   Rider App      │              │   Driver App     │    │
│  │  (React Native)  │              │  (React Native)  │    │
│  │   iOS + Android  │              │   iOS + Android  │    │
│  └──────────────────┘              └──────────────────┘    │
└─────────────────────────────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────┐
│                      API GATEWAY                             │
│  (Load Balancer, Rate Limiting, SSL Termination)           │
└─────────────────────────────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────┐
│                   BACKEND SERVICES                           │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │
│  │   REST API   │  │  WebSocket   │  │   Worker     │     │
│  │  (Node.js)   │  │   Server     │  │   Queue      │     │
│  └──────────────┘  └──────────────┘  └──────────────┘     │
└─────────────────────────────────────────────────────────────┘
                          │
        ┌─────────────────┼─────────────────┐
        ▼                 ▼                 ▼
┌──────────────┐  ┌──────────────┐  ┌──────────────┐
│  PostgreSQL  │  │    Redis     │  │   MongoDB    │
│  (Primary DB)│  │   (Cache)    │  │   (Logs)     │
└──────────────┘  └──────────────┘  └──────────────┘
                          │
        ┌─────────────────┼─────────────────┐
        ▼                 ▼                 ▼
┌──────────────┐  ┌──────────────┐  ┌──────────────┐
│ Orange Money │  │    Mapbox    │  │   Twilio     │
│     API      │  │     API      │  │   (SMS)      │
└──────────────┘  └──────────────┘  └──────────────┘
```

### Design Principles

1. **Offline-First:** App must function with intermittent connectivity
2. **Scalability:** Horizontal scaling for all services
3. **Reliability:** 99.9% uptime target with graceful degradation
4. **Security:** End-to-end encryption, PCI-DSS compliance for payments
5. **Performance:** <3s page load, <500ms API response time
6. **Localization:** Support for French, Susu, Pular, Malinké

---

## Technology Stack

### Mobile Applications

**Framework:** React Native 0.72+  
**Language:** TypeScript  
**State Management:** Redux Toolkit + RTK Query  
**Navigation:** React Navigation 6.x  
**Maps:** Mapbox GL Native  
**Offline Storage:** WatermelonDB (SQLite wrapper)  
**HTTP Client:** Axios with retry logic  
**Real-time:** Socket.IO client  
**Push Notifications:** Firebase Cloud Messaging (FCM)

**Key Libraries:**
- `react-native-geolocation-service` - GPS location
- `react-native-permissions` - Runtime permissions
- `react-native-maps` - Map display
- `react-native-fs` - File system (offline maps)
- `react-native-background-geolocation` - Background tracking
- `react-native-camera` - Photo uploads (driver docs, location sharing)

**Build Tools:**
- Android: Gradle, Android Studio
- iOS: Xcode, CocoaPods
- CI/CD: GitHub Actions

### Backend Services

**Runtime:** Node.js 18 LTS  
**Framework:** Express.js  
**Language:** TypeScript  
**API Style:** REST + WebSocket  
**Authentication:** JWT (JSON Web Tokens)  
**Real-time:** Socket.IO  
**Task Queue:** Bull (Redis-backed)  
**Cron Jobs:** node-cron  

**Key Libraries:**
- `express-validator` - Request validation
- `bcryptjs` - Password hashing
- `jsonwebtoken` - JWT generation/validation
- `helmet` - Security headers
- `cors` - CORS configuration
- `winston` - Logging
- `pm2` - Process management

### Databases

**Primary Database:** PostgreSQL 14  
- **Purpose:** Transactional data (users, trips, payments)
- **Extensions:** PostGIS for geospatial queries
- **Connection Pool:** pg-pool with max 20 connections

**Cache Layer:** Redis 7  
- **Purpose:** Session storage, real-time data, rate limiting
- **Features:** Pub/Sub for real-time updates, sorted sets for leaderboards

**Log Storage:** MongoDB 6  
- **Purpose:** Application logs, analytics events
- **Retention:** 90 days, then archive to S3

### Third-Party Services

**Payments:**
- Orange Money Web Payment API
- MTN MoMo API (Phase 2)
- Lengo Pay (Guinea fintech partner)

**Mapping:**
- Mapbox GL JS & Native SDKs
- What3Words API
- OpenStreetMap data (Geofabrik extracts)

**Communication:**
- Twilio (SMS, Voice)
- Firebase Cloud Messaging (Push notifications)
- SendGrid (Email)

**Infrastructure:**
- AWS (EC2, RDS, S3, CloudFront, Route 53)
- Cloudflare (CDN, DDoS protection)

---

## Mobile Applications

### Rider App Architecture

```
┌─────────────────────────────────────────────┐
│         PRESENTATION LAYER                  │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐ │
│  │  Screens │  │Components│  │Navigation│ │
│  └──────────┘  └──────────┘  └──────────┘ │
└─────────────────────────────────────────────┘
                    │
┌─────────────────────────────────────────────┐
│         STATE MANAGEMENT                    │
│  ┌──────────────────────────────────────┐  │
│  │  Redux Store (RTK)                   │  │
│  │  - User slice                        │  │
│  │  - Ride slice                        │  │
│  │  - Map slice                         │  │
│  │  - Payment slice                     │  │
│  └──────────────────────────────────────┘  │
└─────────────────────────────────────────────┘
                    │
┌─────────────────────────────────────────────┐
│         DATA LAYER                          │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐ │
│  │ REST API │  │WebSocket │  │  Local   │ │
│  │  (RTK)   │  │(Socket.IO)│  │   DB     │ │
│  └──────────┘  └──────────┘  └──────────┘ │
└─────────────────────────────────────────────┘
```

**Key Screens:**
1. Welcome/Onboarding
2. Phone Verification
3. Home (Map with pickup/dropoff)
4. Ride Request (price estimate)
5. Waiting (driver approaching)
6. In-Trip (live tracking)
7. Payment
8. Rating
9. Trip History
10. Profile/Settings

**Offline Capabilities:**
- View trip history
- Access saved locations
- View offline maps (pre-downloaded)
- Queue actions (sync when online)

### Driver App Architecture

Similar to Rider App with additional features:

**Key Screens:**
1. Welcome/Onboarding
2. Document Upload
3. Orientation Scheduling
4. Dashboard (online/offline toggle)
5. Ride Requests (incoming)
6. Navigation (to pickup)
7. In-Trip (to destination)
8. Trip Completion
9. Earnings Dashboard
10. Profile/Documents

**Background Services:**
- GPS tracking (updates every 5 seconds when online)
- Ride request listening (WebSocket)
- Offline map updates (WiFi only)

---

## Backend Services

### REST API Endpoints

#### Authentication
```
POST   /api/v1/auth/register           # Phone number registration
POST   /api/v1/auth/verify-otp         # OTP verification
POST   /api/v1/auth/login              # Login
POST   /api/v1/auth/refresh-token      # JWT refresh
```

#### Users
```
GET    /api/v1/users/me                # Current user profile
PATCH  /api/v1/users/me                # Update profile
POST   /api/v1/users/me/avatar         # Upload avatar
GET    /api/v1/users/:id               # Public profile (ratings only)
```

#### Rides (Rider)
```
POST   /api/v1/rides                   # Request ride
GET    /api/v1/rides/:id               # Get ride details
PATCH  /api/v1/rides/:id/cancel        # Cancel ride
POST   /api/v1/rides/:id/rate          # Rate driver
GET    /api/v1/rides                   # Trip history
```

#### Rides (Driver)
```
GET    /api/v1/driver/rides/pending    # Available rides
POST   /api/v1/driver/rides/:id/accept # Accept ride
POST   /api/v1/driver/rides/:id/reject # Reject ride
PATCH  /api/v1/driver/rides/:id/pickup # Confirm pickup
PATCH  /api/v1/driver/rides/:id/complete # Complete trip
```

#### Payments
```
POST   /api/v1/payments/orange-money   # Process Orange Money payment
POST   /api/v1/payments/cash           # Confirm cash payment
GET    /api/v1/payments/receipts/:id   # Get receipt
```

#### Locations
```
GET    /api/v1/locations/landmarks     # Popular landmarks
GET    /api/v1/locations/search        # Search locations
POST   /api/v1/locations/reverse       # Reverse geocode
```

#### Driver Operations
```
PATCH  /api/v1/driver/status           # Toggle online/offline
GET    /api/v1/driver/earnings         # Earnings dashboard
POST   /api/v1/driver/documents        # Upload documents
GET    /api/v1/driver/payouts          # Payout history
```

### WebSocket Events

#### Client → Server
```
driver:location_update        # GPS coordinates
driver:online                 # Go online
driver:offline                # Go offline
ride:request_accepted         # Driver accepts
ride:arrived_pickup           # Driver at pickup
ride:started                  # Trip started
ride:completed                # Trip completed
```

#### Server → Client
```
ride:request                  # New ride request (to driver)
ride:driver_assigned          # Driver matched (to rider)
ride:driver_location          # Driver GPS update (to rider)
ride:status_update            # Status change
payment:processed             # Payment confirmed
```

### Ride Matching Algorithm

```typescript
interface MatchingCriteria {
  maxSearchRadius: number;      // 5km initial radius
  maxDrivers: number;            // Top 10 nearest drivers
  responseTimeout: number;       // 15 seconds
  preferredDriverRating: number; // 4.5+
}

async function matchRide(ride: Ride): Promise<Driver | null> {
  // 1. Find nearby available drivers using PostGIS
  const drivers = await findNearbyDrivers(
    ride.pickupLocation,
    SEARCH_RADIUS,
    { isOnline: true, isAvailable: true }
  );

  // 2. Sort by time-to-pickup (not just distance)
  const rankedDrivers = await rankByTimeToPickup(drivers, ride.pickupLocation);

  // 3. Send request to top 10 drivers simultaneously
  const acceptedDriver = await broadcastRideRequest(rankedDrivers.slice(0, 10), ride);

  // 4. Return first driver to accept (within 15 seconds)
  return acceptedDriver;
}
```

### Price Calculation

```typescript
interface PriceFactors {
  basePrice: number;          // 5,000 GNF
  pricePerKm: number;         // 1,200 GNF/km
  pricePerMinute: number;     // 200 GNF/min
  minimumFare: number;        // 8,000 GNF
  serviceFee: number;         // 10% platform commission
}

function calculatePrice(distance: number, duration: number): number {
  const distanceCost = distance * PRICE_PER_KM;
  const timeCost = duration * PRICE_PER_MINUTE;
  const subtotal = BASE_PRICE + distanceCost + timeCost;
  
  return Math.max(subtotal, MINIMUM_FARE);
}
```

---

## Database Design

### PostgreSQL Schema

#### users table
```sql
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  phone_number VARCHAR(20) UNIQUE NOT NULL,
  full_name VARCHAR(255),
  email VARCHAR(255),
  avatar_url TEXT,
  role VARCHAR(20) NOT NULL CHECK (role IN ('rider', 'driver', 'admin')),
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_users_phone ON users(phone_number);
CREATE INDEX idx_users_role ON users(role);
```

#### drivers table
```sql
CREATE TABLE drivers (
  id UUID PRIMARY KEY REFERENCES users(id),
  license_number VARCHAR(50) UNIQUE NOT NULL,
  vehicle_make VARCHAR(50),
  vehicle_model VARCHAR(50),
  vehicle_year INTEGER,
  vehicle_color VARCHAR(30),
  license_plate VARCHAR(20) UNIQUE,
  rating DECIMAL(3,2) DEFAULT 5.00,
  total_trips INTEGER DEFAULT 0,
  is_online BOOLEAN DEFAULT FALSE,
  is_available BOOLEAN DEFAULT FALSE,
  current_location GEOGRAPHY(POINT, 4326),
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_drivers_online ON drivers(is_online) WHERE is_online = TRUE;
CREATE INDEX idx_drivers_location ON drivers USING GIST(current_location);
```

#### rides table
```sql
CREATE TABLE rides (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  rider_id UUID REFERENCES users(id),
  driver_id UUID REFERENCES drivers(id),
  status VARCHAR(20) CHECK (status IN (
    'requested', 'accepted', 'driver_arrived', 
    'in_progress', 'completed', 'cancelled'
  )),
  pickup_location GEOGRAPHY(POINT, 4326) NOT NULL,
  pickup_address TEXT,
  pickup_what3words VARCHAR(255),
  dropoff_location GEOGRAPHY(POINT, 4326) NOT NULL,
  dropoff_address TEXT,
  dropoff_what3words VARCHAR(255),
  distance_km DECIMAL(10,2),
  duration_minutes INTEGER,
  estimated_price DECIMAL(10,2),
  final_price DECIMAL(10,2),
  payment_method VARCHAR(20) CHECK (payment_method IN ('cash', 'orange_money', 'mtn_momo', 'wallet')),
  payment_status VARCHAR(20) CHECK (payment_status IN ('pending', 'completed', 'failed')),
  rider_rating INTEGER CHECK (rider_rating BETWEEN 1 AND 5),
  driver_rating INTEGER CHECK (driver_rating BETWEEN 1 AND 5),
  created_at TIMESTAMP DEFAULT NOW(),
  completed_at TIMESTAMP
);

CREATE INDEX idx_rides_rider ON rides(rider_id);
CREATE INDEX idx_rides_driver ON rides(driver_id);
CREATE INDEX idx_rides_status ON rides(status);
CREATE INDEX idx_rides_created ON rides(created_at DESC);
```

#### payments table
```sql
CREATE TABLE payments (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  ride_id UUID REFERENCES rides(id),
  amount DECIMAL(10,2) NOT NULL,
  currency VARCHAR(3) DEFAULT 'GNF',
  payment_method VARCHAR(20) NOT NULL,
  payment_provider VARCHAR(50),
  transaction_id VARCHAR(255) UNIQUE,
  status VARCHAR(20) CHECK (status IN ('pending', 'completed', 'failed', 'refunded')),
  created_at TIMESTAMP DEFAULT NOW(),
  completed_at TIMESTAMP
);

CREATE INDEX idx_payments_ride ON payments(ride_id);
CREATE INDEX idx_payments_status ON payments(status);
```

#### driver_earnings table
```sql
CREATE TABLE driver_earnings (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  driver_id UUID REFERENCES drivers(id),
  ride_id UUID REFERENCES rides(id),
  gross_amount DECIMAL(10,2) NOT NULL,
  commission_amount DECIMAL(10,2) NOT NULL,
  commission_percentage DECIMAL(5,2) DEFAULT 10.00,
  net_amount DECIMAL(10,2) NOT NULL,
  payout_status VARCHAR(20) CHECK (payout_status IN ('pending', 'paid', 'failed')),
  payout_date DATE,
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_driver_earnings_driver ON driver_earnings(driver_id);
CREATE INDEX idx_driver_earnings_payout_date ON driver_earnings(payout_date);
```

### Geospatial Queries

#### Find nearby drivers
```sql
SELECT 
  d.id,
  d.current_location,
  ST_Distance(
    d.current_location::geography,
    ST_SetSRID(ST_MakePoint(:longitude, :latitude), 4326)::geography
  ) AS distance_meters
FROM drivers d
WHERE 
  d.is_online = TRUE 
  AND d.is_available = TRUE
  AND ST_DWithin(
    d.current_location::geography,
    ST_SetSRID(ST_MakePoint(:longitude, :latitude), 4326)::geography,
    5000  -- 5km radius
  )
ORDER BY distance_meters ASC
LIMIT 10;
```

---

## Payment Integration

### Orange Money Web Payment API

**Base URL:** `https://api.orange.com/orange-money-webpay/`  
**Authentication:** OAuth 2.0 Client Credentials

**Integration Flow:**
```
1. Rider confirms booking with Orange Money payment
2. Backend initiates payment request to Orange API
3. Orange API returns payment token
4. User receives USSD prompt on phone (dial *144#)
5. User enters PIN on phone to authorize
6. Orange API sends webhook to confirm payment
7. Backend confirms ride and notifies driver
```

**Implementation:**

```typescript
import axios from 'axios';

class OrangeMoneyService {
  private baseUrl = 'https://api.orange.com/orange-money-webpay/';
  private accessToken: string;

  async initializePayment(amount: number, phoneNumber: string, orderId: string) {
    // 1. Get OAuth token
    const token = await this.getAccessToken();

    // 2. Initiate payment
    const response = await axios.post(
      `${this.baseUrl}v1/webpayment`,
      {
        merchant_key: process.env.ORANGE_MERCHANT_KEY,
        currency: 'GNF',
        order_id: orderId,
        amount: amount,
        return_url: `${process.env.API_URL}/webhooks/orange-money`,
        cancel_url: `${process.env.API_URL}/webhooks/orange-money/cancel`,
        notif_url: `${process.env.API_URL}/webhooks/orange-money/notify`,
        lang: 'fr',
        reference: `RIDE-${orderId}`,
      },
      {
        headers: {
          Authorization: `Bearer ${token}`,
          'Content-Type': 'application/json',
        },
      }
    );

    return response.data;
  }

  async verifyPayment(paymentToken: string) {
    const response = await axios.get(
      `${this.baseUrl}v1/webpayment/${paymentToken}/status`,
      {
        headers: {
          Authorization: `Bearer ${this.accessToken}`,
        },
      }
    );

    return response.data.status === 'SUCCESS';
  }
}
```

### MTN Mobile Money API (Phase 2)

**Base URL:** `https://proxy.momoapi.mtn.com/`  
**Products:** Collection (receive payments), Disbursement (send payouts)

**Key Endpoints:**
- `POST /collection/v1_0/requesttopay` - Request payment from rider
- `POST /disbursement/v1_0/transfer` - Send payout to driver

---

## Mapping & Navigation

### Mapbox Integration

**Services Used:**
- **Maps SDK** - Display interactive maps
- **Navigation SDK** - Turn-by-turn directions
- **Geocoding API** - Address search and reverse geocoding
- **Directions API** - Route calculation
- **Static Images API** - Map thumbnails for receipts

**Offline Maps:**

```typescript
import Mapbox from '@react-native-mapbox-gl/maps';

// Download offline map for Conakry
async function downloadOfflineMap() {
  const bounds = [
    [-13.7549, 9.4510],  // Southwest corner
    [-13.6284, 9.5919],  // Northeast corner
  ];

  const offlinePack = await Mapbox.offlineManager.createPack({
    name: 'Conakry',
    styleURL: Mapbox.StyleURL.Street,
    bounds: bounds,
    minZoom: 10,
    maxZoom: 16,
  });

  // Monitor download progress
  offlinePack.onProgress((percentage) => {
    console.log(`Download: ${percentage}%`);
  });
}
```

### What3Words Integration

**API:** `https://api.what3words.com/v3/`

**Usage:**
```typescript
async function convertToWhat3Words(lat: number, lng: number): Promise<string> {
  const response = await axios.get(
    `https://api.what3words.com/v3/convert-to-3wa`,
    {
      params: {
        coordinates: `${lat},${lng}`,
        language: 'fr',
        key: process.env.WHAT3WORDS_API_KEY,
      },
    }
  );

  return response.data.words; // e.g., "opera.cellblock.limb"
}
```

### OpenStreetMap Data

**Source:** Geofabrik (https://download.geofabrik.de/africa/guinea.html)  
**Update Frequency:** Weekly  
**Processing:**

```bash
# Download latest Guinea OSM data
wget https://download.geofabrik.de/africa/guinea-latest.osm.pbf

# Import to PostgreSQL with PostGIS
osm2pgsql -d pssst_db -c guinea-latest.osm.pbf

# Extract landmarks (POIs)
psql -d pssst_db -c "
  SELECT name, amenity, ST_X(way) as lng, ST_Y(way) as lat
  FROM planet_osm_point
  WHERE amenity IN ('mosque', 'school', 'hospital', 'market', 'bank')
    AND name IS NOT NULL;
"
```

---

## Real-Time Communication

### WebSocket Architecture

**Technology:** Socket.IO over WebSocket

**Connection Flow:**
```
1. Client connects with JWT token in query params
2. Server validates token and authenticates user
3. Client joins room based on user ID
4. Server sends/receives events to/from specific rooms
5. Connection maintained with heartbeat (every 25 seconds)
```

**Implementation:**

```typescript
// Server
import { Server } from 'socket.io';

const io = new Server(server, {
  cors: { origin: '*' },
  transports: ['websocket', 'polling'],
});

io.use((socket, next) => {
  const token = socket.handshake.auth.token;
  const user = verifyJWT(token);
  if (user) {
    socket.data.userId = user.id;
    socket.data.userRole = user.role;
    next();
  } else {
    next(new Error('Authentication error'));
  }
});

io.on('connection', (socket) => {
  // Join user-specific room
  socket.join(`user:${socket.data.userId}`);

  // Driver goes online
  socket.on('driver:online', async () => {
    await updateDriverStatus(socket.data.userId, true);
    socket.join('drivers:online');
  });

  // Driver location update
  socket.on('driver:location_update', async (data) => {
    const { lat, lng } = data;
    await updateDriverLocation(socket.data.userId, lat, lng);
    
    // Broadcast to rider if on active trip
    const activeRide = await getActiveRide(socket.data.userId);
    if (activeRide) {
      io.to(`user:${activeRide.rider_id}`).emit('ride:driver_location', { lat, lng });
    }
  });

  // Ride request acceptance
  socket.on('ride:accept', async (data) => {
    const { rideId } = data;
    const ride = await acceptRide(rideId, socket.data.userId);
    
    // Notify rider
    io.to(`user:${ride.rider_id}`).emit('ride:driver_assigned', {
      driver: await getDriverProfile(socket.data.userId),
      estimatedArrival: ride.estimated_arrival,
    });
  });
});
```

**Reconnection Strategy:**

```typescript
// Client
const socket = io(API_URL, {
  auth: { token: userToken },
  reconnection: true,
  reconnectionAttempts: 5,
  reconnectionDelay: 1000,
  reconnectionDelayMax: 5000,
});

socket.on('connect_error', (error) => {
  console.error('Connection failed:', error);
  // Fall back to HTTP polling for ride status
  startPollingRideStatus();
});

socket.on('reconnect', (attemptNumber) => {
  console.log('Reconnected after', attemptNumber, 'attempts');
  // Re-join rooms and sync state
  socket.emit('driver:online');
});
```

---

## Security & Authentication

### JWT Authentication

**Token Structure:**
```json
{
  "userId": "uuid",
  "role": "rider|driver|admin",
  "phoneNumber": "+224XXXXXXXXX",
  "iat": 1234567890,
  "exp": 1234571490
}
```

**Token Lifecycle:**
- **Access Token:** 1 hour expiry
- **Refresh Token:** 30 days expiry
- Stored in secure storage (Keychain on iOS, Keystore on Android)

**Implementation:**

```typescript
import jwt from 'jsonwebtoken';

function generateTokens(user: User) {
  const accessToken = jwt.sign(
    { userId: user.id, role: user.role, phoneNumber: user.phone_number },
    process.env.JWT_SECRET,
    { expiresIn: '1h' }
  );

  const refreshToken = jwt.sign(
    { userId: user.id },
    process.env.JWT_REFRESH_SECRET,
    { expiresIn: '30d' }
  );

  return { accessToken, refreshToken };
}

function verifyAccessToken(token: string) {
  try {
    return jwt.verify(token, process.env.JWT_SECRET);
  } catch (error) {
    throw new Error('Invalid or expired token');
  }
}
```

### Data Encryption

- **In Transit:** TLS 1.3 for all API calls
- **At Rest:** AES-256 encryption for sensitive fields (phone numbers, payment info)
- **Passwords:** bcrypt with salt rounds = 10

### Security Headers

```typescript
import helmet from 'helmet';

app.use(helmet({
  contentSecurityPolicy: {
    directives: {
      defaultSrc: ["'self'"],
      styleSrc: ["'self'", "'unsafe-inline'"],
      scriptSrc: ["'self'"],
      imgSrc: ["'self'", "data:", "https:"],
    },
  },
  hsts: {
    maxAge: 31536000,
    includeSubDomains: true,
    preload: true,
  },
}));
```

### Rate Limiting

```typescript
import rateLimit from 'express-rate-limit';

const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100, // 100 requests per window
  message: 'Too many requests, please try again later',
  standardHeaders: true,
  legacyHeaders: false,
});

app.use('/api/', limiter);
```

---

## Infrastructure & DevOps

### AWS Architecture

```
┌─────────────────────────────────────────────────────┐
│                    Route 53                         │
│              (DNS, Health Checks)                   │
└─────────────────────────────────────────────────────┘
                        │
                        ▼
┌─────────────────────────────────────────────────────┐
│                  CloudFront                         │
│         (CDN for static assets, SSL)                │
└─────────────────────────────────────────────────────┘
                        │
                        ▼
┌─────────────────────────────────────────────────────┐
│            Application Load Balancer                │
│       (Auto-scaling, Health Checks)                 │
└─────────────────────────────────────────────────────┘
                        │
          ┌─────────────┴─────────────┐
          ▼                           ▼
┌──────────────────┐         ┌──────────────────┐
│   EC2 Instance   │         │   EC2 Instance   │
│  (Node.js API)   │         │  (Node.js API)   │
│   Auto Scaling   │         │   Auto Scaling   │
└──────────────────┘         └──────────────────┘
          │                           │
          └─────────────┬─────────────┘
                        ▼
┌─────────────────────────────────────────────────────┐
│                    RDS PostgreSQL                   │
│         (Multi-AZ, Read Replicas)                   │
└─────────────────────────────────────────────────────┘
```

**Components:**
- **EC2:** t3.medium instances (2 vCPU, 4GB RAM) - Auto-scaling group (min 2, max 10)
- **RDS:** db.t3.medium PostgreSQL 14 - Multi-AZ for high availability
- **ElastiCache:** Redis cache cluster (cache.t3.micro)
- **S3:** Document storage (driver licenses, vehicle photos) - Lifecycle policies for old data
- **CloudFront:** CDN for static assets (maps tiles, images)
- **Route 53:** DNS management with health checks

### CI/CD Pipeline

**Tools:** GitHub Actions

**Pipeline Stages:**

```yaml
name: Deploy to Production

on:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
      - run: npm ci
      - run: npm run test
      - run: npm run lint

  build:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: npm ci
      - run: npm run build
      - uses: actions/upload-artifact@v3
        with:
          name: build
          path: dist/

  deploy:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/download-artifact@v3
      - name: Deploy to EC2
        run: |
          ssh -i ${{ secrets.EC2_KEY }} ubuntu@${{ secrets.EC2_HOST }} '
            cd /var/www/pssst-api
            git pull origin main
            npm ci --production
            pm2 reload ecosystem.config.js
          '
```

### Monitoring & Logging

**Tools:**
- **CloudWatch:** AWS metrics, log aggregation
- **Sentry:** Error tracking and crash reporting
- **DataDog:** APM (Application Performance Monitoring)
- **Uptime Robot:** Uptime monitoring, alerts

**Key Metrics:**
- API response time (p50, p95, p99)
- Error rate
- Active WebSocket connections
- Database connection pool usage
- Queue depth (for background jobs)
- GPS location update frequency

---

## Offline Functionality

### Offline-First Strategy

**Critical Features That Work Offline:**
1. View pre-downloaded maps
2. View trip history
3. View saved locations
4. Read cached driver/rider profiles
5. Queue actions (to sync when online)

**Implementation:**

```typescript
// Redux middleware for offline queue
const offlineMiddleware = (store) => (next) => (action) => {
  const isOnline = store.getState().network.isOnline;

  if (!isOnline && action.meta?.queueIfOffline) {
    // Queue action for later
    store.dispatch({
      type: 'QUEUE_ACTION',
      payload: action,
    });
    return;
  }

  return next(action);
};

// Network state listener
NetInfo.addEventListener((state) => {
  if (state.isConnected) {
    // Flush queued actions
    store.dispatch({ type: 'PROCESS_QUEUE' });
  }
});
```

### Local Database (WatermelonDB)

**Schema:**

```typescript
import { Model, Database } from '@nozbe/watermelondb';

class Trip extends Model {
  static table = 'trips';
  
  @field('rider_id') riderId;
  @field('driver_id') driverId;
  @field('pickup_lat') pickupLat;
  @field('pickup_lng') pickupLng;
  @field('dropoff_lat') dropoffLat;
  @field('dropoff_lng') dropoffLng;
  @field('price') price;
  @field('status') status;
  @date('created_at') createdAt;
  
  @readonly @date('synced_at') syncedAt;
}

// Sync with backend
async function syncDatabase() {
  const lastSync = await getLastSyncTime();
  
  // Pull new data from server
  const newTrips = await api.get('/trips', { since: lastSync });
  await database.write(async () => {
    for (const tripData of newTrips) {
      await tripsCollection.create((trip) => {
        trip._raw = tripData;
      });
    }
  });
  
  await setLastSyncTime(Date.now());
}
```

---

## Performance Optimization

### Backend Optimization

**Database Optimization:**
- Connection pooling (max 20 connections)
- Proper indexes on frequently queried columns
- Query result caching (Redis)
- Read replicas for analytics queries

**API Optimization:**
- Response compression (gzip)
- Pagination (default: 20 items per page)
- Field selection (GraphQL-style partial responses)
- CDN for static assets

**Code Optimization:**
- Async/await throughout (non-blocking I/O)
- Background job queue for heavy tasks
- Lazy loading of modules
- Code splitting

### Mobile App Optimization

**Performance Targets:**
- App startup: <3 seconds
- Screen transitions: <300ms
- Map rendering: <1 second
- API calls: <500ms (p95)

**Techniques:**
- Code splitting with React.lazy()
- Image optimization (WebP format, lazy loading)
- List virtualization (FlatList with optimizations)
- Memoization of expensive computations
- Debouncing/throttling user inputs

**Bundle Size Optimization:**
```bash
# Android APK size target: <30MB
# iOS IPA size target: <40MB

# Hermes JavaScript engine (faster startup)
# ProGuard/R8 (Android code shrinking)
# Bitcode optimization (iOS)
```

---

## Monitoring & Analytics

### Application Metrics

**Key Performance Indicators:**
```typescript
// Track with Mixpanel or Amplitude
analytics.track('Ride Requested', {
  pickup_lat: ride.pickupLat,
  pickup_lng: ride.pickupLng,
  estimated_price: ride.estimatedPrice,
  payment_method: ride.paymentMethod,
});

analytics.track('Ride Completed', {
  ride_id: ride.id,
  duration_minutes: ride.duration,
  distance_km: ride.distance,
  final_price: ride.finalPrice,
  rider_rating: ride.riderRating,
});
```

**Business Metrics:**
- Daily/Weekly/Monthly active users (DAU/WAU/MAU)
- Rides per day
- Average wait time
- Driver online hours
- Revenue per ride
- Customer acquisition cost (CAC)
- Lifetime value (LTV)

### Error Tracking

**Sentry Integration:**

```typescript
import * as Sentry from '@sentry/react-native';

Sentry.init({
  dsn: process.env.SENTRY_DSN,
  environment: process.env.NODE_ENV,
  beforeSend(event, hint) {
    // Filter sensitive data
    if (event.user) {
      delete event.user.phone_number;
    }
    return event;
  },
});

// Capture errors
try {
  await processPayment(ride);
} catch (error) {
  Sentry.captureException(error, {
    tags: { payment_provider: 'orange_money' },
    contexts: { ride: { id: ride.id } },
  });
}
```

---

## Conclusion

This technical architecture provides a robust foundation for Pssst, with:

✅ **Offline-first design** for Guinea's connectivity challenges  
✅ **Scalable infrastructure** to grow from 500 to 50,000+ users  
✅ **Secure payment processing** with Orange Money and MTN MoMo  
✅ **Advanced mapping** using Mapbox, OSM, and What3Words  
✅ **Real-time communication** via WebSocket for live tracking  
✅ **Performance optimization** for low-end Android devices  
✅ **Comprehensive monitoring** for reliability and debugging  

**Next Steps:**
1. Set up AWS infrastructure
2. Implement core REST API endpoints
3. Build React Native mobile apps
4. Integrate Orange Money sandbox
5. Deploy to staging environment
6. Begin pilot testing with 50 drivers
