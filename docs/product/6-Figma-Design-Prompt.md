# Figma Design Prompt: Pssst Ride-Hailing App
## Complete UI/UX Design Brief for Guinea's First Ride-Hailing Platform

---

## 📱 Project Overview

Design a complete mobile application UI/UX for **Pssst**, Guinea's first ride-hailing and delivery platform. This app connects riders with drivers in Conakry and other Guinean cities, addressing unique local challenges like lack of street addresses, intermittent connectivity, and cash-first payment culture.

**Platform:** iOS and Android (React Native)  
**Primary Market:** Conakry, Guinea (West Africa)  
**Target Launch:** Q2 2026  
**Design Deliverables:** Complete design system + Rider App (15 screens) + Driver App (12 screens)

---

## 🎨 Brand Identity

### Brand Name: Pssst
**Meaning:** The sound you make to quietly get someone's attention - informal, friendly, distinctly African

### Brand Personality
- **Trustworthy & Safe** - Riders feel secure, drivers feel supported
- **Local & Relatable** - Built for Guinea, not a Western import
- **Modern & Tech-Forward** - Brings modern convenience to West Africa
- **Friendly & Approachable** - Warm, not corporate or cold
- **Reliable** - Works even when infrastructure fails

### Color Palette

**Primary Colors:**
- **Pssst Blue:** `#1e40af` (rgb: 30, 64, 175) - Trust, professionalism, navigation
- **Pssst Teal:** `#0d9488` (rgb: 13, 148, 136) - Growth, prosperity, secondary actions
- **Accent Orange:** `#f97316` (rgb: 249, 115, 22) - Urgency, CTAs, alerts

**Supporting Colors:**
- **Success Green:** `#10b981` (rgb: 16, 185, 129) - Confirmations, completed trips
- **Warning Yellow:** `#f59e0b` (rgb: 245, 158, 11) - Cautions, pending status
- **Error Red:** `#ef4444` (rgb: 239, 68, 68) - Errors, cancellations, SOS button
- **Neutral Gray:** `#64748b` (rgb: 100, 116, 139) - Secondary text, borders

**Background Colors:**
- **Surface:** `#ffffff` (White) - Main background
- **Surface Light:** `#f8fafc` (rgb: 248, 250, 252) - Cards, containers
- **Surface Dark:** `#1e293b` (rgb: 30, 41, 59) - Dark mode option (Phase 2)

### Typography

**Primary Font:** Inter (Sans-serif)
- Excellent readability on mobile screens
- Supports French diacritics (é, è, à, ô)
- Wide weight range (400-700)
- Free and open-source

**Font Sizes:**
- **H1 (Page Titles):** 28px / Bold (700)
- **H2 (Section Headers):** 22px / Semi-bold (600)
- **H3 (Card Titles):** 18px / Semi-bold (600)
- **Body Large:** 16px / Regular (400)
- **Body:** 14px / Regular (400)
- **Caption:** 12px / Regular (400)
- **Button Text:** 16px / Medium (500)

**Line Heights:**
- Headings: 1.2
- Body text: 1.5
- Captions: 1.4

### Visual Style

**Design Language:** Clean, modern, functional with subtle warmth

**Key Characteristics:**
- **Generous spacing** - Never cluttered, breathing room between elements
- **Rounded corners** - 8px border radius for cards, 12px for buttons (friendly, approachable)
- **Subtle shadows** - Depth without distraction (elevation: 2-4dp)
- **High contrast** - Readable in bright African sunlight
- **Bold CTAs** - Primary actions unmistakable
- **Status-driven colors** - Color communicates state (blue = active, green = complete, orange = waiting)

**Visual Inspiration:**
- Grab (Southeast Asia) - Local adaptation, clear hierarchy
- Gozem (West Africa) - Designed for African infrastructure
- Bolt - Clean, modern interface
- **Avoid:** Uber's complexity, Lyft's playfulness (too casual)

---

## 👥 Target Users & Context

### User Segments

**Riders:**
1. **University Students (24 years, female)** - Safety-conscious, price-sensitive, tech-comfortable
2. **Business Professionals (38 years, male)** - Value time, need receipts, willing to pay premium
3. **Families** - Occasional users, safety first, mixed payment preferences

**Drivers:**
1. **Full-time Drivers (32 years, male)** - Need consistent income, familiar with taxi work
2. **Part-time Drivers (27 years, female)** - Flexible schedule, safety concerns, tech-savvy

### Context & Constraints

**Infrastructure Challenges:**
- ❌ **No street addresses** - Must use pin-drop, What3Words, landmarks
- ❌ **Intermittent connectivity** - App must work offline
- ❌ **Low-end devices** - Android phones with 2GB RAM, small storage
- ❌ **Poor GPS accuracy** - Urban canyons, tall buildings interfere
- ✅ **High mobile money adoption** - Orange Money, MTN MoMo widely used
- ✅ **Strong WhatsApp culture** - Familiar with chat interfaces
- ✅ **Cash still king** - Digital payments growing but cash dominant

**User Behaviors:**
- Read left-to-right (French language)
- Comfortable with emojis and icons
- Expect immediate visual feedback
- Share locations via WhatsApp/SMS
- Distrust new platforms (need trust signals)
- Prefer visual over text (literacy varies)

---

## 📱 Rider App - Screen Requirements (15 Screens)

### 1. Welcome / Onboarding (3 screens)

**Screen 1.1: Splash Screen**
- Pssst logo centered (animated fade-in)
- Tagline: "Votre trajet, à portée de main" (Your trip, at your fingertips)
- Loading indicator below logo
- Full-bleed gradient background (blue to teal)
- **Duration:** 2 seconds

**Screen 1.2: Onboarding Carousel (3 slides)**

*Slide 1:*
- Illustration: Phone with map pin-drop
- Headline: "Pas d'adresse? Pas de problème!" (No address? No problem!)
- Description: "Marquez votre position sur la carte - nous vous trouvons partout"
- Skip button (top-right, subtle)
- Pagination dots (bottom center)

*Slide 2:*
- Illustration: Driver in car with 5-star rating
- Headline: "Conducteurs vérifiés" (Verified drivers)
- Description: "Tous nos conducteurs sont vérifiés avec photo, licence et véhicule"
- Skip button, pagination dots

*Slide 3:*
- Illustration: Phone showing Orange Money + Cash icons
- Headline: "Payez comme vous voulez" (Pay your way)
- Description: "Espèces, Orange Money ou MTN Mobile Money"
- CTA button: "Commencer" (Get Started) - Large, orange, full-width
- Sign In link below (small, subtle)

