# 🌾 FarmDirect — Farm-to-Consumer Agricultural Marketplace

> **Eliminating the Middleman. Empowering the Grower. Feeding the Nation.**
> A production-grade full-stack platform connecting Indian farmers directly with consumers and businesses — ensuring **85–90% direct payout share for farmers** and **100% price transparency** for conscious buyers.

---

## 📌 Executive Summary

**FarmDirect** is an intelligent agricultural marketplace built to dismantle the predatory intermediary chain that plagues Indian agriculture. By connecting verified farmers directly with consumers, the platform ensures fair pricing, traceable produce origins, and transparent payout accounting.

Farmers list their harvests, set real prices, and advance order fulfillment themselves. Consumers browse multi-farm produce, track deliveries on an interactive timeline, and see exactly how much the farmer earns versus a traditional mandi chain. Admins oversee the platform through a live analytics console with GMV tracking, farmer verification queues, and user management.

The platform features **AI-powered demand forecasting**, **map-based logistics routing**, **Razorpay payment integration**, and a **real-time payout ledger** — all built on a clean monorepo architecture.

---

## 🌾 Key Features

### 🛒 1. Consumer Marketplace ( `GET /api/products` ):

- **Browse Verified Produce**: Vegetables, fruits, grains, pulses, dairy, and spices from verified farm partners.
- **Middlemen Elimination Widget**: Live interactive calculator showing traditional mandi markup vs. FarmDirect direct pricing.
- **Multi-Criteria Search & Filtering**: Filter by `category`, `organic`, `minPrice`/`maxPrice`, `sort` (newest / price_asc / price_desc).
- **Grouped Multi-Farmer Cart**: Live stock validation, free shipping progress tracker, and delivery fee calculation.
- **4-Step Checkout Flow**: Multi-address management, order notes, and Razorpay test-mode payment simulation.
- **Order Tracking Timeline**: Interactive stepper — `Confirmed → Harvested → Packed → In-Transit → Delivered`.
- **Post-Purchase Verified Reviews**: Rate and review produce quality only after delivery confirmation.

### 🚜 2. Farmer Portal ( `GET /api/farmers/dashboard/stats` ):

- **Real-Time KPI Dashboard**: Today's sales, gross earnings, net payouts, pending orders, and 7-day revenue trend charts.
- **Produce & Inventory Manager**: Create harvest listings with image URLs, pricing, units, and daily stock adjustments.
- **Order Fulfillment Pipeline**: Advance order status from `Accepted → Preparing → In-Transit` and hand off to logistics.
- **Transparent Payout Ledger**: Auditable accounting with 5% platform fee deduction breakdown and net settlement amounts.
- **Farm Profile Branding**: Showcase farm story, soil practices, farm size, farming type, and certification badges.

### 👑 3. Admin Console ( `GET /api/admin/dashboard` ):

- **Platform Analytics & GMV**: Real-time gross merchandise value, 5% tech commission revenue, and category distribution charts.
- **Farmer Verification Queue**: Audit and approve / reject / suspend farmer applications with status filter.
- **User Management**: View all consumer and farmer accounts with suspension / activation controls.
- **Platform-Wide Orders**: Oversee all system shipments and manage category taxonomies.

### 🚚 4. Rider / Driver Portal ( `GET /api/logistics/jobs` ):

- **Driver Dashboard**: View all assigned logistics jobs with order details, customer info, and delivery address.
- **Verify Pickup**: Mark an order as picked up from the farmer — updates job status to `IN_TRANSIT`.
- **OTP-Based Delivery Confirmation**: Complete delivery by entering a consumer OTP — marks order as `DELIVERED`.
- **Driver Verification**: Admin can verify / approve rider accounts before they can accept jobs.
- **Vehicle Assignment**: Each driver is linked to a vehicle; admin assigns driver + vehicle to a logistics job.

### 🔮 5. AI Demand Forecasting ( `GET /api/forecast` ):

- Predicts upcoming demand for produce categories using historical order patterns.
- Helps farmers plan harvests proactively to reduce wastage and unsold stock.

### 🗺️ 6. Logistics & Route Optimization ( `GET /api/logistics`, `GET /api/routes` ):

