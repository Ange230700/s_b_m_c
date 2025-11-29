<!-- README.md -->

# 🧵 **Solange Bernard — Maison de Couture Platform**

A modern **all-in-one SaaS** built from the ground up for couture ateliers.

It centralizes and elevates every operational, creative, and commercial workflow of an atelier:

* client reception & measurement tracking
* model selection & creative validation
* production planning & team coordination
* appointments & delivery schedule
* inventory & materials management
* revenue, expenses & insights
* marketing & client engagement automation

The mission is simple:
**Empower couture ateliers to deliver excellence, streamline their workflow, and grow sustainably.**

📚 **Documentation**
See more in [`/docs`](./docs).

---

# Workflow of a Couture Atelier

1. **Client Reception & Measurement**

   * Understand client’s expectations and vision
   * Take detailed measurements
   * Record notes, fabrics, inspirations

2. **Model Selection & Design Validation**

   * Client chooses model
   * Designer provides sketch or proposal
   * Approval + revisions captured digitally
   * Delivery appointment is planned

3. **Production Planning & Tracking**

   * Internal calendar planning
   * Team task assignments
   * Deadlines per stage (cutting → sewing → QC)
   * Real-time progress status

4. **Appointment & Delivery Scheduling**

   * Fittings
   * Mid-stage adjustments
   * Delivery

5. **Production Pipeline**

   * Cutting
   * Sewing
   * QC preparation

6. **Quality Control (currently missing)**

   * Verify conformity to model
   * Measurement accuracy
   * Finishing/stitching check
   * Photo reference & issue flags

---

# Technology Stack

### **Design & Productivity**

* Mermaid (diagrams)
* DrawSQL (database schema)
* Figma (UX/UI)
* VS Code
* Git + GitHub
* Agile + Scrum
* Jira

### **Core Stack**

* **TypeScript-first** ecosystem
* Node.js, Express
* PostgreSQL + MongoDB
* Prisma ORM

### **Frontend**

* React + Vite
* PrimeReact
* TailwindCSS
* i18next

### **State & Data**

* Zustand
* React Query
* GraphQL (Apollo)
* Redis

### **Mobile**

* Expo
* React Native

### **DevOps**

* pnpm (Monorepo)
* Docker
* GitHub Actions
* Husky + lint-staged
* Commitlint
* validate-branch-name

### **Testing**

* Vitest
* React Testing Library
* Supertest
* Postman
* Playwright

### **Infra & Delivery**

* AWS (EC2, S3, RDS)
* Cloudflare
* Vercel
* Render
* AlwaysData

### **Other**

* Stripe
* Socket.io
* Swagger
* Sentry
* Electron

---

# Roles at Solange Bernard’s Atelier

### **Receptionist / Manager**

* Welcome clients
* Take measurements
* Manage appointments
* Maintain client files
* Communicate with production team
* Handle follow-ups

### **Cutter**

* Interpret patterns & sketches
* Cut fabric accurately
* Collaborate with designers & seamstresses

### **Seamstress / Tailor**

* Sew according to specs
* Perform fittings
* Adjustments
* Ensure finishing quality

### **Quality Control Specialist (to introduce)**

* Inspect finished garments
* Validate against design & measurements
* Document issues
* Tag garments “Ready / Needs Fix / Reject”

---

# Problems to Solve

## 1. Sur-mesure is draining and not profitable enough

* Huge time investment per client
* Physically exhausting
* Margins too low

## 2. No visibility or marketing

* No online presence
* No strategy
* Word-of-mouth only

## 3. Information chaos

* Paper-based measurement sheets
* No centralized system
* Progress not tracked
* Missed appointments
* Scattered info everywhere

## 4. Quality Control Issues

* Measurement errors
* Model deviations
* Stitching problems

## 5. Productivity & Motivation

* No performance tracking
* No employee incentives
* No KPIs

---

# Top Priorities

## **PRIORITY #1 — Ready-to-Wear**

* Collection plan
* Stock system
* E-commerce
* Size chart management
* Photo catalog
* Visibility strategy

## **PRIORITY #2 — Marketing & Visibility**

* Revamp Facebook page
* Early teasers for RTW line

## **PRIORITY #3 — Information Flow**

Digitize everything:

* Measurements
* Model approvals
* Production calendar
* Appointments
* Clients
* Inventory

## **PRIORITY #4 — Quality Control**

Checklist system:

* Measurement accuracy
* Model conformity
* Stitching quality

## **PRIORITY #5 — Productivity**

* Soft KPIs
* Training
* Bonuses

---

# Features

### **Ready-to-Wear Module (TOP PRIORITY)**

* Online catalog
* E-commerce
* Size guide
* Mobile money + Stripe

### **Client Intake**

* Client file
* Vision notes
* Model sketches
* Approval workflow

### **Measurement Form**

* Digital, searchable
* Shareable
* QC integration

### **Dual Production Calendar**

* Internal calendar
* Client-facing calendar
* Automated reminders
* Dashboard view

### **Production Pipeline**

* Not Started → Cutting → Sewing → QC → Ready
* Task assignment
* Deadlines per step

### **Quality Control**

* Mandatory QC checklist
* Measurement comparison
* Photos
* Error flags

### **Inventory**

* Fabrics
* Materials
* Tools
* Supplier info
* Low stock alerts

### **Performance & Payroll**

* Productivity indicators
* Bonus logic
* Staff history

---

# Career Development Inside the Platform

* Talent acquisition module
* Training tracks for beginners
* Upskilling for transitions
* Long-term talent pipeline

---

# Engineering Best Practices for Solange Bernard

* UX/UI Inspirations (Awwwards, Dribbble…)
* Style guide & design system discipline
* Scrum with Jira
* Clean Architecture
* TDD
* CI/CD
* Domain-Driven Design
* Microservices (API Gateway, service discovery, DB per service)
* UML & Mermaid
* JSDoc
* Quality tools
* A11y & i18n
* Security & privacy
* Performance optimization
* Monitoring & logging
* SEO
* User Settings & Preferences
* Responsive + Mobile-first
* PWA + Offline sync
* Scalability planning

---

# 🧵 Design Directory (Linked to Jira Workflow)

| Folder          | Jira Phase                       | Purpose                                 |
| --------------- | -------------------------------- | --------------------------------------- |
| `inspirations/` | Creative Discovery & Inspiration | Moodboards, references, benchmarks      |
| `ux-flows/`     | Creative Discovery & Inspiration | User journeys, personas, diagrams       |
| `wireframes/`   | Wireframing & UX Blueprint       | Low-fi layouts & IA                     |
| `mockups/`      | Mockups & Visual Design          | Figma exports, high-fi screens          |
| `style-guide/`  | Visual System                    | Tokens, palette, typography, components |

Each artefact is versioned and linked to Jira for traceability.