**Screen 1.3: Phone Verification**
- Header: "Entrez votre numéro" (Enter your number)
- Country selector: Guinea flag + +224 (locked, not changeable)
- Phone input: Large, numeric keyboard auto-opens
- Format: XXX XX XX XX (auto-formatting as they type)
- Info text: "Nous enverrons un code de vérification par SMS"
- CTA: "Envoyer le code" (Send code) - Disabled until valid phone number
- Terms: Small text at bottom "En continuant, vous acceptez nos Conditions et Politique de confidentialité" (links)

**Screen 1.4: OTP Verification**
- Header: "Entrez le code" (Enter the code)
- Subtext: "Code envoyé au +224 XXX XX XX XX" with "Modifier" (Edit) link
- 6-digit OTP input boxes (auto-focus, auto-advance)
- Resend code link: "Renvoyer le code (30s)" (countdown timer)
- Auto-verify when 6 digits entered (no submit button needed)
- Error state: Red border + "Code incorrect" message

**Screen 1.5: Basic Profile Setup**
- Header: "Complétez votre profil" (Complete your profile)
- Avatar upload (optional, camera icon placeholder)
- Name input: "Prénom et Nom" (First and Last name) - Required
- Email input (optional): "Email (facultatif)"
- Payment method selection:
  - Radio buttons: Cash (selected by default), Orange Money, MTN MoMo
  - Icons for each payment method
- CTA: "Continuer" (Continue)
- Skip link: "Passer pour l'instant" (subtle, top-right)

---

### 2. Home / Booking Flow (5 screens)

**Screen 2.1: Home Screen (Map View)**

*Top Bar:*
- Hamburger menu (left) - Opens profile/settings
- "Où allez-vous?" (Where are you going?) search bar
- Notification bell icon (right, with badge if unread)

*Map Area:* (Fills most of screen)
- Current location marked with blue dot + pulsing circle
- Nearby drivers shown as car icons with direction indicator
- Zoom controls (+ / -) bottom-right
- Recenter button (location crosshair icon) if user pans away

*Bottom Sheet (Collapsed):*
- Handle bar (drag to expand)
- Saved locations: 
  - "🏠 Maison" (Home) - If set
  - "💼 Travail" (Work) - If set
  - "+ Ajouter un lieu favori" (Add favorite place)
- Recent trips (show last 2 with small cards)
  - Destination name, date, price
  - Tap to repeat trip

*Floating Action Button:*
- Large orange circle, bottom-right
- Icon: Plus (+) or "Nouvelle course" (New ride)
- Tap to start booking

**Screen 2.2: Set Pickup Location**

