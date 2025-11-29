# 🧵 **RTW MVP Zero — Architecture Overview**

This document summarizes the entire Ready-to-Wear (RTW) MVP Zero system using **five essential diagrams**:

1. **Canonical ERD** (what data exists and how it connects)
2. **Order Lifecycle** (how orders move through the system + stock rules)
3. **Customer Flow** (how customers place orders)
4. **System Architecture** (microservices + databases + frontend)
5. **Frontend Structure** (how the app is organized)

Together, these diagrams provide the complete conceptual foundation of the RTW platform.

---

# 1. 📦 Canonical Domain Model (ERD)

This is the **single source of truth** for all data in RTW MVP Zero.

```mermaid
erDiagram
    Product ||--o{ ProductVariant : has
    Product ||--o{ ProductImage  : has

    Product {
        string  id
        string  name
        string  slug
        string  description
        float   price
        boolean isPublished
        datetime createdAt
        datetime updatedAt
    }

    ProductVariant {
        string id
        string productId
        string size
        string color
        string sku
    }

    ProductImage {
        string id
        string productId
        string url
        string altText
        int    position
    }

    ProductVariant ||--|| StockItem : tracked_by

    StockItem {
        string  id
        string  productVariantId
        int     quantity
        int     safetyStock
        datetime updatedAt
    }

    Order ||--o{ OrderItem    : contains
    Order ||--o| DeliveryInfo : has

    Order {
        string  id
        string  status
        string  customerName
        string  customerPhone
        string  customerAddress
        string  paymentMethod
        string  paymentStatus
        datetime createdAt
        datetime updatedAt
    }

    OrderItem {
        string id
        string orderId
        string productId
        string productVariantId
        float  unitPrice
        int    quantity
    }

    DeliveryInfo {
        string  id
        string  orderId
        string  deliveryStatus
        datetime plannedDate
        datetime actualDate
        string  notes
    }

    AdminUser ||--o{ Product : created
    AdminUser ||--o{ Order   : managed

    AdminUser {
        string  id
        string  name
        string  email
        string  passwordHash
        string  role
        datetime createdAt
        datetime updatedAt
    }
```

---

# 2. 🔄 Order Lifecycle & Stock Behaviour

This state machine defines how orders evolve and ensures **consistent stock management** across all services.

```mermaid
stateDiagram-v2
    [*] --> Pending: placeOrder() [stockAvailable]

    Pending --> Confirmed: confirmOrder()
    Confirmed --> OutForDelivery: startDelivery()
    OutForDelivery --> Delivered: markDelivered()

    Pending --> Cancelled: cancelOrder()
    Confirmed --> Cancelled: cancelOrder()
    OutForDelivery --> Cancelled: cancelDelivery()

    Delivered --> [*]
    Cancelled --> [*]

    note right of Pending
        - Stock RESERVED (decrement quantity)
        - Cancel here → RESTOCK
    end note

    note right of Confirmed
        - Stock was already reserved
        - Cancel here → RESTOCK
    end note

    note right of OutForDelivery
        - Items have physically left the atelier
        - Cancel here → NO restock
    end note

    note right of Delivered
        - Final sale completed
    end note

    note right of Cancelled
        - Behaviour depends on previous state
    end note
```

### What it enforces

* **A single universal definition of order states** across frontend, backend, and admin.
* **Correct inventory behaviour**, so stock and sales are always in sync.
* **Deterministic transitions**, allowing clean APIs such as:

  * `POST /orders/:id/confirm`
  * `POST /orders/:id/start-delivery`
  * `POST /orders/:id/cancel`

---

# 3. 🧍‍♂️ Customer Flow (MVP Ordering Process)

This is the public-facing journey.

```mermaid
flowchart TD
    A[Browse RTW Catalog] --> B[Select Product]
    B --> C[Choose Size]
    C --> D[Check Availability]
    D -->|In Stock| E[Fill Order Form]
    D -->|Out of Stock| X[Show 'Unavailable']
    E --> F[Confirm Order]
    F --> G[Order Created Pending]
```

### What it represents

* Minimal friction for the customer
* Single-product, single-size ordering (simple MVP)
* Clear alignment with the state machine (`Pending` created at step G)

---

# 4. 🏗️ System Architecture (Microservices + Gateway)

This diagram shows **how the whole RTW platform is wired together**.

