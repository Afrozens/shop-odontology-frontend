# Shop Odontology Frontend - Agent Context

## Project Overview

**Project Name:** Shop Odontology Frontend
**Type:** E-commerce SPA (Single Page Application)
**Framework:** Nuxt 4 + Vue 3
**Styling:** Tailwind CSS v4
**Purpose:** E-commerce platform for selling dental/odontology supplies in Venezuela with nationwide delivery and multiple payment methods.

---

## Technology Stack

| Category | Technology | Version |
|----------|------------|---------|
| Framework | Nuxt | 4.3.1 |
| UI Library | Vue | 3.5.28 |
| Router | Vue Router | 4.6.4 |
| Styling | Tailwind CSS | 4.2.2 |
| Build Tool | Vite (via Nuxt) | - |

### Project Structure

```
shop-odontology-frontend/
├── app/
│   ├── assets/
│   │   └── css/
│   │       └── main.css        # Tailwind v4 theme configuration
│   └── app.vue                # Root component
├── nuxt.config.ts             # Nuxt configuration
├── package.json               # Dependencies
├── tsconfig.json              # TypeScript configuration
├── DESIGN.md                  # Design system tokens & guidelines
├── README.md                  # Project documentation
└── .nuxt/                     # Generated (do not edit)
```

---

## Design System

### Color Palette

| Token | Hex | Usage |
|-------|-----|-------|
| Canvas White | `#ffffff` | Page backgrounds, cards, inputs |
| Off White Clay | `#f5f4f1` | Secondary backgrounds |
| Midnight Ink | `#000000` | Primary text, icons |
| Graphite | `#707170` | Muted text, placeholders |
| Steel Gray | `#eeeeee` | Borders, dividers |
| Accent Blue | `#2f59f8` | Primary actions, CTAs |
| Highlight Orange | `#ff632a` | Promotional elements, accents |
| Active Yellow | `#eaff00` | Special highlights, sale tags |

### Typography

- **Primary Font:** Founders Grotesk (fallback: Inter)
- **Secondary Font:** GT Planar (fallback: Montserrat)
- **Base Size:** 14px
- **Line Height:** 1.25 (body), 1.5 (body-lg)

### Border Radius

| Element | Radius |
|---------|--------|
| Buttons | 50px (pill) |
| Cards | 16px |
| Inputs | 9999px (full pill) |
| General | 4px |

---

## Business Logic Overview

### User Roles

#### 1. Customer (Client)
- Browse products catalog
- Register and login
- Manage shopping cart
- Place orders with delivery address
- Select payment method
- View order history
- Add/manage shipping addresses

#### 2. Administrator
- View all orders
- Report/confirm payments manually
- View payment history
- Manage product inventory (future)
- Manage orders status

### Authentication Flow

```
User Registration → Email/Phone verification → Login
                                            ↓
                                    JWT Token Storage
                                            ↓
                              Protected Routes (Customer/Admin)
```

### Payment Methods

| Method | Description | Availability |
|--------|-------------|--------------|
| **Binance Pay** | Cryptocurrency payment via Binance | Nationwide |
| **Pago Móvil** | Venezuelan mobile payment system | Nationwide |
| **Bank Transfer** | Direct bank transfer | Nationwide |
| **Cash (Physical)** | In-person payment | Bolívar, Puerto Ordaz, Valencia (by appointment only) |

### Shipping Methods

| Carrier | Coverage | Notes |
|---------|----------|-------|
| **MRW** | National | Primary courier |
| **Zoom** | National | Secondary courier |

### Order Flow

```
Cart → Checkout → Address Selection → Payment Method → Order Confirmation
                                                              ↓
                                                    Payment Verification
                                                              ↓
                                                    Order Status Update
```

---

## Component Architecture

### Pages to Build (Route Structure)

