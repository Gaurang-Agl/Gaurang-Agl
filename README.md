<div align="center">

<img src="./assets/banner.svg" width="100%" alt="Gaurang Agarwal — Senior QA Engineer & Backend Software Developer" />

<br />

**Senior QA Engineer (7+ Yrs) · Backend Software Developer**

</div>

---

### `01 / ABOUT`

I am a **Software Quality Engineer with 7+ years of experience** spanning enterprise QA, automated API validation, and full software development lifecycles (SDLC), actively expanding my career into **Backend Software Engineering**.

While entering backend software engineering without years of dedicated backend developer job titles, I am **not a typical fresher**. I bring 7+ years of deep familiarity with software delivery processes, agile sprint planning, code review workflows, defect lifecycle management, and cross-functional team collaboration. To bridge this with hands-on coding, I build production-grade backend services using **Python, Django REST Framework, Celery worker queues, Redis, and PostgreSQL**—delivering clean, reliable, defensive, and thoroughly tested APIs.

```text
PRIMARY DOMAIN       7+ Years in Software Quality Assurance & Test Engineering
BACKEND CAPABILITY   Hands-on Production-Style Systems (Python, DRF, Celery, Redis, PostgreSQL)
PROCESS MATURITY     Agile/Scrum • CI/CD Delivery • API Testing • Root Cause Analysis • Defect Prevention
TARGET ROLES         Backend Software Developer & Senior QA / SDET Roles
DEVELOPMENT TOOLS    Cursor • VS Code • Postman • Docker Desktop • GitHub Actions
```

---


### `02 / FEATURED SYSTEMS & REPOSITORIES (PUBLIC DEEP-DIVE)`

#### 🏢 [TeamBoard (B2BKnowledgeBase) — Enterprise B2B Knowledge Platform](https://github.com/Gaurang-Agl/B2BKnowledgeBase)
> **Stack:** Python 3.14 · Django 6.1 · Django REST Framework · Simple JWT · PostgreSQL 17 · Docker Compose
- **Platform Architecture:** Centralized B2B Knowledge Base API service serving multi-company client applications with dual authentication (Company API Key + JWT Bearer tokens).
- **Authentication Gateway & Query Telemetry:**
  - Company self-service registration automatically issues cryptographically secure 64-character API keys using `secrets.token_urlsafe(32)`.
  - Secure JWT authentication (`Simple JWT`) governs user-level access to full-text knowledge base queries.
  - Built-in query logging middleware and admin usage statistics tracking endpoint consumption across tenant companies.
  - Zero-Result Query Logging: Unmatched queries are recorded in `QueryLog` to detect customer documentation gaps.
- **Deterministic Seeding & Containerization:**
  - Custom Django management command (`python manage.py seed_kb`) providing automated database population with baseline knowledge entries for testing and CI.
  - Containerized PostgreSQL 17 managed via Docker Compose for clean, reproducible development and staging environments.
  - Full API validation suite via `B2BKnowledgeBase_Postman_Collection.json` covering 11 distinct scenarios.


#### ⚡ [EventHub — Concurrency-Safe Ticketing & Seat Reservation Platform](https://github.com/Gaurang-Agl/EventHub-Assignment)
> **Stack:** Python · Django · Django REST Framework · SQLite / PostgreSQL · Custom Middleware
- **Concurrency & Anti-Overbooking Engine:** High-volume event booking backend designed to prevent race conditions and double-booking anomalies during peak ticket drops.
- **Transactional Integrity:**
  - Single Source of Truth: Inventory deductions are encapsulated inside `ReservationSerializer.create()` to guarantee reservations cannot exist without inventory reduction.
  - Dynamic seat restoration logic that safely replenishes venue availability when reservations are cancelled or expire, with idempotent protection against re-cancellation.
- **Performance Middleware & Filtering:**
  - Custom request/response logging middleware (`middleware.py`) tracking HTTP methods, status codes, and latency in milliseconds.
  - Multi-parameter query filtering on event listings (by status, venue, date ranges).

👉 *Explore all public source code:* **[View All Public Repositories →](https://github.com/Gaurang-Agl?tab=repositories)**

---