```mermaid
flowchart LR

    subgraph Clients
        CUST["Public Web App (RTW)"]
        ADMIN["Admin Dashboard"]
    end

    GW["API Gateway / BFF<br/>rtw-api-gateway"]

    CUST --> GW
    ADMIN --> GW

    subgraph Catalog["Catalog Service<br/>rtw-catalog-service"]
        CAT_API[(HTTP API)]
        CAT_DB[(Catalog DB)]
    end

    subgraph Orders["Orders Service<br/>rtw-orders-service"]
        ORD_API[(HTTP API)]
        ORD_DB[(Orders DB)]
    end

    subgraph Inventory["Inventory Service<br/>rtw-inventory-service"]
        INV_API[(HTTP API)]
        INV_DB[(Inventory DB)]
    end

    subgraph Auth["Auth / Admin Service<br/>rtw-auth-service"]
        AUTH_API[(HTTP API)]
        AUTH_DB[(Auth DB)]
    end

    GW --> CAT_API
    GW --> ORD_API
    GW --> INV_API
    GW --> AUTH_API

    CAT_API --> CAT_DB
    ORD_API --> ORD_DB
    INV_API --> INV_DB
    AUTH_API --> AUTH_DB
```

### Key ideas

* **Each microservice owns its own database** (no shared DB).
* The API Gateway provides:

  * request routing
  * authentication
  * response shaping
* Services communicate only through:

  * HTTP APIs
  * or domain events later (future version)

---

# 5. 🎨 Frontend Architecture (React App Structure)

```mermaid
flowchart TD

    App[App.tsx] --> Router[AppRouter]
    Router --> PublicLayout
    Router --> AdminLayout

    subgraph PublicApp["Public (Customer) Area"]
        PublicLayout --> CatalogPage
        PublicLayout --> ProductDetailPage
        PublicLayout --> OrderFormPage
        PublicLayout --> OrderConfirmationPage
    end

    subgraph AdminApp["Admin (Atelier) Area"]
        AdminLayout --> AdminLoginPage
        AdminLayout --> AdminDashboardPage
        AdminLayout --> AdminProductsPage
        AdminLayout --> AdminOrdersPage
        AdminLayout --> AdminProductFormPage
    end

    App --> QueryClientProvider
    App --> ThemeProvider
    App --> ToastProvider
```

### What this expresses

* The RTW web app is split into **Public** and **Admin** zones.
* They share:

  * React Query for data
  * Theme provider
  * Toasts / notifications
* Admin routes map directly to order lifecycle transitions.

---

# 6. 🧠 Putting It All Together (Narrative Explanation)

## 6.1 Customer Perspective

1. **Browse Catalog**
   The frontend fetches `/products` from the Catalog service → via API Gateway.

2. **Select Product & Size**
   The UI loads product details + variants + available stock.

3. **Place Order**
   Customer fills the form → public API call to Orders service.

4. **Order Creation**

   * Orders service validates data
   * Inventory service **reserves** stock
   * New order is saved as `Pending`

5. **Customer sees confirmation screen**
   Done.

---

## 6.2 Admin Perspective

1. **Admin Logs In** (Auth service)
2. **Adds/Edits Products** (Catalog service)
3. **Manages Stock** (Inventory service)
4. **Receives New Orders** (Orders service)

   * All new orders appear in `Pending`
5. Admin clicks:

   * **Confirm** → order becomes `Confirmed`
   * **Start Delivery** → `OutForDelivery`
   * **Delivered** → `Delivered`
   * **Cancel** → `Cancelled` (with stock rules)

Everything aligns with the **order lifecycle**.

---

## 6.3 Services Perspective

* **Catalog** exposes product listings.
* **Inventory** tracks stock state + reservations.
* **Orders** manages order lifecycle + items.
* **Auth** handles admin authentication.
* **API Gateway** routes and protects everything.

Each service owns its data, allowing independence and scalability.

---

# 7. ✔️ Summary

These diagrams together form the entire mental model of RTW MVP Zero:

* **ERD** → what entities exist
* **Order State Machine** → how orders evolve
* **Customer Flow** → how orders are created
* **Architecture** → how services and DBs are organized
* **React Structure** → how the UI is organized

This README gives anyone (developer or non-tech) a **clear, unified, systematic understanding** of how the RTW platform works from A to Z.