```
/ (Home)
├── /products (Product Catalog)
│   └── /products/[id] (Product Detail)
├── /cart (Shopping Cart)
├── /checkout (Checkout Flow)
├── /orders (Order History)
├── /order/[id] (Order Detail)
├── /auth/login (Login)
├── /auth/register (Register)
├── /auth/forgot-password (Password Recovery)
├── /account (User Account)
└── /admin (Admin Dashboard)
    ├── /admin/orders (Manage Orders)
    ├── /admin/payments (Payment Management)
    └── /admin/payments/report (Report Payment)
```

### Shared Components

```
components/
├── ui/
│   ├── Button.vue
│   ├── Input.vue
│   ├── Card.vue
│   ├── Modal.vue
│   └── Badge.vue
├── layout/
│   ├── Header.vue
│   ├── Footer.vue
│   └── Sidebar.vue
├── product/
│   ├── ProductCard.vue
│   ├── ProductGrid.vue
│   └── ProductFilters.vue
├── cart/
│   ├── CartItem.vue
│   ├── CartSummary.vue
│   └── CartDrawer.vue
├── checkout/
│   ├── AddressForm.vue
│   ├── PaymentMethodSelector.vue
│   └── ShippingSelector.vue
└── order/
    ├── OrderCard.vue
    ├── OrderStatus.vue
    └── PaymentReportForm.vue
```

---

## State Management

### Pinia Stores (Future Implementation)

```typescript
// stores/
// ├── auth.ts        - Authentication state & user info
// ├── cart.ts        - Shopping cart management
// ├── products.ts    - Product catalog & filters
// ├── orders.ts      - Order history & status
// └── ui.ts          - UI state (modals, drawers, notifications)
```

---

## API Integration (Backend Expected)

### Endpoints Structure

```typescript
// Auth
POST   /api/auth/register
POST   /api/auth/login
POST   /api/auth/logout
GET    /api/auth/me

// Products
GET    /api/products
GET    /api/products/:id
GET    /api/products/categories

// Cart (optional server-side)
GET    /api/cart
POST   /api/cart/items
PUT    /api/cart/items/:id
DELETE /api/cart/items/:id

// Orders
POST   /api/orders
GET    /api/orders
GET    /api/orders/:id
PUT    /api/orders/:id/status

// Payments
POST   /api/payments/report
GET    /api/payments/history
PUT    /api/payments/:id/verify  // Admin only

// Addresses
GET    /api/addresses
POST   /api/addresses
PUT    /api/addresses/:id
DELETE /api/addresses/:id
```

---

## Environment Variables

```env
# API Base URL
NUXT_PUBLIC_API_URL=http://localhost:3001/api

# Binance Pay
NUXT_PUBLIC_BINANCE_PAY_ENABLED=true

# App Config
NUXT_PUBLIC_APP_NAME="Shop Odontology"
NUXT_PUBLIC_SUPPORT_EMAIL="support@shopodontology.com"
```

---

## Venezuelan Market Specifics

### Payment Methods (Venezuela)

| Method | Code | Processing | Available Zones |
|--------|------|-------------|------------------|
| **Binance Pay** | CRYPTO | Instant | Nationwide (online) |
| **Pago Móvil** | PMOVIL | Instant | Nationwide |
| **Bank Transfer** | TRANSFER | 1-48h | Nationwide |
| **Cash (Physical)** | CASH | In-person | Bolívar, Puerto Ordaz, Valencia (appointment required) |

### Shipping Carriers (Venezuela)

| Carrier | Coverage | Typical Time | Notes |
|---------|----------|--------------|-------|
| **MRW** | National | 24-72h | Primary courier, tracking available |
| **Zoom** | National | 24-48h | Secondary option, faster for major cities |

### Physical Payment Locations

```
CASH payment requires:
1. Previous appointment scheduling
2. Location: Bolívar, Puerto Ordaz, or Valencia only
3. Verification via WhatsApp/telephone
4. Order confirmation only after payment receipt
```

---

## Important Notes for Development

### Key Business Rules

1. **Cash payments** restricted to Bolívar, Puerto Ordaz, Valencia with prior appointment
2. **Shipping** available nationwide via MRW and Zoom carriers
3. **Payment verification** for manual methods requires admin confirmation
4. **Admin role** has access to payment reporting and history verification
5. **Order status flow:** Pending → Paid Confirmed → Processing → Shipped → Delivered