- Map-based delivery route planning using **Leaflet** + **OpenStreetMap Nominatim** geocoding.
- Haversine distance calculation for nearest-farm matching.
- Progressive geocoding fallback to resolve imprecise address strings.

### 🔔 7. Notification System ( `GET /api/notifications` ):

- Real-time in-app notification dispatch for order status changes and farmer approvals.


---

## 🏛️ System Architecture

```
┌────────────────────────────────────────────────────────┐
│        React 18 + Vite + Tailwind CSS Frontend         │
│                (http://localhost:5173)                  │
└───────────────────────┬────────────────────────────────┘
                        │  REST JSON API (Axios)
                        ▼
┌────────────────────────────────────────────────────────┐
│       Node.js + Express + TypeScript Backend            │
│                (http://localhost:5000)                  │
└──────┬──────────┬────────────┬──────────────┬──────────┘
       │          │            │              │
       ▼          ▼            ▼              ▼
 ┌──────────┐ ┌────────┐ ┌──────────┐ ┌───────────────┐
 │  Prisma  │ │Razorpay│ │  OSM     │ │  Forecast     │
 │  ORM +   │ │Payment │ │Nominatim │ │  Engine       │
 │  SQLite  │ │Service │ │Geocoding │ │  (AI Layer)   │
 └──────────┘ └────────┘ └──────────┘ └───────────────┘
```

---

## 🛠️ Tech Stack

| Layer | Technologies |
| :--- | :--- |
| **Frontend** | React 18, TypeScript, Vite, Tailwind CSS, React Router DOM, Recharts, Lucide React, Leaflet + React-Leaflet, Axios |
| **Backend** | Node.js, Express 4, TypeScript, Zod (validation), JWT (auth), bcryptjs, Morgan |
| **Database & ORM** | Prisma ORM with **SQLite** (zero-setup local) — **PostgreSQL-ready** |
| **Payment** | Razorpay Service — test-mode simulation with cryptographic signature verification |
| **Geolocation** | OpenStreetMap Nominatim API — progressive geocoding + Haversine distance |
| **DevOps** | Docker Compose, Vercel (frontend), tsx (watch mode), Prisma Studio |

---

## 🌟 Demo Credentials

| Role | Email | Password | Access / Portal |
| :--- | :--- | :--- | :--- |
| **Admin** | `admin@farmdirect.com` | `Admin@123` | `/admin/dashboard` (Full platform oversight) |
| **Farmer** | `farmer1@farmdirect.com` | `Farmer@123` | `/farmer/dashboard` (Green Valley Organics) |
| **Consumer** | `consumer1@farmdirect.com` | `User@123` | `/shop` (Regular shopper account) |
| **Rider** | `rider1@farmdirect.com` | `Rider@123` | `/driver/dashboard` (Ramesh Delivery — verified rider) |

> 💡 Quick 1-click login buttons are available directly on the `/login` page.

---

## 🚀 Live Demo — Already Deployed!

> **No setup needed.** The app is live and fully functional on Vercel.

| Service | URL |
| :--- | :--- |
| 🌐 **Web Application** | **https://farmer-steel.vercel.app/** |
| 🔑 **Login Page** | https://farmer-steel.vercel.app/login |
| 🛒 **Marketplace** | https://farmer-steel.vercel.app/shop |
| 👑 **Admin Dashboard** | https://farmer-steel.vercel.app/admin/dashboard |
| 🚜 **Farmer Dashboard** | https://farmer-steel.vercel.app/farmer/dashboard |
| 🚚 **Rider Dashboard** | https://farmer-steel.vercel.app/driver/dashboard |

> 💡 Use the **1-click demo login buttons** on the `/login` page to instantly access any role.

---



## 🧪 Verification & Testing

Open browser and execute the complete user journeys:

1. **Consumer**: Browse marketplace → view price transparency widget → add to cart → complete checkout with simulated Razorpay → view live order tracking timeline.
2. **Farmer**: Log in → view dashboard KPIs & revenue chart → fulfill new order → advance fulfillment status → review payout ledger.
3. **Admin**: Log in → verify new farmer application → inspect platform GMV & 5% commission → manage user accounts.
4. **Rider**: Log in → view assigned delivery jobs → verify pickup from farmer → complete delivery with OTP confirmation.