*Map Interaction:*
- Fixed pin in center of screen (doesn't move with map)
- User drags map underneath to position pickup
- Instruction banner at top: "Déplacez la carte pour ajuster" (Move map to adjust)

*Top Search Bar:*
- "Rechercher un lieu..." (Search for a place)
- Mic icon for voice search
- Recent searches dropdown when focused

*Bottom Card:*
- What3Words address: "///opera.cellblock.limb" (auto-generated from pin)
- Street address: "Près de Grande Mosquée de Conakry" (if available via reverse geocoding)
- Landmark selector: "📍 Sélectionner un point de repère" (Select a landmark)
- Photo button: "📷 Partager une photo" (Share a photo of location)
- CTA: "Confirmer la position" (Confirm position) - Slides up to next screen

**Screen 2.3: Set Destination**

*Similar to 2.2 but with differences:*
- Header: "Où allez-vous?" (Where are you going?)
- Show pickup location as small card at top (confirmed, not editable here)
- Route line drawn from pickup to destination pin (updates as user drags)
- Distance and estimated time shown in top card
- Bottom card same as 2.2 (What3Words, address, landmark, photo)
- CTA: "Voir le prix" (See price)

**Screen 2.4: Ride Options & Price**

*Map Header:*
- Route shown with pickup (A) and destination (B) markers
- Minimap (can't interact, just visual reference)

*Ride Options:* (Scrollable horizontal cards)

*Pssst Standard* (Default, highlighted)
- Car icon + "1-3 passagers" (1-3 passengers)
- Price: "18,000 GNF" (large, bold)
- Estimated time: "Arrivée dans 5 min" (Arrival in 5 min)
- Description: "Berline confortable, climatisée" (Comfortable sedan, air-conditioned)

*Pssst Moto* (Phase 2)
- Motorcycle icon + "1 passager" 
- Price: "12,000 GNF"
- Time: "Arrivée dans 3 min"
- Description: "Rapide dans le trafic" (Fast in traffic)

*Payment Method Selector:*
- Current method shown: "💵 Espèces" (Cash) with "Modifier" (Change) link
- Tapping opens modal with payment options

*Promo Code Field:*
- Collapsed by default: "Code promo?" (Promo code?) - Expands on tap
- Input + "Appliquer" (Apply) button
- Success state: "20% de réduction appliquée!" (20% discount applied!) in green

*Bottom CTA:*
- Large button: "Demander une Pssst" (Request a Pssst)
- Safety note below: "🔒 Partagez votre trajet avec vos proches"

**Screen 2.5: Searching for Driver**

*Top Half:*
- Animated searching indicator (pulsing circles or car animation)
- Status text: "Recherche d'un conducteur..." (Searching for a driver...)
- Subtext: "Cela prend généralement moins d'une minute" (Usually takes less than a minute)

*Bottom Half:*
- Trip summary card:
  - Pickup: "Grande Mosquée" 
  - Destination: "Université Gamal Abdel Nasser"
  - Price: "18,000 GNF"
  - Payment: Cash icon
  - Edit button (small, top-right of card)

*Cancel Button:*
- Text link at bottom: "Annuler la demande" (Cancel request)
- Confirmation modal if tapped: "Êtes-vous sûr?" (Are you sure?)

---

### 3. Trip Experience (4 screens)

**Screen 3.1: Driver Assigned**

*Driver Card:* (Top, prominent)
- Driver photo (large, circular)
- Name: "Ibrahim T." (First name + initial)
- Rating: "4.8 ⭐ (324 trajets)" (324 trips)
- Vehicle: "Toyota Corolla blanche" (White Toyota Corolla)
- License plate: "GN-1234-XX"

*Action Buttons:*
- Call driver button: "📞 Appeler" (green)
- Message driver button: "💬 Message" (blue)

*Map Area:*
- Driver's current location (car icon with driver photo)
- Animated route from driver to pickup point
- ETA: Large text "5 min" at top of map
- Pickup point marked with "A"

*Bottom Card:*
- Status: "Ibrahim arrive" (Ibrahim is arriving)
- Progress: Visual timeline (Driver assigned → Arriving → Picked up → Dropped off)
  - Currently on "Arriving" (highlighted)
- Trip details (collapsible):
  - Pickup, Destination, Price, Payment method

*Emergency Button:*
- Small red SOS button (top-right)
- Tapping shows modal with:
  - "🚨 Urgence" (Emergency)
  - Options: "Appeler la police" (Call police), "Partager ma position" (Share location), "Annuler le trajet" (Cancel trip)

**Screen 3.2: Driver Arrived at Pickup**

*Notification Banner:* (Top, animated slide-down)
- "🚗 Ibrahim est arrivé!" (Ibrahim has arrived!)
- Auto-dismisses after 5 seconds

*Driver Card:* (Same as 3.1 but with update)
- Status changed to: "Le conducteur vous attend" (Driver is waiting)
- Timer: "Temps d'attente: 02:30" (Wait time: 2:30) - Counts up
- Note: After 5 minutes, may incur waiting fee

*Map:*
- Zoomed in to show pickup area
- Driver car icon stationary at pickup point
- Rider location (blue dot) if nearby

*Action Buttons:*
- Primary: "Je suis là!" (I'm here!) button
  - Tap when entering car
  - Confirms pickup to driver
- Secondary: Call/Message buttons still available

*Bottom Sheet:*
- "Où est ma Pssst?" (Where is my Pssst?)
- Car details: Make, model, color, plate
- What driver sees: Your What3Words address, landmark, photo (if shared)

**Screen 3.3: In-Trip (Active)**

*Top Bar:*
- Status: "En cours" (In progress) with green dot
- ETA: "Arrivée dans 12 min"
- Distance remaining: "3.2 km"

*Map:*
- Full-screen map showing route
- Current location updating every 5 seconds
- Route line: Gray (traveled) + Blue (remaining)
- Destination marker "B"

*Bottom Sheet:* (Swipeable, collapsed by default)

*Collapsed View:*
- Driver info bar (photo, name, rating)
- Trip progress bar
- "Voir les détails" (See details) - Swipe up to expand

*Expanded View:*
- Full trip details:
  - Pickup address
  - Destination address  
  - Distance
  - Estimated price
  - Payment method
- Share trip button: "📤 Partager le trajet"
  - Opens share sheet (WhatsApp, SMS, etc.)
  - Shares live tracking link
- Support button: "❓ Aide"

*Floating Buttons:*
- Recenter map (if panned away)
- Emergency SOS (red, top-right)

**Screen 3.4: Trip Completed**

*Celebration Moment:*
- Checkmark animation (green, circular)
- "Trajet terminé!" (Trip completed!)

*Trip Summary Card:*
- Map thumbnail: Route traveled (static image)
- Distance: "3.2 km"
- Duration: "18 minutes"
- Final price: "18,000 GNF" (large, bold)
- Breakdown (expandable):
  - Base fare: 5,000 GNF
  - Distance (3.2 km): 11,000 GNF
  - Time (18 min): 2,000 GNF
  - Service fee (10%): Included

*Payment Confirmation:*
- If cash: "Paiement en espèces confirmé" (Cash payment confirmed)
- If Orange Money: "Payé via Orange Money" with transaction ID

*Rate Your Driver:*
- Large section: "Comment était votre trajet avec Ibrahim?" (How was your trip with Ibrahim?)
- 5-star rating (tappable stars, 40px size)
- Optional feedback tags (quick taps):
  - "👍 Poli" (Polite)
  - "🚗 Conduite sûre" (Safe driving)
  - "⏰ À l'heure" (On time)
  - "🎵 Bonne ambiance" (Good vibes)
  - "❄️ Voiture propre" (Clean car)
- Optional text feedback: "Ajouter un commentaire" (collapsed)
- Tip option (Phase 2): "+ Laisser un pourboire" (Leave a tip)

*Bottom CTAs:*
- Primary: "Envoyer l'évaluation" (Submit rating)
- Secondary: "Demander un reçu" (Request receipt)
- Tertiary: "Nouvelle course" (New ride)

---

### 4. Profile & Settings (3 screens)

**Screen 4.1: Profile / Menu**

*Accessed via hamburger menu on home screen*

*Header:*
- Profile photo (circular, large)
- Name: "Aminata Diallo"
- Phone: "+224 XXX XX XX XX"
- Edit button (pencil icon, top-right)

*Menu Sections:*

*Mes courses* (My trips)
- "Historique" (History) - Trip list icon
- "Lieux favoris" (Favorite places) - Star icon  
- "Reçus" (Receipts) - Document icon

*Paiement* (Payment)
- "Modes de paiement" (Payment methods) - Credit card icon
- "Portefeuille Pssst" (Pssst wallet) - Wallet icon, shows balance
- "Codes promo" (Promo codes) - Tag icon

*Paramètres* (Settings)
- "Notifications" - Bell icon
- "Langue" (Language) - Globe icon, shows "Français"
- "Confidentialité" (Privacy) - Lock icon

*Aide* (Help)
- "Centre d'aide" (Help center) - Question mark icon
- "Signaler un problème" (Report an issue) - Flag icon
- "Nous contacter" (Contact us) - Chat icon

*Autres* (Other)
- "Partager Pssst" (Share Pssst) - Share icon
- "Conditions d'utilisation" (Terms) - Document icon
- "Version 1.0.0" - Small gray text

*Footer:*
- "Se déconnecter" (Sign out) - Red text, bottom

**Screen 4.2: Trip History**

*Header:*
- Back button (left)
- Title: "Historique des courses" (Trip history)
- Filter button (right): By date, status

*Trip List:* (Scrollable)

Each trip card shows:
- Date: "Lundi 18 déc, 08:30" (Monday Dec 18, 08:30)
- Route: "Grande Mosquée → Université" with arrow
- Driver: Small photo + "Ibrahim T."
- Price: "18,000 GNF"
- Status badge: "Terminé" (Completed) in green
- Rating: 5 stars (if rated)
- Tap to expand:
  - View route map
  - Redownload receipt
  - Report issue
  - Repeat trip button

*States:*
- Completed trips: Green badge
- Cancelled trips: Gray badge  
- Refunded trips: Orange badge with "Remboursé"

*Empty State:*
- Illustration: Empty folder
- Text: "Aucun trajet pour le moment" (No trips yet)
- CTA: "Demander votre première Pssst!"

**Screen 4.3: Payment Methods**

*Header:*
- Back button
- Title: "Modes de paiement" (Payment methods)
- Add payment button (+ icon, top-right)

*Payment Methods List:*

*Espèces* (Cash)
- Icon: 💵
- Label: "Espèces"
- Default badge: "Par défaut" (Default)
- Radio button selected

*Orange Money*
- Icon: Orange Money logo
- Label: "Orange Money"
- Number: "•••• •••• 5678"
- Radio button
- Remove link (small, right)

*MTN Mobile Money*
- Icon: MTN logo
- Label: "MTN Mobile Money"  
- Status: "Ajouter" link
- Radio button (disabled until added)

*Portefeuille Pssst*
- Icon: Wallet
- Label: "Portefeuille Pssst"
- Balance: "12,500 GNF"
- "Recharger" (Top up) link
- Radio button

*Add Payment Modal:*
- Triggered by + button or "Ajouter" link
- Title: "Ajouter Orange Money"
- Phone input: "+224 XXX XX XX XX"
- Verification: "Nous enverrons un code de confirmation"
- CTA: "Ajouter"

---

## 🚗 Driver App - Screen Requirements (12 Screens)

### 1. Driver Onboarding (4 screens)

**Screen D1.1: Driver Splash & Welcome**
- Similar to rider splash
- Tagline: "Gagnez plus, attendez moins" (Earn more, wait less)
- Illustration: Driver with car + money

**Screen D1.2: Get Started**
- Header: "Devenez conducteur Pssst" (Become a Pssst driver)
- Benefits listed:
  - "💰 Commission de 10-15% seulement" (Only 10-15% commission)
  - "📅 Paiements quotidiens" (Daily payouts)
  - "📍 Navigation hors ligne" (Offline navigation)
  - "🎯 Plus de courses, moins d'attente" (More trips, less waiting)
- Requirements:
  - "✓ Permis de conduire valide" (Valid driver's license)
  - "✓ Véhicule de 2015 ou plus récent" (2015+ vehicle)
  - "✓ Assurance valide" (Valid insurance)
- CTAs:
  - Primary: "Commencer l'inscription" (Start registration)
  - Secondary: "J'ai déjà un compte" (I already have an account)

**Screen D1.3: Document Upload**

*Multi-step form (Progress bar: 1/4)*

*Step 1: Personal Info*
- Full name
- Phone number (verified)
- Date of birth
- National ID number
- Photo of National ID (upload front + back)

*Step 2: Driver License*
- License number
- Expiry date
- License photo (upload)
- Category (A, B, C, D)

*Step 3: Vehicle Information*
- Make (dropdown: Toyota, Honda, Nissan, etc.)
- Model
- Year (2015+)
- Color
- License plate number
- Vehicle registration photo (upload)
- Insurance certificate (upload)

*Step 4: Vehicle Photos*
- Front view
- Rear view
- Interior (dashboard)
- Left side
- Right side
- Upload instructions: "Prenez des photos claires en plein jour" (Take clear photos in daylight)

*Photo Upload Component:*
- Tap to open camera OR select from gallery
- Preview before submit
- Retry button if photo unclear
- File size limit: 5MB per photo
- Compression automatic

*Bottom Navigation:*
- "Retour" (Back) button
- "Continuer" (Continue) button
- "Sauvegarder et continuer plus tard" (Save and continue later) link

**Screen D1.4: Orientation Scheduling**

*Success Banner:*
- "✅ Documents soumis!" (Documents submitted!)
- "Notre équipe les examine maintenant" (Our team is reviewing them now)
- "Cela prend généralement 24-48 heures" (Usually takes 24-48 hours)

*Next Step:*
- Header: "Planifier votre orientation" (Schedule your orientation)
- Description: "Session de 2 heures pour apprendre à utiliser l'application et rencontrer l'équipe"
  (2-hour session to learn the app and meet the team)

*Onboarding Centers:*
- Map showing 3 locations in Conakry
- List view:
  - "Centre Kaloum" - Address + "Sélectionner" button
  - "Centre Matoto" - Address + "Sélectionner" button  
  - "Centre Ratoma" - Address + "Sélectionner" button

*Date Picker:*
- Calendar view (next 2 weeks)
- Available time slots: 9 AM, 2 PM, 5 PM
- Unavailable dates grayed out

*Confirmation:*
- Selected: "Centre Kaloum, Jeudi 15 déc à 14:00"
- CTA: "Confirmer le rendez-vous" (Confirm appointment)
- Reminder: "Nous vous enverrons un SMS de rappel 24h avant"

*Status Tracking:*
- Timeline showing:
  - ✅ Documents soumis (Completed)
  - 🔄 Vérification en cours (In progress)
  - ⏳ Orientation planifiée (Scheduled)
  - ⏳ Compte activé (Pending)

---

### 2. Driver Dashboard (Main Interface)

**Screen D2.1: Dashboard (Offline State)**

*Header:*
- Pssst driver logo (small, left)
- Balance: "125,000 GNF" (large, center)
  - Subtext: "Gains aujourd'hui" (Today's earnings)
- Menu icon (right)

*Status Card:* (Prominent, center)
- Large toggle switch: "Hors ligne" (Offline) ↔ "En ligne" (Online)
- State: Currently OFF (gray)
- Text: "Passez en ligne pour recevoir des courses" (Go online to receive trips)
- Icon: Car with sleep symbol

*Today's Summary:* (Even when offline, shows previous stats)
- Grid of 4 metrics:
  - "0 courses" (0 trips) - Today
  - "0 km" (0 km) - Distance
  - "0 min" (0 min) - Online time
  - "0 GNF" (0 GNF) - Earnings

*Weekly Goals:* (Gamification)
- Progress bar: "32/50 courses cette semaine" (32/50 trips this week)
- Reward: "Complétez 50 courses = Bonus de 100,000 GNF!"
- Days remaining: "3 jours restants" (3 days left)

*Quick Actions:*
- "📊 Voir les gains" (View earnings)
- "📍 Zones demandées" (Busy areas) - Shows heat map
- "⚙️ Paramètres" (Settings)

**Screen D2.2: Dashboard (Online State)**

*Same header but status card changed:*

*Status Card:*
- Toggle: "En ligne" (Online) - Switched ON (green)
- Live indicator: Pulsing green dot + "En ligne" text
- Queue position: "Position dans la file: #3" (Queue position: #3)
- Estimated wait: "Prochaine course dans ~5 min" (Next trip in ~5 min)

*Heat Map:* (Replaces offline message)
- Small map showing demand zones
- Red/orange/yellow gradient (high to low demand)
- Current location marked
- Suggestion: "📍 Demande élevée à Kaloum" (High demand in Kaloum)

*Active Trips Counter:*
- "En attente de course..." (Waiting for trip...)
- Animation: Pulsing radar circles

*Today's Summary:* (Live updating)
- "7 courses" (7 trips)
- "42 km" (42 km)
- "3h 25min" (3h 25min online)
- "126,000 GNF" (126,000 GNF earned)

*Earnings Breakdown:* (Tap to expand)
- Fares: 140,000 GNF
- Commission (10%): -14,000 GNF
- Bonus: +0 GNF
- Net: 126,000 GNF

**Screen D2.3: Incoming Ride Request**

*Full-screen modal (slides up from bottom)*

*Top Section:*
- "Nouvelle course!" (New trip!) - Large, bold
- Countdown timer: "15s" (circular, counts down)
- Auto-reject message: "Refus automatique dans 15 secondes"

*Ride Details Card:*
- Pickup location:
  - "📍 Grande Mosquée de Conakry"
  - What3Words: "///opera.cellblock.limb"
  - Distance from you: "1.2 km (3 min)"
- Destination:
  - "📍 Université Gamal Abdel Nasser"
  - Distance: "3.8 km"
- Estimated earnings: "16,200 GNF" (after commission)
  - Gross: 18,000 GNF
  - Commission: -1,800 GNF (10%)
- Trip duration: "~15 min"
- Rider rating: "4.9 ⭐" (if available, Phase 2)

*Mini Map:*
- Shows your location, pickup (A), destination (B)
- Estimated route drawn

*Action Buttons:*
- Primary: "Accepter" (Accept) - Large, green, full-width
- Secondary: "Refuser" (Reject) - Smaller, gray, below
  - Tapping shows quick reason: "Trop loin", "En pause", "Autre"

*Sound:*
- Plays notification sound
- Vibration pattern
- Continues until accepted/rejected/timeout

---

### 3. Navigation & Trip Screens

**Screen D3.1: Navigating to Pickup**

*Status Banner:* (Top, sticky)
- "En route vers le passager" (En route to passenger)
- Timer: "Arrivée estimée: 3 min"
- Rider name: "Aminata D." with call/message buttons

*Map:* (Full screen)
- Turn-by-turn navigation
- Your location: Blue car icon (updates every 5 seconds)
- Pickup point: "A" marker with pulsing circle
- Route: Thick blue line with white border
- Next turn indicator: Arrow + "Tournez à gauche dans 200m"
- Speed: Shows current speed (optional, settings toggle)

*Rider Info Card:* (Swipeable from bottom)

*Collapsed:*
- Small bar showing: Photo, name, rating, call/message buttons

*Expanded:*
- Full rider profile:
  - Name: "Aminata Diallo"
  - Rating: "4.9 ⭐ (87 courses)"
  - Phone: "Appeler" / "Message" buttons
  - Pickup details:
    - What3Words: ///opera.cellblock.limb
    - Landmark: "Devant la Grande Mosquée"
    - Photo (if rider shared): Thumbnail, tap to view full
    - Voice note (if sent): Play button
  - Trip details:
    - Destination: "Université Gamal Abdel Nasser"  
    - Estimated fare: 18,000 GNF
    - Your earnings: 16,200 GNF
    - Payment method: 💵 Espèces

*Navigation Controls:*
- Recenter button (if panned)
- Zoom controls
- Audio toggle (mute/unmute voice directions)

*Action Button:*
- "J'arrive bientôt" (Arriving soon) - When within 500m
  - Sends notification to rider
  - Changes to "Je suis arrivé" (I've arrived) when at pickup

**Screen D3.2: Waiting for Rider (At Pickup)**

*Status Banner:*
- "En attente du passager" (Waiting for passenger)
- Timer: "Temps d'attente: 01:45" (counts up)
- Note: "Frais d'attente après 5 min: 2,000 GNF"

*Map:*
- Zoomed in to pickup area
- Your car stationary
- Rider location (if they've shared): Blue dot with distance
  - "Passager à 50m" (Passenger 50m away)

*Rider Card:*
- Photo prominent
- "Aminata arrive" (Aminata is arriving)
- Contact buttons: Call, Message
- Pickup details visible

*Action Buttons:*
- Primary: "Passager à bord" (Passenger on board)
  - Tap to start trip
  - Confirmation: "Confirmer que Aminata est dans le véhicule?"
- Secondary: "Annuler la course" (Cancel trip)
  - Reasons: "Passager introuvable" (Can't find passenger), "Passager annule", "Autre"
  - Cancellation fee may apply after 5 min

*Safety Note:*
- "✓ Vérifiez que c'est bien Aminata avant de démarrer"
- Photo verification recommended

**Screen D3.3: In-Trip (Active)**

*Status Banner:*
- "Course en cours" (Trip in progress)
- ETA to destination: "12 min"
- Distance remaining: "3.2 km"

*Map:*
- Turn-by-turn navigation to destination
- Route: Your location → Destination (B)
- Traveled route: Gray line
- Remaining route: Blue line
- Next turn: Large arrow + "Tournez à droite dans 500m"

*Trip Info Card:* (Bottom, swipeable)

*Collapsed:*
- Rider photo + name
- Destination preview
- Earnings: "16,200 GNF"

*Expanded:*
- Full trip details:
  - Pickup: "Grande Mosquée" ✓ (completed)
  - Destination: "Université"
  - Distance: 3.8 km (updating as you drive)
  - Time elapsed: "06:30"
  - Estimated earnings: "16,200 GNF"
  - Payment: Cash

*Action Button:*
- "Arrivée" (Arrived) - Appears when within 100m of destination
  - Tap to complete trip

*Safety:*
- SOS button (top-right, red) for emergencies

**Screen D3.4: Trip Completion**

*Full-screen card (slides up)*

*Header:*
- "Course terminée!" (Trip completed!)
- Checkmark animation

*Trip Summary:*
- Map thumbnail: Route traveled
- Pickup: "Grande Mosquée"
- Destination: "Université"
- Distance: "3.8 km"
- Duration: "15 min"

*Payment Collection:*

*If Cash:*
- Large text: "Montant à collecter: 18,000 GNF"
- Instruction: "Demandez le paiement au passager"
- Checkbox: "✓ Paiement reçu" (Must check to continue)
- Warning if not checked: "Confirmez le paiement avant de continuer"

*If Orange Money:*
- Status: "Paiement automatique en cours..."
- Success: "✅ 18,000 GNF reçu via Orange Money"
- Transaction ID shown

*Your Earnings:*
- Fare: 18,000 GNF
- Commission (10%): -1,800 GNF
- Bonus: +0 GNF
- Net: "16,200 GNF" (large, green)

*Rating Request:*
- "Comment était ce trajet?" (How was this trip?)
- 5-star rating for rider
- Quick tags: "Poli", "À l'heure", "Bonne destination"
- Optional comment field

*Action Buttons:*
- Primary: "Terminer" (Finish) - Returns to dashboard
- Secondary: "Signaler un problème" (Report issue)

---

### 4. Earnings & Payouts

**Screen D4.1: Earnings Dashboard**

*Header:*
- Back button
- Title: "Mes gains" (My earnings)
- Date range selector: "Cette semaine ▼" (This week)
  - Options: Aujourd'hui (Today), Cette semaine (This week), Ce mois (This month), Personnalisé (Custom)

*Balance Card:* (Top, prominent)
- Large number: "548,750 GNF"
- Label: "Solde disponible" (Available balance)
- Subtext: "Paiement automatique ce soir à 18h00" (Auto-payout today at 6 PM)
- Progress bar: Shows earnings toward payout threshold
- Payout button: "Demander un paiement anticipé" (Request early payout) - If eligible

*Earnings Breakdown:*

*Cette semaine:* (This week)
- Gross earnings: 610,000 GNF
- Trips: 34 courses
- Commission (10%): -61,000 GNF
- Bonuses: +0 GNF
- Net: 548,750 GNF

*Chart:* (Bar graph)
- Shows daily earnings for past 7 days
- Tap bar to see that day's breakdown
- Y-axis: Earnings in GNF
- X-axis: Days (Lun, Mar, Mer, Jeu, Ven, Sam, Dim)

*Stats Grid:*
- Total trips: 34
- Average per trip: 16,140 GNF
- Total distance: 127 km
- Online hours: 23h 15min
- Acceptance rate: 94%
- Rating: 4.8 ⭐

*Bonus Opportunities:*
- "🎯 Complétez 50 courses cette semaine" (Complete 50 trips this week)
  - Progress: 34/50 (68%)
  - Reward: 100,000 GNF bonus
  - Time left: "2 jours" (2 days)

**Screen D4.2: Payout History**

*List of payouts:* (Scrollable)

Each payout card shows:
- Date: "Lundi 18 déc 2024"
- Amount: "548,750 GNF" (large, bold)
- Method: "Orange Money +224 XXX XX XX XX"
- Status: "✅ Payé" (Paid) - Green badge
- Transaction ID: "OM-2024-12-18-XXXX"
- Tap to expand:
  - Period: "11 déc - 17 déc"
  - Trips: 34
  - Gross: 610,000 GNF
  - Commission: -61,000 GNF
  - Net: 548,750 GNF
  - Reçu button: Download PDF receipt

*Statuses:*
- Paid: Green checkmark
- Pending: Orange clock icon
- Failed: Red X with "Réessayer" (Retry) button

*Empty State:*
- "Aucun paiement encore" (No payouts yet)
- "Complétez votre première course pour commencer à gagner!"

---

## 🎨 Design System Components

### Buttons

**Primary Button:**
- Background: Orange (#f97316)
- Text: White, 16px, medium weight
- Height: 48px
- Border radius: 12px
- Shadow: 0px 2px 8px rgba(249, 115, 22, 0.3)
- States:
  - Default: Solid orange
  - Hover/Press: Darker orange (#ea580c)
  - Disabled: Gray (#e5e7eb), text gray (#9ca3af)
  - Loading: Orange with spinner

**Secondary Button:**
- Background: White
- Border: 2px solid Blue (#1e40af)
- Text: Blue, 16px, medium weight
- Height: 48px
- Border radius: 12px
- States:
  - Default: As described
  - Hover/Press: Light blue background (#eff6ff)
  - Disabled: Gray border, gray text

**Text Button:**
- No background or border
- Text: Blue (#1e40af), 14px, medium weight
- Underline on hover/press
- Used for: "Skip", "Cancel", "Learn more"

**Icon Button:**
- 40px × 40px circle
- Background: White or light gray
- Icon: 20px, centered
- Shadow: 0px 1px 4px rgba(0,0,0,0.1)
- Examples: Call, Message, Menu, Close

### Input Fields

**Text Input:**
- Height: 48px
- Border: 1px solid #cbd5e1
- Border radius: 8px
- Padding: 12px 16px
- Placeholder: Gray (#94a3b8), 14px
- Text: Black, 16px
- States:
  - Focus: Border blue (#1e40af), 2px width
  - Error: Border red (#ef4444), error text below
  - Disabled: Gray background (#f8fafc)
  - Success: Border green (#10b981), checkmark icon

**Search Input:**
- Similar to text input
- Icon: Magnifying glass (left, 20px)
- Clear button (right, appears when text entered)
- Autocomplete dropdown (if applicable)

**Phone Input:**
- Country code prefix: "+224" (locked)
- Auto-formatting: XXX XX XX XX
- Numeric keyboard

### Cards

**Standard Card:**
- Background: White
- Border radius: 12px
- Shadow: 0px 2px 8px rgba(0,0,0,0.06)
- Padding: 16px
- Margin bottom: 12px

**Elevated Card:** (For important content)
- Background: White
- Border radius: 16px
- Shadow: 0px 4px 16px rgba(0,0,0,0.12)
- Padding: 20px

**List Item Card:**
- Background: White
- Border bottom: 1px solid #e5e7eb (except last)
- Padding: 16px
- Tap area: Full width

### Icons

**Icon Library:** Lucide Icons (open-source, consistent style)

**Common Icons:**
- Navigation: ChevronLeft, ChevronRight, Menu, X
- Actions: Phone, MessageCircle, Share, Edit, Trash
- Status: Check, AlertCircle, Info, AlertTriangle, XCircle
- Maps: MapPin, Navigation, Map, Compass
- Money: DollarSign, CreditCard, Wallet, TrendingUp
- User: User, Users, UserCheck, Star
- Vehicle: Car, Bike (motorcycle), Package
- Time: Clock, Calendar, Timer

**Icon Sizes:**
- Small: 16px (in text, minor actions)
- Medium: 20px (buttons, list items)
- Large: 24px (headers, primary actions)
- Extra Large: 32px+ (empty states, onboarding)

### Typography Scale

**Scale:**
```
Display: 32px / Bold - For large headings, landing pages
H1: 28px / Bold - Page titles
H2: 22px / Semi-bold - Section headers
H3: 18px / Semi-bold - Card titles
Body Large: 16px / Regular - Primary content, buttons
Body: 14px / Regular - Secondary content, descriptions
Caption: 12px / Regular - Timestamps, metadata
Overline: 11px / Medium / UPPERCASE - Labels, tags
```

**Colors:**
- Primary text: #1e293b (dark gray, not pure black)
- Secondary text: #64748b (medium gray)
- Tertiary text: #94a3b8 (light gray)
- Disabled text: #cbd5e1 (very light gray)
- Link text: #1e40af (blue)
- Error text: #ef4444 (red)
- Success text: #10b981 (green)

### Spacing System

**8px base unit:**
```
4px (0.5 unit) - Tight spacing within components
8px (1 unit) - Compact spacing
12px (1.5 units) - Standard element spacing
16px (2 units) - Card padding, section spacing
24px (3 units) - Large spacing between sections
32px (4 units) - Page margins
48px (6 units) - Major section dividers
```

### Status Colors & Badges

**Trip Status:**
- Requested: Blue (#1e40af) with "Demandé"
- Accepted: Blue (#1e40af) with "Accepté"
- In Progress: Green (#10b981) with "En cours"
- Completed: Green (#10b981) with "Terminé"
- Cancelled: Gray (#64748b) with "Annulé"
- Refunded: Orange (#f59e0b) with "Remboursé"

**Payment Status:**
- Pending: Orange (#f59e0b) with clock icon
- Completed: Green (#10b981) with checkmark
- Failed: Red (#ef4444) with X icon

**Driver Status:**
- Online: Green dot + "En ligne"
- Offline: Gray dot + "Hors ligne"
- On Trip: Blue dot + "En course"

### Animations

**Purpose:** Smooth, purposeful animations that provide feedback, not decoration

**Micro-interactions:**
- Button press: Scale down to 0.95, 100ms
- Toggle switch: Slide animation, 200ms ease-in-out
- Modal slide up: Translate Y from bottom, 300ms ease-out
- Card expand: Height animation, 250ms ease-in-out
- Loading spinner: Rotate 360° continuously, 1s linear

**Page Transitions:**
- Screen push: Slide from right, 300ms ease-out
- Screen pop: Slide to right, 300ms ease-in
- Modal present: Fade + slide up, 300ms ease-out
- Modal dismiss: Fade + slide down, 250ms ease-in

**Feedback Animations:**
- Success checkmark: Scale + fade in, 400ms
- Error shake: Horizontal shake 3 times, 400ms
- Loading pulse: Opacity 1 → 0.5 → 1, 1.5s infinite

**Performance:**
- All animations use CSS transforms (GPU-accelerated)
- No layout animations (width/height/top/left)
- Reduce motion respected for accessibility

---

## 📐 Layout Guidelines

### Grid System

**Mobile Grid:**
- Container padding: 16px (left and right)
- Column gutter: 8px
- Number of columns: 4 (for mobile)
- Breakpoint: 375px base (iPhone SE), up to 428px (iPhone Pro Max)

**Safe Areas:**
- iOS: Respect notch and home indicator
- Android: Respect system navigation
- No interactive elements in bottom 16px (gesture area)

### Common Layouts

**Full-bleed Map:**
- Map fills entire screen
- UI elements floating on top
- Status bar: Dark text on light overlay or light text on dark map
- Bottom sheet: Draggable overlay with handle

**List View:**
- Scrollable vertical list
- Pull-to-refresh at top
- Infinite scroll at bottom
- Sticky headers for date sections

**Form Layout:**
- Each input full-width (with 16px side margins)
- 16px vertical spacing between inputs
- Labels above inputs (12px, semi-bold)
- Helper text below inputs (12px, gray)
- Validation messages below (red or green)

**Bottom Sheet:**
- Handle bar: 32px wide, 4px tall, centered, 12px from top
- Draggable (swipe down to collapse/dismiss)
- Backdrop: Semi-transparent dark overlay (rgba(0,0,0,0.4))
- States: Collapsed (1/3 height), Expanded (2/3 height), Full (90% height)

---

## ♿ Accessibility Requirements

### Color Contrast

**WCAG AA Compliance:**
- Normal text (14-16px): 4.5:1 minimum contrast ratio
- Large text (18px+): 3:1 minimum contrast ratio
- Interactive elements: 3:1 minimum

**Testing:**
- Use contrast checker for all text/background combinations
- Ensure buttons are visible in all states
- Icons must have sufficient contrast

### Touch Targets

**Minimum Size:**
- Primary actions: 48px × 48px (comfortable tap)
- Secondary actions: 44px × 44px
- Text links: 32px height minimum

**Spacing:**
- 8px minimum between tappable elements
- 16px preferred spacing for critical actions

### Text Sizing

**Accessibility:**
- Support dynamic type (iOS)
- Respect user font size preferences
- Text should scale up to 200% without breaking layout
- Line height: 1.5 for body text (readability)

### Screen Reader Support

**Labels:**
- All interactive elements have accessible labels
- Icons have text alternatives
- Form inputs have associated labels
- Meaningful button text (not just "OK" or "Cancel")

**Focus Order:**
- Logical tab order (top to bottom, left to right)
- Focus visible on interactive elements
- Keyboard navigation support (for Android tablets)

### Color Blindness

**Design Considerations:**
- Never use color alone to convey information
- Use icons + color for status (e.g., green checkmark for success)
- Distinct patterns in addition to colors
- Test with color blindness simulators (protanopia, deuteranopia, tritanopia)

---

## 🌍 Localization & Language

### Language Support

**Launch Languages:**
- **French** (Primary) - Official language of Guinea
- **Susu** (Phase 2) - Spoken in coastal areas
- **Pular** (Phase 2) - Spoken in Fouta Djallon
- **Malinké** (Phase 2) - Spoken in upper Guinea

### French Localization

**Terminology:**
- Ride = "Course" (not "trajet" which means journey)
- Driver = "Conducteur" (not "chauffeur" which implies professional driver)
- Pickup = "Point de départ" or "Prise en charge"
- Destination = "Destination" or "Point d'arrivée"
- Cash = "Espèces"
- Wallet = "Portefeuille"

**Address:**
- Use "tu" form (informal, friendly) for riders
- Use "vous" form (formal, respectful) for drivers
- Error messages: Polite but direct

**Cultural Considerations:**
- Respect Islamic holidays (Ramadan, Tabaski)
- Time format: 24-hour preferred (14:30 not 2:30 PM)
- Date format: DD/MM/YYYY (European style)
- Number format: Space as thousands separator (18 000 not 18,000)
- Currency: Guinean Franc (GNF) - No decimal places

### RTL Support

Not required (French is LTR), but architecture should support future Arabic if expanding to North Africa.

---

## 🚀 Performance Requirements

### Load Times

**Targets:**
- App launch: <3 seconds (cold start)
- Screen transition: <300ms
- Map render: <1 second (cached tiles)
- API response: <500ms (p95)
- Image load: Progressive (show low-res placeholder first)

### File Sizes

**Constraints:**
- App download size: <30MB (Android), <40MB (iOS)
- Image assets: WebP format, <200KB per image
- Offline map: <100MB for Conakry (Progressive download)
- Font files: <100KB total

### Optimization

**Images:**
- Use WebP format (better compression than JPEG/PNG)
- Lazy load images outside viewport
- Use appropriate resolutions (1x, 2x, 3x)
- Compress to 80% quality

**Animations:**
- Use transform and opacity (GPU-accelerated)
- Avoid animating width, height, top, left (CPU-intensive)
- Limit simultaneous animations to 3 max

**Network:**
- Cache API responses (5-minute TTL for dynamic data)
- Prefetch likely next screens
- Offline-first architecture (service workers for React Native)

---

## 📱 Platform-Specific Considerations

### iOS

**Design:**
- Use iOS native navigation patterns (back button, swipe to go back)
- Respect safe areas (notch, home indicator)
- Use SF Symbols for system icons (when appropriate)
- iOS-style switches and pickers

**Interaction:**
- Swipe gestures for common actions
- Long-press for contextual menus
- Pull-to-refresh with iOS bounce
- Haptic feedback on important actions

### Android

**Design:**
- Material Design 3 principles
- Use Android navigation patterns (back button in hardware or software)
- Floating Action Button (FAB) for primary actions
- Bottom navigation for main sections

**Interaction:**
- Ripple effect on button press
- Swipe gestures optional (not all users know them)
- Long-press for contextual menus
- Pull-to-refresh with Android spinner

### Cross-Platform Consistency

**What should be the same:**
- Colors, typography, spacing
- Information architecture
- Core user flows
- Brand personality

**What can differ:**
- Navigation patterns (tab bar vs. drawer)
- System interactions (share sheet, permissions)
- Animations (platform-specific feel)
- Icons (use platform conventions when appropriate)

---

## 🔐 Privacy & Security UI

### Data Collection Transparency

**Permissions:**
- Explain why each permission is needed BEFORE requesting
- Clear language: "Nous avons besoin de votre position pour vous connecter avec des conducteurs proches"
  (We need your location to connect you with nearby drivers)
- Allow users to deny and still use app (with limitations)

**Privacy Settings:**
- Control over data sharing
- Location sharing: Always, Only while using, Never
- Contact sharing: Optional
- Marketing communications: Opt-in, not opt-out

### Security Indicators

**Trust Signals:**
- Verified driver badge (checkmark icon)
- SSL/TLS connection indicator
- Payment security messaging: "Paiements sécurisés et chiffrés"
- Driver/vehicle photo verification

**Sensitive Actions:**
- Confirm before canceling trips
- Confirm before deleting payment methods
- Confirm before signing out
- Re-authenticate for payment changes (PIN or biometric)

---

## 📋 Design Deliverables Checklist

### Required Deliverables

**Design System:**
- [ ] Color palette with hex codes
- [ ] Typography scale with fonts and sizes
- [ ] Component library (buttons, inputs, cards, etc.)
- [ ] Icon set (all icons used, labeled)
- [ ] Spacing and grid system
- [ ] Animation specifications

**Rider App (15 Screens):**
- [ ] Splash screen
- [ ] Onboarding (3 slides)
- [ ] Phone verification
- [ ] OTP entry
- [ ] Profile setup
- [ ] Home/Map view
- [ ] Set pickup location
- [ ] Set destination
- [ ] Ride options & pricing
- [ ] Searching for driver
- [ ] Driver assigned/tracking
- [ ] In-trip
- [ ] Trip completed
- [ ] Profile/Settings
- [ ] Trip history

**Driver App (12 Screens):**
- [ ] Driver welcome
- [ ] Get started
- [ ] Document upload (4 steps)
- [ ] Orientation scheduling
- [ ] Dashboard (offline)
- [ ] Dashboard (online)
- [ ] Incoming ride request
- [ ] Navigating to pickup
- [ ] Waiting at pickup
- [ ] In-trip navigation
- [ ] Trip completion
- [ ] Earnings dashboard

**States & Variations:**
- [ ] Loading states
- [ ] Empty states
- [ ] Error states
- [ ] Success states
- [ ] Skeleton screens (content loading)

**Responsive:**
- [ ] Small phone (iPhone SE, 375px width)
- [ ] Large phone (iPhone Pro Max, 428px width)
- [ ] Android variations (if necessary)

**Interactions:**
- [ ] Button press states
- [ ] Form validation feedback
- [ ] Animation specifications
- [ ] Gesture interactions (swipe, drag, pinch)

**Export:**
- [ ] Figma file with proper organization
- [ ] Developer handoff annotations
- [ ] Asset export (PNG, SVG, WebP)
- [ ] Style guide document

---

## 🎯 Success Criteria

The design will be considered successful if:

1. **Usability:** Users can complete core flows without instructions
   - Book a ride in <60 seconds
   - Understand all icons and labels
   - Find help when needed

2. **Accessibility:** WCAG AA compliance
   - All text readable (contrast ratios met)
   - All interactive elements tappable (44px+)
   - Screen reader compatible

3. **Brand:** Feels distinctly "Pssst"
   - Color palette used consistently
   - Personality comes through (friendly, trustworthy)
   - Not generic (could be any ride app)

4. **Localization:** Works for Guinea context
   - French language correct and natural
   - Addresses Guinea-specific challenges (no addresses, offline, etc.)
   - Culturally appropriate imagery and examples

5. **Performance:** Fast and responsive
   - No perceived lag (<300ms transitions)
   - Images load progressively
   - Works on low-end Android devices

6. **Developer-Ready:** Easy to implement
   - Components clearly defined
   - Specifications complete (sizes, colors, spacing)
   - Edge cases considered
   - Responsive behavior documented

---

## 📞 Questions & Clarifications

If you need clarification on any aspect of this brief, please ask about:

- Specific user flows or edge cases
- Technical constraints or capabilities
- Brand tone or personality
- Market-specific considerations
- Feature prioritization
- Accessibility requirements
- Platform-specific needs

**Key Contact:** Product team available for questions throughout design process

---

## 🚀 Next Steps

1. **Review this brief thoroughly** - Ask questions before starting
2. **Create mood board** - Visual direction exploration (optional but recommended)
3. **Build design system** - Colors, typography, components first
4. **Design key screens** - Focus on core flows (booking, trip, earnings)
5. **Review with team** - Get feedback early and often
6. **Iterate based on feedback** - Refine and polish
7. **Complete all screens** - Fill in remaining screens
8. **Prepare developer handoff** - Annotations, specs, assets
9. **Final review** - Check against success criteria

**Timeline:** 4-6 weeks for complete design system + all screens + variations

---

**Thank you for designing Pssst! Let's build something great for Guinea. 🇬🇳**
