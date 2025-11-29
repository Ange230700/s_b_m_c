<!-- docs\mvp\README.md -->

# 👗 **RTW-First Strategy — Phase 0 (Highest Priority)**

**Goal:** Launch a minimal RTW product line with digital catalog + stock + order flow.

---

# 🎯 **1. RTW-Focused Mission**

Create a clean, simple, modern digital system that allows customers to:

1. Browse RTW items
2. Check availability
3. Place orders
4. Pay (even offline/pay-on-delivery)
5. Receive products reliably

Before we build the full atelier platform.

---

# 🧱 **2. Absolute Must-Have Modules for RTW (Phase 0 MVP)**

## **2.1 Product Catalog**

**Must-have features:**

* Add RTW products
* Product fields:

  * Name
  * Photos
  * Description
  * Sizes available
  * Price
  * Stock quantity per size

**Why?**
This is the core of the RTW experience.

---

## **2.2 Stock Management**

**Must-have features:**

* Track stock per size
* Reduce stock when order placed
* Prevent orders when stock = 0
* Manually adjust stock

**Why?**
No RTW business without knowing inventory.

---

## **2.3 Order Placement**

**Must-have features:**

* Customer submits order
* Required fields:

  * Full name
  * Phone number
  * Delivery address
  * Chosen product + size
  * Payment method (mobile money / cash-on-delivery)
* Order summary view

**Why?**
This is how money flows.

---

## **2.4 Order Management (Internal)**

**Must-have features:**

* List all orders
* Update order status:

  * Pending
  * Confirmed
  * Out for Delivery
  * Delivered
  * Cancelled
* View payment status

**Why?**
Operational control.

---

## **2.5 Delivery Tracking (Simple)**

**Must-have features:**

* Assign delivery person (optional)
* Mark “Out for Delivery”
* Mark “Delivered”

**Why?**
Ensures clean fulfillment.

---

## **2.6 Basic Authentication (Internal Only)**

**Must-have features:**

* Admin login to add products + manage orders
* Staff login optional for later

**Why?**
Minimum security.

---

## **2.7 Simple Reporting**

**Must-have features:**

* Sold units per product
* Stock running low (alert)
* Revenue (manual if no online payments yet)

**Why?**
Immediate business visibility.

---

# 🔥 **3. RTW User Flows (Ultra-Clear)**

## **Customer Flow**

Browse Catalog → Choose Item → Select Size → Fill Info → Confirm Order

## **Admin Flow**

Login → Add Product → Add Stock → View Orders → Update Status → Mark Delivered

That’s it.

---

# 🧬 **4. RTW Phase 0 Entities**

Only **five** entities needed:

1. **Product**
2. **ProductSize / StockUnit**
3. **Order**
4. **OrderItem**
5. **AdminUser**

This is extremely lightweight and can be built in < 2 weeks.

---

# ⭐ **5. RTW Success Criteria (Specific)**

* At least **20 RTW products** added to catalog
* Ability to process **50–100 orders** manually with the system
* < 5% stock errors
* Simple, frictionless ordering for clients
* Clean and fast internal workflow
* Real sales happening in 2–4 weeks after MVP deployment

---

# 🚀 **6. What We Build Next (Prioritized Roadmap)**

### **Phase 0 — RTW MVP**

(Catalog, stock, orders, delivery)

### **Phase 1 — Atelier Operations MVP**

(measurements, model validation, production workflow)

### **Phase 2 — Client Experience Layer**

(notifications, customer portal)

### **Phase 3 — Inventory & Fabric Management**

### **Phase 4 — Advanced SaaS (multi-tenant, analytics, AI)**

→ Powered by V∅ID Labs
