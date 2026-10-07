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

#### 🚀 [PulseNotify — Flight Price Monitor & Asynchronous Alert Engine](https://github.com/Gaurang-Agl/PulseNotify)
> **Stack:** Python 3.14 · Django REST Framework · Celery · Celery Beat · Redis · PostgreSQL · Docker Compose
- **Engine Architecture:** Modeled after distributed price-alert systems in Google Flights and Skyscanner. Tracks non-blocking route thresholds (e.g., `DEL-BOM` under ₹4,500) and triggers automated dispatches upon price drops.
- **Asynchronous Task Architecture:**
  - Configured **Celery Beat** to wake periodic worker processes every 60 seconds without manual intervention.
  - Workers poll route pricing, evaluate deltas against stored alerts, and fire `send_notification.delay()` asynchronously to log notification history and update alert states.
  - Query Optimization: Extracts distinct origin-destination pairs via `active_alerts.values_list('origin', 'destination').distinct()` to query external price feeds once per route rather than once per alert.
  - Internal simulation feed (`/api/flights/price/`) dynamically models live fare fluctuations for realistic end-to-end testing.
- **Data Modeling & Access Control:**
  - Models: `UserProfile` (auto-created via `post_save` signals), `PriceAlert`, and `NotificationLog`.
  - Enforces user-scoped query isolation and a custom `IsAdminUser` permission layer for platform telemetry.
  - Soft Delete: Deleted alerts transition to `inactive` instead of SQL `DELETE`, preserving audit trails and metrics.
- **DevOps & Testing:**
  - Split settings architecture (`config/settings/base.py`, `local.py`, `production.py`).
  - Multi-container `docker-compose.yml` orchestrating PostgreSQL and Redis broker services with healthchecks.
  - Automated Postman collection (`PulseNotify.postman_collection.json`) validating alert lifecycles and token propagation.


#### 🛡️ [CollabDocs — Multi-Tenant Collaborative Document Platform](https://github.com/Gaurang-Agl/CollabDocs)
> **Stack:** Python · Django 5.2.6 · DRF 3.16.1 · PostgreSQL (`psycopg 3`) · Postman Collections
- **Multi-Tenant Architecture:** Enterprise workspace backend providing tenant-isolated workspaces with granular Role-Based Access Control (**Admin, Editor, Viewer**).
- **Relational Data Integrity & 8 UUID Models:**
  - Custom data architecture built across 8 UUID-keyed models: `User`, `Workspace`, `WorkspaceMember`, `Document`, `DocumentVersion`, `Comment`, `Tag`, and `AuditLog`.
  - Uses `transaction.atomic()` to guarantee rollback safety during workspace provisioning and snapshot generation for document revision history.
- **ORM Optimization & High-Efficiency Queries:**
  - Extensively tuned queries utilizing `select_related`, `prefetch_related`, `distinct()`, `values_list()`, and complex `Q` object lookups to eliminate $N+1$ query overhead.
  - Real-time aggregation endpoints for workspace summaries and document stats powered by `Count`, `annotate()`, and `aggregate()`.
- **Audit Logging & Quality Rigor:**
  - Custom request-duration middleware profiling endpoint performance in milliseconds.
  - Signal-driven `AuditLog` generation via `post_save` on `Document` checking `instance._state.adding` to automatically track user modifications.
  - **31 Automated Test Cases** in `collaboration/tests.py` (1,112 lines of tests) covering atomic creation, rollback on duplicate member conflicts (409 Conflict), sequential versioning, and RBAC enforcement.
  - Accompanied by a comprehensive 252-line security audit (`API_ANALYSIS_AND_IMPROVEMENTS.md`) detailing boundary condition handling and privilege escalation guards.


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

