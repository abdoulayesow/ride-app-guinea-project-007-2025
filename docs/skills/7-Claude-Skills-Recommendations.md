# Recommended Claude Skills for Building Pssst
## Custom Skills to Accelerate Development

**Date:** December 2025  
**Project:** Pssst - Guinea Ride-Hailing Application

---

## 📚 Table of Contents

1. [Overview](#overview)
2. [Immediate Priority Skills](#immediate-priority-skills)
3. [Development Phase Skills](#development-phase-skills)
4. [Testing & Quality Skills](#testing--quality-skills)
5. [Deployment & Operations Skills](#deployment--operations-skills)
6. [Skill Implementation Examples](#skill-implementation-examples)
7. [How to Create These Skills](#how-to-create-these-skills)

---

## Overview

Claude skills are knowledge packages that extend Claude's capabilities with specialized expertise, best practices, and workflow patterns. For building Pssst, you should create custom skills that encode:

- Your specific tech stack decisions (React Native, Node.js, PostgreSQL)
- Best practices for ride-hailing applications
- Guinea-specific implementation patterns (offline-first, mobile money, etc.)
- Code patterns and architectures you want to follow consistently
- Integration guides for third-party services

**Benefits:**
- ✅ Consistent code quality across the team
- ✅ Faster development (Claude knows your patterns)
- ✅ Reduced errors (best practices encoded)
- ✅ Better onboarding (new developers can ask Claude)
- ✅ Knowledge preservation (tribal knowledge documented)

---

## Immediate Priority Skills

### 1. React Native Mobile Development Skill

**Purpose:** Encode best practices for building Pssst's mobile apps (Rider & Driver)

**What it should contain:**

```markdown
# React Native for Pssst

## Project Structure
/src
  /components      # Reusable UI components
  /screens         # Screen components
  /navigation      # React Navigation setup
  /store           # Redux store, slices
  /services        # API clients, utilities
  /hooks           # Custom React hooks
  /assets          # Images, fonts
  /localization    # i18n files

## Key Libraries
- React Native 0.72+
- TypeScript
- Redux Toolkit + RTK Query
- React Navigation 6.x
- Mapbox GL Native
- WatermelonDB (offline storage)
- Socket.IO client

## Code Patterns

### Screen Component Template
```typescript
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';
import { useNavigation } from '@react-navigation/native';

interface HomeScreenProps {
  // Define props
}

export const HomeScreen: React.FC<HomeScreenProps> = () => {
  const navigation = useNavigation();

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Pssst Home</Text>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#ffffff',
  },
  title: {
    fontSize: 28,
    fontWeight: '700',
    color: '#1e40af',
  },
});
```

### API Call Pattern (RTK Query)
```typescript
import { createApi, fetchBaseQuery } from '@reduxjs/toolkit/query/react';

export const rideApi = createApi({
  reducerPath: 'rideApi',
  baseQuery: fetchBaseQuery({
    baseUrl: process.env.API_URL,
    prepareHeaders: (headers, { getState }) => {
      const token = (getState() as RootState).auth.token;
      if (token) {
        headers.set('authorization', `Bearer ${token}`);
      }
      return headers;
    },
  }),
  endpoints: (builder) => ({
    requestRide: builder.mutation({
      query: (rideData) => ({
        url: '/rides',
        method: 'POST',
        body: rideData,
      }),
    }),
  }),
});
```

## Performance Optimizations
- Use React.memo for expensive components
- FlatList for long lists (virtualization)
- Image optimization (react-native-fast-image)
- Debounce search inputs (500ms)
- Lazy load heavy screens

## Offline-First Patterns
- WatermelonDB for local storage
- Queue failed API calls
- Sync when connection restored
- Show offline indicator

## Testing Requirements
- Unit tests for utilities/hooks
- Integration tests for API calls
- E2E tests for critical flows (Detox)
- Minimum 70% code coverage
```

**When to use:** Whenever building React Native components, screens, or features

---

### 2. Node.js Backend API Skill

**Purpose:** Standardize backend API development patterns

**What it should contain:**

```markdown
# Node.js Backend for Pssst

## Tech Stack
- Node.js 18 LTS
- Express.js
- TypeScript
- PostgreSQL (pg + pg-pool)
- Redis (ioredis)
- Socket.IO
- Bull (job queue)

## Project Structure
/src
  /routes          # API routes
  /controllers     # Request handlers
  /services        # Business logic
  /models          # Database models
  /middleware      # Auth, validation, etc.
  /utils           # Helpers
  /config          # Configuration
  /workers         # Background jobs

## API Endpoint Template
```typescript
// routes/rides.ts
import { Router } from 'express';
import { authenticate } from '../middleware/auth';
import { validateRequest } from '../middleware/validation';
import { RideController } from '../controllers/ride';

const router = Router();

router.post(
  '/rides',
  authenticate,
  validateRequest(rideRequestSchema),
  RideController.createRide
);

export default router;

// controllers/ride.ts
export class RideController {
  static async createRide(req: Request, res: Response) {
    try {
      const userId = req.user.id;
      const rideData = req.body;
      
      const ride = await RideService.createRide(userId, rideData);
      
      res.status(201).json({
        success: true,
        data: ride,
      });
    } catch (error) {
      res.status(500).json({
        success: false,
        error: error.message,
      });
    }
  }
}
```

## Database Patterns

### PostgreSQL Connection Pool
```typescript
import { Pool } from 'pg';

export const pool = new Pool({
  host: process.env.DB_HOST,
  port: parseInt(process.env.DB_PORT),
  database: process.env.DB_NAME,
  user: process.env.DB_USER,
  password: process.env.DB_PASSWORD,
  max: 20,
  idleTimeoutMillis: 30000,
  connectionTimeoutMillis: 2000,
});
```

### Query Helper
```typescript
export async function query(text: string, params?: any[]) {
  const start = Date.now();
  const result = await pool.query(text, params);
  const duration = Date.now() - start;
  
  console.log('Executed query', { text, duration, rows: result.rowCount });
  return result;
}
```

## Error Handling
- Use custom error classes
- Centralized error middleware
- Log all errors (Winston)
- Don't expose internal errors to clients

## Security
- Helmet.js for headers
- Rate limiting (express-rate-limit)
- Input validation (express-validator)
- SQL injection prevention (parameterized queries)
- JWT authentication
- CORS configuration

## Background Jobs (Bull)
```typescript
import Queue from 'bull';

export const payoutQueue = new Queue('payouts', {
  redis: {
    host: process.env.REDIS_HOST,
    port: parseInt(process.env.REDIS_PORT),
  },
});

payoutQueue.process(async (job) => {
  const { driverId, amount } = job.data;
  await processDriverPayout(driverId, amount);
});

// Schedule daily payouts
payoutQueue.add(
  { driverId: 'xxx', amount: 100000 },
  { delay: 3600000 } // 1 hour
);
```
```

**When to use:** Whenever building backend APIs, database queries, or services

---

### 3. Database Schema & Migration Skill

**Purpose:** Maintain consistent database design and migration practices

**What it should contain:**

```markdown
# PostgreSQL Database for Pssst

## Schema Design Principles
- Use UUIDs for primary keys (gen_random_uuid())
- Add created_at and updated_at to all tables
- Use ENUM types for status fields
- Index foreign keys
- Use PostGIS for geospatial data

## Migration Pattern
```sql
-- migrations/001_create_users_table.sql
-- Up
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  phone_number VARCHAR(20) UNIQUE NOT NULL,
  full_name VARCHAR(255),
  role VARCHAR(20) NOT NULL CHECK (role IN ('rider', 'driver', 'admin')),
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_users_phone ON users(phone_number);
CREATE INDEX idx_users_role ON users(role);

-- Down
DROP TABLE users;
```

## Common Queries

### Find Nearby Drivers
```sql
SELECT 
  d.id,
  d.current_location,
  ST_Distance(
    d.current_location::geography,
    ST_SetSRID(ST_MakePoint($1, $2), 4326)::geography
  ) AS distance_meters
FROM drivers d
WHERE 
  d.is_online = TRUE 
  AND d.is_available = TRUE
  AND ST_DWithin(
    d.current_location::geography,
    ST_SetSRID(ST_MakePoint($1, $2), 4326)::geography,
    5000  -- 5km radius
  )
ORDER BY distance_meters ASC
LIMIT 10;
```

### Trip History with Aggregates
```sql
SELECT 
  DATE(created_at) as date,
  COUNT(*) as total_trips,
  SUM(final_price) as total_revenue,
  AVG(distance_km) as avg_distance
FROM rides
WHERE driver_id = $1
  AND status = 'completed'
  AND created_at >= NOW() - INTERVAL '30 days'
GROUP BY DATE(created_at)
ORDER BY date DESC;
```

## Performance Tips
- Use EXPLAIN ANALYZE for slow queries
- Add indexes on frequently queried columns
- Use materialized views for complex aggregates
- Partition large tables by date
- Use connection pooling
```

**When to use:** When creating database schemas, writing queries, or optimizing performance

---

### 4. Payment Integration Skill (Orange Money & MTN MoMo)

**Purpose:** Encode payment integration patterns specific to Guinea

**What it should contain:**

```markdown
# Payment Integration for Pssst

## Orange Money Web Payment API

### Authentication
```typescript
import axios from 'axios';

async function getOrangeMoneyToken() {
  const response = await axios.post(
    'https://api.orange.com/oauth/v2/token',
    {
      grant_type: 'client_credentials',
    },
    {
      auth: {
        username: process.env.ORANGE_CLIENT_ID,
        password: process.env.ORANGE_CLIENT_SECRET,
      },
    }
  );
  
  return response.data.access_token;
}
```

### Initiate Payment
```typescript
async function initiateOrangeMoneyPayment(
  amount: number,
  phoneNumber: string,
  orderId: string
) {
  const token = await getOrangeMoneyToken();
  
  const response = await axios.post(
    'https://api.orange.com/orange-money-webpay/gn/v1/webpayment',
    {
      merchant_key: process.env.ORANGE_MERCHANT_KEY,
      currency: 'GNF',
      order_id: orderId,
      amount: amount,
      return_url: `${process.env.API_URL}/webhooks/orange-money/return`,
      cancel_url: `${process.env.API_URL}/webhooks/orange-money/cancel`,
      notif_url: `${process.env.API_URL}/webhooks/orange-money/notify`,
      lang: 'fr',
      reference: `PSSST-${orderId}`,
    },
    {
      headers: {
        Authorization: `Bearer ${token}`,
        'Content-Type': 'application/json',
      },
    }
  );
  
  return {
    paymentToken: response.data.payment_token,
    paymentUrl: response.data.payment_url,
  };
}
```

### Webhook Handler
```typescript
app.post('/webhooks/orange-money/notify', async (req, res) => {
  const { order_id, status, txnid } = req.body;
  
  if (status === 'SUCCESS') {
    await updateRidePayment(order_id, {
      status: 'completed',
      transactionId: txnid,
      provider: 'orange_money',
    });
  } else {
    await updateRidePayment(order_id, {
      status: 'failed',
    });
  }
  
  res.status(200).send('OK');
});
```

## MTN Mobile Money API

### Collection Request
```typescript
import { v4 as uuidv4 } from 'uuid';

async function requestMTNPayment(
  amount: number,
  phoneNumber: string,
  externalId: string
) {
  const referenceId = uuidv4();
  
  const response = await axios.post(
    `https://proxy.momoapi.mtn.com/collection/v1_0/requesttopay`,
    {
      amount: amount.toString(),
      currency: 'GNF',
      externalId: externalId,
      payer: {
        partyIdType: 'MSISDN',
        partyId: phoneNumber.replace('+224', '224'),
      },
      payerMessage: 'Paiement Pssst',
      payeeNote: `Course ${externalId}`,
    },
    {
      headers: {
        'X-Reference-Id': referenceId,
        'X-Target-Environment': process.env.MTN_ENVIRONMENT,
        'Ocp-Apim-Subscription-Key': process.env.MTN_SUBSCRIPTION_KEY,
        Authorization: `Bearer ${await getMTNToken()}`,
      },
    }
  );
  
  return referenceId;
}
```

## Error Handling
- Retry failed payments (3 attempts)
- Log all payment attempts
- Send SMS notifications
- Refund process for failed transactions
- Manual reconciliation for disputes

## Testing
- Use sandbox environments
- Test with small amounts first
- Verify webhook signatures
- Monitor transaction success rates
```

**When to use:** When implementing payment features or debugging payment issues

---

### 5. Mapbox & Navigation Skill

**Purpose:** Standardize map and navigation implementation

**What it should contain:**

```markdown
# Mapbox Integration for Pssst

## Setup

### Install Dependencies
```bash
npm install @react-native-mapbox-gl/maps
npm install @mapbox/mapbox-sdk
```

### Configuration
```typescript
import Mapbox from '@react-native-mapbox-gl/maps';

Mapbox.setAccessToken(process.env.MAPBOX_ACCESS_TOKEN);
Mapbox.setConnected(true);
```

## Map Component
```typescript
import MapboxGL from '@react-native-mapbox-gl/maps';

export const PssstMap = () => {
  return (
    <MapboxGL.MapView
      style={{ flex: 1 }}
      styleURL={MapboxGL.StyleURL.Street}
      zoomLevel={13}
      centerCoordinate={[-13.6785, 9.5091]} // Conakry
    >
      {/* User location */}
      <MapboxGL.UserLocation
        visible={true}
        showsUserHeadingIndicator={true}
      />
      
      {/* Pickup marker */}
      <MapboxGL.MarkerView
        id="pickup"
        coordinate={pickupCoords}
      >
        <View style={styles.marker}>
          <Text>A</Text>
        </View>
      </MapboxGL.MarkerView>
      
      {/* Route line */}
      <MapboxGL.ShapeSource
        id="routeSource"
        shape={{
          type: 'Feature',
          geometry: {
            type: 'LineString',
            coordinates: routeCoordinates,
          },
        }}
      >
        <MapboxGL.LineLayer
          id="routeLine"
          style={{
            lineColor: '#1e40af',
            lineWidth: 4,
          }}
        />
      </MapboxGL.ShapeSource>
    </MapboxGL.MapView>
  );
};
```

## Offline Maps
```typescript
import Mapbox from '@react-native-mapbox-gl/maps';

async function downloadConakryMap() {
  const bounds = [
    [-13.7549, 9.4510],  // Southwest
    [-13.6284, 9.5919],  // Northeast
  ];
  
  const progressListener = (offlineRegion, status) => {
    console.log(`Download progress: ${status.percentage}%`);
  };
  
  const errorListener = (offlineRegion, err) => {
    console.error('Download error:', err);
  };
  
  await Mapbox.offlineManager.createPack(
    {
      name: 'Conakry',
      styleURL: Mapbox.StyleURL.Street,
      bounds: bounds,
      minZoom: 10,
      maxZoom: 16,
    },
    progressListener,
    errorListener
  );
}
```

## Directions API
```typescript
import MapboxClient from '@mapbox/mapbox-sdk/services/directions';

const directionsClient = MapboxClient({
  accessToken: process.env.MAPBOX_ACCESS_TOKEN,
});

async function getRoute(origin: [number, number], destination: [number, number]) {
  const response = await directionsClient
    .getDirections({
      profile: 'driving',
      waypoints: [
        { coordinates: origin },
        { coordinates: destination },
      ],
      geometries: 'geojson',
      language: ['fr'],
      steps: true,
      overview: 'full',
    })
    .send();
  
  const route = response.body.routes[0];
  
  return {
    coordinates: route.geometry.coordinates,
    distance: route.distance, // meters
    duration: route.duration, // seconds
    steps: route.legs[0].steps,
  };
}
```

## What3Words Integration
```typescript
async function convertToWhat3Words(lat: number, lng: number) {
  const response = await axios.get(
    'https://api.what3words.com/v3/convert-to-3wa',
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

async function convertFromWhat3Words(words: string) {
  const response = await axios.get(
    'https://api.what3words.com/v3/convert-to-coordinates',
    {
      params: {
        words: words,
        key: process.env.WHAT3WORDS_API_KEY,
      },
    }
  );
  
  return {
    lat: response.data.coordinates.lat,
    lng: response.data.coordinates.lng,
  };
}
```

## Performance
- Cache map tiles
- Limit marker count (<100 visible)
- Simplify routes for long distances
- Use clustering for many markers
```

**When to use:** When implementing maps, navigation, or location features

---

## Development Phase Skills

### 6. WebSocket & Real-Time Communication Skill

**Purpose:** Standardize Socket.IO patterns for real-time features

**Key topics:**
- Server setup and authentication
- Room management (user rooms, driver zones)
- Event patterns (driver location updates, ride status)
- Reconnection handling
- Fallback to HTTP polling
- Error handling and logging

### 7. State Management (Redux) Skill

**Purpose:** Consistent Redux patterns across the app

**Key topics:**
- Store configuration
- Slice patterns (auth, ride, map, payment)
- RTK Query setup
- Selectors and memoization
- Async thunks
- Middleware (offline queue)

### 8. Authentication & Security Skill

**Purpose:** Secure authentication and authorization patterns

**Key topics:**
- JWT generation and validation
- Token refresh logic
- Secure storage (Keychain/Keystore)
- Password hashing (bcrypt)
- Role-based access control
- API rate limiting
- Input sanitization

---

## Testing & Quality Skills

### 9. Testing Strategy Skill

**Purpose:** Comprehensive testing guidelines

**Key topics:**
- Unit testing (Jest)
- Integration testing (Supertest for API)
- E2E testing (Detox for mobile)
- Test coverage requirements (70%+)
- Mocking strategies
- Continuous integration

Example content:
```markdown
## Unit Test Template
```typescript
import { calculatePrice } from '../utils/pricing';

describe('calculatePrice', () => {
  it('should calculate correct price for 5km trip', () => {
    const result = calculatePrice(5, 15);
    expect(result).toBe(16000); // 5000 base + 6000 distance + 3000 time
  });
  
  it('should apply minimum fare', () => {
    const result = calculatePrice(0.5, 2);
    expect(result).toBe(8000); // Minimum fare
  });
});
```

## API Integration Test
```typescript
import request from 'supertest';
import app from '../app';

describe('POST /api/v1/rides', () => {
  it('should create a new ride request', async () => {
    const response = await request(app)
      .post('/api/v1/rides')
      .set('Authorization', `Bearer ${validToken}`)
      .send({
        pickupLat: 9.5091,
        pickupLng: -13.6785,
        dropoffLat: 9.5150,
        dropoffLng: -13.6800,
      });
    
    expect(response.status).toBe(201);
    expect(response.body.success).toBe(true);
    expect(response.body.data.id).toBeDefined();
  });
});
```
```

### 10. Code Quality & Linting Skill

**Purpose:** Maintain consistent code style

**Key topics:**
- ESLint configuration
- Prettier setup
- TypeScript strict mode
- Code review checklist
- Git commit conventions
- Pre-commit hooks (Husky)

---

## Deployment & Operations Skills

### 11. AWS Deployment Skill

**Purpose:** Standardize cloud infrastructure and deployment

**Key topics:**
- EC2 instance setup and configuration
- RDS PostgreSQL setup (Multi-AZ)
- S3 bucket policies
- CloudFront CDN configuration
- Route 53 DNS management
- Auto-scaling groups
- Load balancer configuration
- CI/CD pipeline (GitHub Actions)

Example content:
```markdown
## EC2 Instance Setup
```bash
# Install Node.js
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs

# Install PM2
sudo npm install -g pm2

# Clone repository
git clone https://github.com/yourusername/pssst-api.git
cd pssst-api

# Install dependencies
npm ci --production

# Start with PM2
pm2 start ecosystem.config.js
pm2 save
pm2 startup
```

## Database Backup
```bash
# Automated daily backups
0 2 * * * pg_dump -U pssst_user pssst_db | gzip > /backups/pssst_$(date +\%Y\%m\%d).sql.gz
```
```

### 12. Monitoring & Observability Skill

**Purpose:** Track application health and performance

**Key topics:**
- CloudWatch metrics and alarms
- Application logging (Winston)
- Error tracking (Sentry)
- Performance monitoring (DataDog)
- Uptime monitoring
- Database query performance
- API response times
- User analytics (Mixpanel)

---

## Skill Implementation Examples

### Example 1: Complete React Native Skill

Here's what a full skill file might look like:

```markdown
# React Native Development for Pssst

## Overview
This skill contains best practices, patterns, and guidelines for developing Pssst's React Native mobile applications (Rider and Driver apps).

## Tech Stack
- React Native 0.72+
- TypeScript 5.0+
- Redux Toolkit + RTK Query
- React Navigation 6.x
- Mapbox GL Native
- WatermelonDB
- Socket.IO Client

## Project Structure
```
/PssstApp
  /android            # Android native code
  /ios                # iOS native code
  /src
    /assets           # Images, fonts
      /images
      /fonts
    /components       # Reusable components
      /buttons
      /inputs
      /cards
      /common
    /screens          # Screen components
      /rider
      /driver
      /shared
    /navigation       # Navigation configuration
    /store            # Redux store
      /slices
      /api
    /services         # API clients, utilities
    /hooks            # Custom hooks
    /localization     # i18n files
    /types            # TypeScript types
    /utils            # Helper functions
    /constants        # App constants
```

## Component Patterns

### Functional Component Template
```typescript
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';
import { colors, spacing, typography } from '@/constants/theme';

interface ComponentNameProps {
  title: string;
  onPress?: () => void;
}

export const ComponentName: React.FC<ComponentNameProps> = ({
  title,
  onPress,
}) => {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>{title}</Text>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    padding: spacing.md,
    backgroundColor: colors.surface,
  },
  title: {
    fontSize: typography.sizes.h2,
    fontWeight: typography.weights.bold,
    color: colors.primary,
  },
});
```

### Custom Hook Pattern
```typescript
import { useState, useEffect } from 'react';
import Geolocation from 'react-native-geolocation-service';

export const useLocation = () => {
  const [location, setLocation] = useState(null);
  const [error, setError] = useState(null);

  useEffect(() => {
    Geolocation.getCurrentPosition(
      (position) => {
        setLocation({
          lat: position.coords.latitude,
          lng: position.coords.longitude,
        });
      },
      (err) => setError(err),
      { enableHighAccuracy: true, timeout: 15000 }
    );
  }, []);

  return { location, error };
};
```

## State Management (Redux Toolkit)

### Slice Template
```typescript
import { createSlice, PayloadAction } from '@reduxjs/toolkit';

interface RideState {
  currentRide: Ride | null;
  status: 'idle' | 'requesting' | 'active' | 'completed';
}

const initialState: RideState = {
  currentRide: null,
  status: 'idle',
};

export const rideSlice = createSlice({
  name: 'ride',
  initialState,
  reducers: {
    setCurrentRide: (state, action: PayloadAction<Ride>) => {
      state.currentRide = action.payload;
    },
    updateRideStatus: (state, action: PayloadAction<RideStatus>) => {
      if (state.currentRide) {
        state.currentRide.status = action.payload;
      }
    },
  },
});

export const { setCurrentRide, updateRideStatus } = rideSlice.actions;
export default rideSlice.reducer;
```

### RTK Query API
```typescript
import { createApi, fetchBaseQuery } from '@reduxjs/toolkit/query/react';

export const pssstApi = createApi({
  reducerPath: 'pssstApi',
  baseQuery: fetchBaseQuery({
    baseUrl: process.env.API_URL,
    prepareHeaders: (headers, { getState }) => {
      const token = (getState() as RootState).auth.token;
      if (token) {
        headers.set('authorization', `Bearer ${token}`);
      }
      return headers;
    },
  }),
  tagTypes: ['Ride', 'User', 'Payment'],
  endpoints: (builder) => ({
    requestRide: builder.mutation<Ride, RideRequest>({
      query: (rideData) => ({
        url: '/rides',
        method: 'POST',
        body: rideData,
      }),
      invalidatesTags: ['Ride'],
    }),
    getRideHistory: builder.query<Ride[], void>({
      query: () => '/rides',
      providesTags: ['Ride'],
    }),
  }),
});

export const { useRequestRideMutation, useGetRideHistoryQuery } = pssstApi;
```

## Performance Best Practices

### 1. List Optimization
```typescript
import { FlatList } from 'react-native';

const TripHistory = ({ trips }) => {
  const renderItem = useCallback(({ item }) => (
    <TripCard trip={item} />
  ), []);

  const keyExtractor = useCallback((item) => item.id, []);

  return (
    <FlatList
      data={trips}
      renderItem={renderItem}
      keyExtractor={keyExtractor}
      windowSize={10}
      maxToRenderPerBatch={10}
      removeClippedSubviews={true}
      initialNumToRender={10}
    />
  );
};
```

### 2. Memoization
```typescript
import { useMemo } from 'react';

const ExpensiveComponent = ({ data }) => {
  const processedData = useMemo(() => {
    return data.map(item => /* expensive operation */);
  }, [data]);

  return <View>{/* render */}</View>;
};
```

### 3. Image Optimization
```typescript
import FastImage from 'react-native-fast-image';

<FastImage
  source={{
    uri: driverPhotoUrl,
    priority: FastImage.priority.normal,
  }}
  resizeMode={FastImage.resizeMode.cover}
  style={styles.driverPhoto}
/>
```

## Offline Storage (WatermelonDB)

### Model Definition
```typescript
import { Model } from '@nozbe/watermelondb';
import { field, date } from '@nozbe/watermelondb/decorators';

export class Trip extends Model {
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
```

### Database Operations
```typescript
import database from './database';

// Create
const newTrip = await database.write(async () => {
  return await database.collections
    .get('trips')
    .create(trip => {
      trip.riderId = userId;
      trip.price = 18000;
      trip.status = 'completed';
    });
});

// Query
const trips = await database.collections
  .get('trips')
  .query(Q.where('rider_id', userId))
  .fetch();
```

## Testing

### Component Test
```typescript
import { render, fireEvent } from '@testing-library/react-native';
import { PrimaryButton } from './PrimaryButton';

describe('PrimaryButton', () => {
  it('renders correctly', () => {
    const { getByText } = render(
      <PrimaryButton title="Request Ride" onPress={() => {}} />
    );
    expect(getByText('Request Ride')).toBeTruthy();
  });

  it('calls onPress when tapped', () => {
    const onPress = jest.fn();
    const { getByText } = render(
      <PrimaryButton title="Request Ride" onPress={onPress} />
    );
    fireEvent.press(getByText('Request Ride'));
    expect(onPress).toHaveBeenCalled();
  });
});
```

## Localization

### Setup
```typescript
import i18n from 'i18next';
import { initReactI18next } from 'react-i18next';
import fr from './locales/fr.json';

i18n
  .use(initReactI18next)
  .init({
    resources: {
      fr: { translation: fr },
    },
    lng: 'fr',
    fallbackLng: 'fr',
    interpolation: { escapeValue: false },
  });
```

### Usage
```typescript
import { useTranslation } from 'react-i18next';

const HomeScreen = () => {
  const { t } = useTranslation();
  
  return <Text>{t('where_going')}</Text>;
};
```

## Common Pitfalls to Avoid

1. **Don't mutate state directly** - Always use Redux actions
2. **Don't use inline functions in renders** - Causes unnecessary re-renders
3. **Don't forget to unsubscribe** - Clean up listeners in useEffect
4. **Don't ignore performance warnings** - Profile with React DevTools
5. **Don't hardcode strings** - Use localization from day 1

## Code Review Checklist

- [ ] TypeScript types defined correctly
- [ ] No `any` types (use `unknown` if necessary)
- [ ] Components memoized where appropriate
- [ ] Styles extracted to StyleSheet
- [ ] No hardcoded strings (use i18n)
- [ ] Error handling implemented
- [ ] Loading states handled
- [ ] Offline behavior considered
- [ ] Tests written
- [ ] Accessibility labels added

## Resources

- [React Native Docs](https://reactnative.dev/)
- [Redux Toolkit Docs](https://redux-toolkit.js.org/)
- [React Navigation Docs](https://reactnavigation.org/)
- [WatermelonDB Docs](https://watermelondb.dev/)
```

This is a complete, production-ready skill that Claude can reference whenever working on React Native code for Pssst.

---

## How to Create These Skills

### Using the Skill Creator

You have access to the `skill-creator` skill at `/mnt/skills/examples/skill-creator/SKILL.md`. Here's how to use it:

1. **Read the skill-creator guide first:**
```
I want to create a new skill for [topic]. Can you first read the skill-creator guide?
```

2. **Create the skill:**
```
Create a React Native development skill for the Pssst app with:
- Component patterns
- State management (Redux)
- API integration (RTK Query)
- Performance optimization
- Testing patterns
- Code review checklist
```

3. **Save it to the user skills directory:**
Skills should be saved in `/mnt/skills/user/` with this structure:
```
/mnt/skills/user/
  /react-native-pssst/
    SKILL.md           # Main skill file
    README.md          # Overview (optional)
    /examples/         # Code examples (optional)
```

### Skill File Template

Every skill should follow this structure:

```markdown
# [Skill Name]

## Overview
Brief description of what this skill helps with

## When to Use This Skill
Specific scenarios where this skill applies

## Key Concepts
Core concepts and principles

## Patterns & Templates
Reusable code patterns

## Best Practices
Do's and don'ts

## Common Pitfalls
Mistakes to avoid

## Examples
Real-world code examples

## Testing
How to test code using these patterns

## Resources
Links to documentation
```

---

## Priority Implementation Plan

### Week 1: Core Development Skills
1. ✅ React Native Mobile Development Skill
2. ✅ Node.js Backend API Skill  
3. ✅ Database Schema & Migration Skill

### Week 2: Integration Skills
4. ✅ Payment Integration Skill (Orange Money & MTN)
5. ✅ Mapbox & Navigation Skill
6. ✅ WebSocket & Real-Time Communication Skill

### Week 3: Quality & Deployment
7. ✅ Testing Strategy Skill
8. ✅ Code Quality & Linting Skill
9. ✅ AWS Deployment Skill

### Week 4: Operations
10. ✅ Monitoring & Observability Skill
11. ✅ State Management (Redux) Skill
12. ✅ Authentication & Security Skill

---

## Additional Recommended Skills

### 13. Guinea-Specific Implementation Patterns

**Purpose:** Encode knowledge about Guinea's unique requirements

**Topics:**
- Offline-first architecture patterns
- Mobile money integration specifics
- Low-end device optimization
- French localization guidelines
- Cultural considerations (Islamic holidays, etc.)
- Local payment agent workflows

### 14. Ride-Hailing Domain Logic

**Purpose:** Business logic specific to ride-hailing

**Topics:**
- Ride matching algorithms
- Price calculation formulas
- Driver rating systems
- Trip cancellation policies
- Surge pricing (if implemented)
- Driver earnings calculation
- Payout schedules

### 15. Mobile Permissions & Privacy

**Purpose:** Handle sensitive permissions correctly

**Topics:**
- Location permission flows
- Camera/photo permissions
- Push notification setup
- Privacy policy implementation
- GDPR compliance (if applicable)
- Data retention policies

---

## Measuring Skill Effectiveness

Track these metrics to see if skills are helping:

1. **Development Speed**
   - Time to implement new features
   - Time to fix bugs
   - Code review cycle time

2. **Code Quality**
   - Bug rate (bugs per 1000 lines)
   - Test coverage
   - Code duplication

3. **Team Consistency**
   - Style guide violations
   - Pattern adherence
   - Documentation completeness

4. **Developer Experience**
   - Time to onboard new developers
   - Questions asked in code reviews
   - Stack Overflow searches (should decrease)

---

## Conclusion

Creating these custom Claude skills will:

✅ **Accelerate development** - Claude knows your exact patterns  
✅ **Improve consistency** - Everyone follows same best practices  
✅ **Reduce errors** - Common pitfalls documented and avoided  
✅ **Enable knowledge sharing** - Tribal knowledge made explicit  
✅ **Simplify onboarding** - New developers can ask Claude  

**Start with the top 5 priority skills and add more as you go!**

---

## Next Steps

1. Read `/mnt/skills/examples/skill-creator/SKILL.md`
2. Create React Native skill first (highest priority)
3. Create Node.js Backend skill second
4. Add integration skills as you implement features
5. Iterate and improve skills based on team feedback

**Remember:** Skills are living documents. Update them as you learn what works!