### Security Considerations

- JWT token-based authentication
- Role-based route protection (middleware)
- Input validation on all forms
- XSS prevention
- CSRF protection

### Responsive Design

- Mobile-first approach
- Breakpoints: sm (640px), md (768px), lg (1024px), xl (1280px)
- Optimized for Venezuelan market (mobile usage priority)

---

## Reference Website: SuperMush Style

**URL:** https://www.supermush.com

This e-commerce project should follow SuperMush's design aesthetic and UX patterns. Below is a detailed analysis:

### Visual Identity

- **Theme:** Light, clean, and modern
- **Feel:** Wellness/health brand with vibrant energy
- **Canvas:** White backgrounds with strategic color accents
- **Imagery:** High-quality product photography + lifestyle shots

### Homepage Structure

```
┌─────────────────────────────────────────────────────┐
│ HEADER: Logo | Nav Links | Account | Cart (count)  │
├─────────────────────────────────────────────────────┤
│ HERO: Full-width image, headline, CTA button      │
├─────────────────────────────────────────────────────┤
│ ANNOUNCEMENT BAR: Promo code or sale notice        │
├─────────────────────────────────────────────────────┤
│ CATEGORY NAV: Horizontal pills (Shop Gummies...)   │
├─────────────────────────────────────────────────────┤
│ FEATURED PRODUCTS: 4-col grid with badges         │
│  - Product Image                                   │
│  - Subscribe & Save badge                          │
│  - Star rating + review count                      │
│  - Product Name                                    │
│  - Benefits (dots separated)                       │
│  - Price (sale if applicable)                      │
├─────────────────────────────────────────────────────┤
│ BRAND SECTION: "Think. Move. Feel." + benefits     │
├─────────────────────────────────────────────────────┤
│ INGREDIENTS SHOWCASE: 4-col grid with images       │
├─────────────────────────────────────────────────────┤
│ VALUE PROPS: 3-column icons + descriptions          │
├─────────────────────────────────────────────────────┤
│ TESTIMONIALS: Customer reviews with photos         │
├─────────────────────────────────────────────────────┤
│ TRUST BADGES: Free shipping, returns, testing      │
├─────────────────────────────────────────────────────┤
│ FOOTER: Links, newsletter, social icons            │
└─────────────────────────────────────────────────────┘
```

### Product Card Design

```vue
<!-- Product Card Pattern -->
<div class="product-card">
  <div class="relative">
    <img :src="product.image" :alt="product.name" />
    <span v-if="product.badge" class="badge absolute top-4 left-4">
      {{ product.badge }}
    </span>
  </div>
  <div class="product-info">
    <span v-if="product.subscription" class="subscription-tag">
      Subscribe & Save 40%
    </span>
    <div class="rating">
      <StarIcon /> {{ product.rating }}
      <span>{{ product.reviewCount }} Reviews</span>
    </div>
    <h3>{{ product.name }}</h3>
    <p class="benefits">{{ product.benefits.join(' • ') }}</p>
    <div class="price">
      <span v-if="product.originalPrice" class="sale">
        {{ formatCurrency(product.salePrice) }}
        {{ formatCurrency(product.originalPrice) }}
      </span>
      <span v-else>{{ formatCurrency(product.price) }}</span>
    </div>
    <button>Add to cart</button>
  </div>
</div>
```

### Header Navigation

- Sticky header with transparent-to-white scroll effect
- Logo centered or left-aligned
- Navigation: Shop, Science, Bundle & Save (with dropdown)
- Right side: Account icon, Cart icon with item count badge

### Footer Structure

- 4-column layout: Shop, Science, About, Connect
- Newsletter signup form
- Social media icons (Instagram, Facebook, X, TikTok, YouTube)
- Legal links and copyright

### Key UI Components