---


## 🧾 API Contract Reference

Base URL: `http://localhost:5000/api`

> All protected endpoints require: `Authorization: Bearer <JWT_TOKEN>`

### Authentication

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/auth/register/customer` | Register a consumer account |
| `POST` | `/auth/register/farmer` | Register a farmer + create farm profile |
| `POST` | `/auth/login` | Login and receive JWT token |
| `GET` | `/auth/me` | Fetch authenticated user identity & role |

### Products & Marketplace

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/products` | Browse produce with search, filter, pagination |
| `GET` | `/products/:id` | Product detail with reviews & price comparison |
| `POST` | `/products` | Create new harvest listing *(Farmer/Admin)* |
| `PUT` | `/products/:id` | Update listing pricing or stock *(Farmer/Admin)* |
| `DELETE` | `/products/:id` | Remove listing *(Farmer/Admin)* |

### Cart & Shopping

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/cart` | Get cart with live stock validation & fee breakdown |
| `POST` | `/cart/items` | Add product to cart |
| `PUT` | `/cart/items/:id` | Update item quantity |
| `DELETE` | `/cart/items/:id` | Remove item from cart |

### Orders & Checkout

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/orders` | Transactional order creation with atomic stock decrement |
| `GET` | `/orders` | List orders (role-filtered) |
| `GET` | `/orders/:id` | Full order invoice & delivery timeline |
| `PUT` | `/orders/:id/status` | Advance order status *(Farmer/Admin)* |
| `PUT` | `/orders/:id/cancel` | Cancel order & restore inventory |

### Payments (Razorpay)

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/payments/create` | Generate Razorpay payment session |
| `POST` | `/payments/verify` | Verify payment signature & confirm order |

### Farmer Portal

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/farmers/dashboard/stats` | Revenue KPIs, 7-day chart & top produce |
| `GET` | `/farmers/dashboard/earnings` | Payout ledger with fee deduction breakdown |
| `PUT` | `/farmers/profile` | Update farm bio & practices |

### Admin Operations

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/admin/dashboard` | GMV, commission, orders & category distribution |
| `GET` | `/admin/farmers` | Farmer audit list with status filter |
| `PUT` | `/admin/farmers/:id/status` | Approve / reject / suspend farmer |
| `GET` | `/admin/users` | Platform user directory |

### Rider & Logistics

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/logistics/jobs` | List all logistics jobs (driver sees only their own) |
| `PUT` | `/logistics/jobs/:id/assign` | Assign driver + vehicle to a job *(Admin)* |
| `POST` | `/logistics/jobs/:id/verify-pickup` | Rider verifies pickup → status `IN_TRANSIT` |
| `POST` | `/logistics/jobs/:id/complete-delivery` | Rider completes delivery with OTP → `DELIVERED` |
| `GET` | `/logistics/vehicles` | List all registered vehicles |
| `GET` | `/logistics/drivers` | List all registered drivers |
| `PUT` | `/logistics/drivers/:id/verify` | Admin verifies a driver account |

