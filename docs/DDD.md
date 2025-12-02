<!-- docs\DDD.md -->

# 🟦 1. **Modeling**

**The code must mirror the domain.**
Not the database.
Not the framework.
Not the infrastructure.

### Key consequences:

* Anyone who knows the business can look at the code and understand what’s happening.
* Changes in business rules → changes should appear in the exact domain module.
* The domain shapes the code structure.
* The code also uncovers gaps in the domain → feedback loop.

This is why your RTW product, ordering flow, customer, and atelier workflows must each have their **own domain modules**.

---

# 🟩 2. **DDD is incremental**

**No Big Bang architecture.**
DDD grows as the domain grows.

### Core rules:

* Don’t design the whole architecture up-front → only enough to solve today's story.
* Architecture expands as understanding deepens.
* Domain evolves → architecture mirrors this evolution.
* DDD naturally follows agile / SCRUM.
* Each refinement adds:

  * new Aggregates
  * new Domain Events
  * new Value Objects
  * new Bounded Contexts
  * new choreography flows

### Why this matters for you:

You begin with **RTW MVP**.
Then extend to atelier operations.
Then multi-tenancy.
Then microservices.

DDD *makes this evolutionary path smooth*.

---

# 🟧 3. **DDD works extremely well with Agile**

Because:

* You work in small slices of functionality (stories)
* Each story uncovers new events, entities, roles, rules
* Each “slice” grows the model
* Every sprint improves clarity in the domain language

Your workflow should be:
**Story → Event Storming → Implement minimal model → Release → Refine.**

---

# 🟥 4. **Microservices & DDD**

DDD is almost **the perfect mental model** for microservices.

### Why:

* Microservices = modular business capabilities
* DDD’s Bounded Contexts = natural microservices boundaries

### Microservice benefits (from DDD perspective):

* **Independently deployable**
* **Implementation details hidden**
  (no service should leak its domain rules to another)
* **Modeled around business concepts**
* **Decentralized** by design
* **Observable**
* **Autonomous** — each service owns its own data + logic

### Why this matters for you:

You start with a **modular monolith** (for RTW).
Later, you split into separate services naturally (Products, Orders, Customers, Atelier, Payments).

---

# 🟪 5. **Bounded Contexts** (THE single most important strategic concept)

Bounded Context =
**A semantic boundary in which a specific Ubiquitous Language is valid.**

### What defines a Bounded Context:

* A team with specific responsibilities
* A business purpose
* A model that holds meaning only inside this context
* Terms defined in the Ubiquitous Language

### Entities in a context:

* An Entity belongs to **ONE** and only one context.
* Its meaning exists only inside that context.
* No sharing of the same “Product” across contexts.
  (`Product` in Catalog != `Product` in Ordering != `Product` in Inventory)

### Aggregates:

* A cluster of Entities you access via **one root**
* The Aggregate Root = **the only entry point**
* The root enforces invariants (consistency rules)

Example for Solange Bernard RTW:

* ProductAggregate: ProductRoot + Variants + Attributes
* OrderAggregate: OrderRoot + LineItems
* CustomerAggregate: CustomerRoot + Addresses

---

# 🟨 6. **Ubiquitous Language**

The shared business language across:

* Domain model
* Code
* Docs
* Conversations

Rules:

* Entities named after **roles**, not actors
* Everyone uses the same terms
* If the business says “Order Placed”, your event is `OrderPlaced`
* If the business says “Customer Preferences”, your VO is `CustomerPreferences`

You and I will craft this language for the RTW platform soon.

---

# 🟫 7. **One Entity = One Context**

You avoid using the same entity across bounded contexts.

Bad:

* A single “Product” table for Pricing + Catalog + Orders

Good:

* ProductCatalog.Product
* Ordering.PricedProductSnapshot
* Inventory.StockItem

DDD pushes you AWAY from shared database designs.
Each context owns its model and data.

---

# 🟩 8. **Choreography (Reactive Systems)**

DDD strongly favors **asynchronous**, **decoupled** communication.

### Publish/Subscribe

* Publishers emit events (they don’t know who listens)
* Subscribers react to those events
* You can add/remove subscribers without breaking publishers

### Why it matters:

* Upstream doesn’t depend on downstream
* Downstream services can change safely
* It is perfect for microservices and modular monoliths

### Event brokers to use:

* Kafka
* RabbitMQ
* NATS
* Even simple in-memory event bus during MVP

For you:

* MVP → in-process DomainEvents
* Later → event bus → microservices

---

# 🟦 9. **Event Storming** (the best DDD design technique)

Event Storming lets you collaboratively discover:

* Events
* Activities
* Entities
* Roles
* Bounded Contexts
* Workflows
* Command/Policy flows

### Color system:

* **Orange = Event** (the most important)
* Blue = Action
* Red = Questions
* Purple = Policy
* Yellow = Human Actor
* Pink = External Systems

### How:

1. Pick a **single user story**
2. Identify its domain-level events
3. Place them chronologically
4. Identify actions and actors
5. Identify invariants
6. Cluster patterns → Bounded Contexts emerge

### Event definition:

* Something meaningful that **already happened**
* In **past tense**
* Something the business cares about

---

# 🟩 10. What Event Storming reveals

* Full flow of operations
* Who triggers what
* Where boundaries exist
* Where Aggregates live
* Which contexts need to talk to each other
* Which policies react to which events

This is how you will design:

* RTW Product domain
* Atelier / custom tailoring domain
* Order flows
* Measurements
* Inventory