| Component | Style | Usage |
|-----------|-------|-------|
| **Primary Button** | Pill shape (50px radius), Accent Blue bg, white text | Add to Cart, Shop Now |
| **Ghost Button** | Transparent bg, black text, no border | Nav links |
| **Badge** | Active Yellow bg, black text, pill shape | "Limited Edition", "Sale" |
| **Announcement Bar** | Full-width, Highlight Orange bg or gradient | Promo codes, sales |
| **Product Image** | Rounded corners (8px), subtle shadow | Cards, galleries |
| **Price Display** | Sale price in bold, original crossed out | Product cards |
| **Rating Display** | Stars + number + "Reviews" text | Product cards |
| **Subscription Tag** | Small pill, muted color | Subscription options |

### UX Patterns to Emulate

1. **Quick Add to Cart** - Single click from product grid
2. **Sticky Cart Badge** - Update count without page refresh
3. **Announcement Bar** - Persistent top bar for promotions
4. **Category Pills** - Horizontal scrolling category filters
5. **Star Ratings** - Social proof with review counts
6. **Sale Badges** - Visual urgency with percentage off
7. **Subscription Options** - "Subscribe & Save X%" toggle
8. **Testimonials Section** - Real customer photos + quotes
9. **Ingredient Showcase** - Educational product sections
10. **Value Props Grid** - Trust-building icon cards

### Animations & Interactions

- Smooth scroll behavior
- Hover effects on product cards (subtle scale)
- Image zoom on hover (product detail)
- Cart icon bounce on add
- Fade transitions between pages
- Loading skeletons for async content

### Responsive Strategy

- Mobile-first design
- Hamburger menu for mobile nav
- 2-column product grid on mobile
- Full-width hero images
- Stacked layout for mobile footer

---

## Design Guidelines Summary

- Use **Accent Blue** (#2f59f8) for primary CTAs
- Pill-shaped buttons with 50px radius
- Cards with 16px border radius
- Light theme with white/off-white backgrounds
- Clean, minimal aesthetic
- Focus on usability and conversion optimization
- High-quality product imagery
- Social proof elements (reviews, ratings, testimonials)

---

## Development Commands

```bash
# Install dependencies
npm install

# Development server (http://localhost:3000)
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview

# Generate static site
npm run generate
```

---

## Next Steps for Development

### Phase 1: Core Infrastructure
1. Create `layouts/default.vue` with SuperMush-style header and footer
2. Set up `app/pages/` directory structure
3. Configure Tailwind v4 theme variables from DESIGN.md
4. Create base UI components (Button, Input, Card, Badge)

### Phase 2: Homepage (SuperMush Style)
5. Build hero section with full-width image and CTA
6. Create announcement/promo bar component
7. Implement category navigation pills
8. Build featured products grid (4-column, desktop)
9. Create product card component with:
   - Image with hover zoom effect
   - Badge system (sale, new, limited)
   - Star rating display
   - Price with sale formatting
   - Quick add to cart button
10. Build trust badges section
11. Create testimonials/reviews section

### Phase 3: Authentication
12. Build login page with SuperMush aesthetic
13. Build registration page with validation
14. Create password recovery flow
15. Implement auth middleware for protected routes

### Phase 4: Product Catalog
16. Build product listing page with filters
17. Create product detail page with:
   - Image gallery
   - Product info
   - Add to cart
   - Subscription options if applicable
   - Reviews section
18. Implement product search

### Phase 5: Shopping Cart
19. Create cart drawer/slide-out
20. Build cart page with item management
21. Implement quantity controls
22. Add cart persistence (localStorage)

### Phase 6: Checkout Flow
23. Build address form with Venezuela states
24. Create shipping method selector (MRW, Zoom)
25. Implement payment method selection
26. Build order summary
27. Create order confirmation page

### Phase 7: User Account
28. Build account dashboard
29. Create address management
30. Implement order history view
31. Build order detail page with tracking

### Phase 8: Admin Dashboard
32. Create admin layout
33. Build orders management view
34. Create payment report form
35. Implement payment verification system
36. Build payment history viewer

### Phase 9: Polish & Performance
37. Add loading skeletons
38. Implement page transitions
39. Add hover animations
40. Optimize for mobile
41. Add toast notifications
42. Implement error handling

---

*Last Updated: 2026-05-12*