### Advanced Modules

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET/POST` | `/forecast/*` | AI demand forecasting for produce categories |
| `GET/POST` | `/routes/*` | Delivery route planning & optimization |
| `GET` | `/notifications` | In-app notification feed |
| `POST` | `/upload` | File / image upload handler |

---

## 📁 Repository Structure

```
farmdirect/
├── backend/
│   ├── prisma/
│   │   ├── schema.prisma        # DB models — User, Product, Order, Payout, etc.
│   │   └── seed.ts              # Rich realistic seed dataset (demo accounts + data)
│   ├── src/
│   │   ├── config/              # Database client, env & constants
│   │   ├── controllers/         # REST API request handlers (14 controllers)
│   │   │   ├── auth.controller.ts
│   │   │   ├── product.controller.ts
│   │   │   ├── order.controller.ts
│   │   │   ├── farmer.controller.ts
│   │   │   ├── admin.controller.ts
│   │   │   ├── forecast.controller.ts
│   │   │   ├── logistics.controller.ts
│   │   │   └── ...
│   │   ├── middleware/          # JWT auth, RBAC guards, error handlers, validation
│   │   ├── routes/              # Express route definitions (16 route files)
│   │   ├── services/            # Razorpay payment, location geocoding, notifications
│   │   │   └── location.service.ts   # OSM Nominatim + Haversine distance
│   │   ├── validators/          # Zod validation schemas per entity
│   │   ├── utils/               # Shared utility helpers
│   │   ├── app.ts               # Express app setup (CORS, Morgan, routes)
│   │   └── server.ts            # Server entrypoint
│   ├── .env.example             # Environment variable template
│   └── package.json
│
├── frontend/
│   ├── src/
│   │   ├── components/          # Reusable UI components, layout & widgets
│   │   ├── context/             # AuthContext, CartContext (React Context API)
│   │   ├── pages/               # Public, Consumer, Farmer & Admin page views
│   │   │   ├── admin/           # AdminUsers, AdminDashboard, FarmerVerification
│   │   │   ├── farmer/          # FarmerDashboard, Inventory, Payouts
│   │   │   └── consumer/        # Shop, Cart, Checkout, OrderTracking
│   │   ├── router/              # App routing & RBAC-protected route guards
│   │   ├── services/            # Axios API client (service layer per entity)
│   │   ├── types/               # TypeScript interfaces & shared types
│   │   └── index.css            # Custom design tokens & Tailwind base styles
│   ├── tailwind.config.js
│   ├── vite.config.ts
│   └── package.json
│
├── docs/
│   ├── API_DOCUMENTATION.md     # Full REST endpoint specification
│   ├── DATABASE.md              # ER diagram & schema details
│   └── DEPLOYMENT.md            # Production deployment guide
│
├── docker-compose.yml           # Containerized multi-service setup
├── vercel.json                  # Vercel frontend deployment config
├── package.json                 # Monorepo root script runner
└── README.md
```

---

## 🗄️ Database Schema Overview

The Prisma schema defines the following core models:

| Model | Description |
| :--- | :--- |
| `User` | Unified user entity with `CONSUMER`, `FARMER`, `ADMIN` roles |
| `FarmerProfile` | Farm details, lat/lon coordinates, verification status, experience |
| `Product` | Harvest listing with price, stock, organic flag, market price comparison |
| `Category` | Produce taxonomy (Vegetables, Fruits, Grains, Dairy, Spices...) |
| `Cart` / `CartItem` | Per-user shopping cart with quantity and product relation |
| `Order` / `OrderItem` | Transactional order with status pipeline and delivery details |
| `PayoutRecord` | Auditable ledger — gross amount, platform fee (5%), net settlement |
| `Review` | Post-delivery product review with rating |
| `Address` | Multi-address per user with geocoded lat/lon |
| `Notification` | In-app alert records per user |

---

## 🐳 Docker Deployment

```bash
docker-compose up --build
```

Services started:
- **backend** → `http://localhost:5000`
- **frontend** → `http://localhost:5173`

---

## 🏗️ Architecture & Design Decisions

| Decision | Rationale |
| :--- | :--- |
| **Prisma + SQLite** | Zero-setup local execution; schema is PostgreSQL-ready for production |
| **Zod Validation** | Runtime schema validation at API boundary — no raw `req.body` trust |
| **JWT + RBAC Middleware** | Stateless auth with role-level guards (`CONSUMER`, `FARMER`, `ADMIN`) |
| **Atomic Order Transactions** | Prisma `$transaction` ensures stock decrement and payout record creation are atomic |
| **Progressive Geocoding** | Falls back gracefully from full address → city+state if OSM returns no result |
| **Razorpay Test Mode** | Full payment flow simulation without real money; signature verification intact |
| **Monorepo Root Scripts** | `npm run dev` from root starts both frontend and backend concurrently |

---

## 📄 License

This project is licensed under the **MIT License**.

---

<div align="center">

**Built with ❤️ for Indian Farmers**

*FarmDirect — From the field to your table, transparently.*

</div>
