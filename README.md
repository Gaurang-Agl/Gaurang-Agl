<span id="top"></span>
<div align="center">

<img src="./assets/git_profile_banner.jpg" width="100%" alt="Gaurang Agarwal — Senior QA Engineer & Backend Software Developer" />

<br />

**Senior QA Engineer (7+ Yrs) · Backend Software Developer**

7+ years ensuring high software quality & reliability, actively engineering backend services with Python, Django, Celery, and PostgreSQL.

[![RECOMMENDATIONS](https://img.shields.io/badge/RECOMMENDATIONS-LINKEDIN-00E5FF?style=for-the-badge&logo=linkedin&logoColor=white&labelColor=0d1117)](https://www.linkedin.com/in/gaurang-agl/details/recommendations/)
[![REPOSITORIES](https://img.shields.io/badge/REPOSITORIES-5%20ACTIVE-00E5FF?style=for-the-badge&logo=github&logoColor=white&labelColor=0d1117)](https://github.com/Gaurang-Agl?tab=repositories)
![PROFILE VIEWS](https://hits.sh/github.com/Gaurang-Agl/profile.svg?style=for-the-badge&label=PROFILE+VIEWS&color=00e5ff&labelColor=0d1117)

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

```text
01  ASYNCHRONOUS WORKERS      Periodic polling, background tasks & alert dispatches (Celery / Redis)
02  MULTI-TENANCY & RBAC      Role-based access control, tenant isolation & audit logging
03  API PLATFORMS & GATEWAYS  API key authentication, JWT security tokens & query analytics
04  CONCURRENCY & INTEGRITY   Atomic database transactions & overbooking prevention
```

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

#### ⚡ [EventHub — Concurrency-Safe Ticketing & Seat Reservation Platform](https://github.com/Gaurang-Agl/EventHub)
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

### `03 / ENTERPRISE & PRIVATE CONTRIBUTIONS (A BRIEF GLIMPSE)`

```text
ENTERPRISE WORK UNDER PROPRIETARY / CLIENT NDAs
```

While proprietary codebases and production enterprise repositories remain private under strict NDAs, here is a structured summary of the systems, architectures, and testing platforms delivered across **7+ years in enterprise environments**:

```text
01  AUTOMATION FRAMEWORKS    Engineered modular test automation suites using Python, Pytest, and Selenium/Playwright
02  API VALIDATION PIPELINES Authored extensive contract & regression test suites with Postman, Newman & CI/CD
03  PERFORMANCE & LOAD RIGS  Conducted throughput validation and latency profiling under simulated peak traffic
04  DATA INTEGRITY SUITES    Authored automated database assertion scripts validating ETL workflows & mutations
05  INTERNAL DEVELOPER TOOLS Built workflow automation scripts & mock services streamlining team QA cycles
```

| Domain | Scope & Technical Implementation | Impact / Outcome |
| :--- | :--- | :--- |
| **Enterprise Test Frameworks** | Designed and maintained scalable automation frameworks in Python (Pytest) with custom fixtures, multi-browser parallel execution, and detailed HTML reporting. | Reduced regression cycle times by over 60% and prevented high-severity defects prior to production. |
| **API Contract & Integration Testing** | Built end-to-end API test suites using Postman, Newman CLI, and REST client libraries, integrating test stages into CI/CD pipelines. | Guaranteed strict contract compliance across microservices and eliminated payload breaking changes. |
| **Defect Root-Cause & Code Tracing** | Traced defects directly through application logs, database queries, and backend codebase flows rather than reporting superficial symptoms. | Drastically shortened bug triage time and strengthened technical collaboration with development teams. |
| **Agile Quality Delivery** | Partnered in sprint planning, user story grooming, defect triage meetings, and cross-functional release management. | Championed Shift-Left quality principles ensuring requirements and acceptance criteria were testable early. |

> [!NOTE]
> *Repository code, proprietary business logic, and internal API credentials are confidential. However, the architectural design, defensive coding standards, and rigorous validation methodologies developed across these enterprise engagements directly inform my public backend projects.*

---

### `04 / TECHNICAL TOOLKIT`

| Category | Skills & Technologies |
| :--- | :--- |
| **Quality Engineering (7+ Yrs Core)** | Test Strategy & Planning · Functional & Regression Testing · API Testing (Postman/Newman) · Test Automation Principles · Defect Root-Cause Analysis · Shift-Left QA · Agile / Scrum |
| **Backend Development (Projects)** | Python (3.12+ / 3.14) · Django · Django REST Framework (DRF) · Celery · Celery Beat · RESTful API Design · Async Task Pipelines |
| **Databases, Caching & Queues** | PostgreSQL (17) · SQLite · Redis (Message Broker & Caching) · Relational Data Modeling · Transaction Safety (`transaction.atomic`) |
| **DevOps, Environments & Tooling** | Cursor · Docker · Docker Compose · GitHub Actions · Postman API Collections · VS Code |

<div align="center">

<a href="https://www.python.org" target="_blank" title="Python"><img src="https://skillicons.dev/icons?i=py" height="40" alt="Python" /></a> &nbsp;
<a href="https://www.djangoproject.com" target="_blank" title="Django"><img src="https://skillicons.dev/icons?i=django" height="40" alt="Django" /></a> &nbsp;
<a href="https://www.postgresql.org" target="_blank" title="PostgreSQL"><img src="https://skillicons.dev/icons?i=postgres" height="40" alt="PostgreSQL" /></a> &nbsp;
<a href="https://redis.io" target="_blank" title="Redis"><img src="https://skillicons.dev/icons?i=redis" height="40" alt="Redis" /></a> &nbsp;
<a href="https://www.postman.com" target="_blank" title="Postman"><img src="https://skillicons.dev/icons?i=postman" height="40" alt="Postman" /></a> &nbsp;
<a href="https://www.docker.com" target="_blank" title="Docker"><img src="https://skillicons.dev/icons?i=docker" height="40" alt="Docker" /></a> &nbsp;
<a href="https://github.com/features/actions" target="_blank" title="GitHub Actions"><img src="https://skillicons.dev/icons?i=githubactions" height="40" alt="GitHub Actions" /></a> &nbsp;
<a href="https://code.visualstudio.com" target="_blank" title="VS Code"><img src="https://skillicons.dev/icons?i=vscode" height="40" alt="VS Code" /></a> &nbsp;
<a href="https://cursor.com" target="_blank" title="Cursor Code Editor"><img src="./assets/cursor.svg" height="40" alt="Cursor" /></a>

<br /><br />

<a href="https://www.postman.com" target="_blank" title="Postman API Platform"><img src="https://img.shields.io/badge/API_TESTED-POSTMAN-0B1220?style=for-the-badge&logo=postman&logoColor=55B6FF" alt="Postman" /></a>
<a href="https://docs.docker.com/compose/" target="_blank" title="Docker Compose Documentation"><img src="https://img.shields.io/badge/CONTAINERIZED-DOCKER_COMPOSE-0B1220?style=for-the-badge&logo=docker&logoColor=55B6FF" alt="Docker Compose" /></a>
<a href="https://cursor.com" target="_blank" title="Cursor Code Editor"><img src="https://img.shields.io/badge/DEVELOPED_WITH-CURSOR-0B1220?style=for-the-badge&logo=cursor&logoColor=55B6FF" alt="Cursor" /></a>

</div>

---

### `05 / GITHUB ACTIVITY & METRICS`

<div align="center">

<!-- Real-Time Activity Line Graph -->
<a href="https://github.com/Gaurang-Agl?tab=overview" target="_blank">
  <img width="98%" src="https://arshbibhaw-github-activity-graph.vercel.app/graph?username=Gaurang-Agl&amp;bg_color=080D17&amp;color=8EAFCB&amp;line=258DFF&amp;point=64DDFF&amp;area=true&amp;hide_border=true" alt="GitHub contribution activity graph" />
</a>

<sub><a href="https://github.com/Gaurang-Agl?tab=overview">View live contribution activity directly on GitHub →</a></sub>

</div>

<br />

<!-- GitHub Contribution Calendar Heatmap Section -->
<div align="center">
  <a href="https://github.com/Gaurang-Agl?tab=overview" target="_blank">
    <img width="98%" src="https://github-readme-stats.vercel.app/api?username=Gaurang-Agl&show_icons=true&hide_border=true&bg_color=080D17&title_color=55B6FF&text_color=C6D7E8&icon_color=258DFF" alt="GitHub statistics" />
  </a>
</div>

<details>
<summary><strong>📊 Telemetry &amp; Repository Analytics</strong></summary>

<br />

<div align="center">

<img height="165" src="https://github-readme-stats.vercel.app/api?username=Gaurang-Agl&show_icons=true&hide_border=true&bg_color=080D17&title_color=55B6FF&text_color=C6D7E8&icon_color=258DFF" alt="GitHub statistics" />
<img height="165" src="https://github-readme-streak-stats.herokuapp.com/?user=Gaurang-Agl&hide_border=true&background=080D17&stroke=243448&ring=258DFF&fire=55B6FF&currStreakLabel=C6D7E8&sideLabels=C6D7E8&dates=8EAFCB" alt="GitHub streak statistics" />

</div>

</details>

---

### `06 / THE HYBRID ADVANTAGE`

```text
7+ YEARS OF QA INDUSTRY MATURITY  +  HANDS-ON PYTHON & BACKEND CAPABILITY
```

Why this combination is a distinct asset whether evaluating for Backend Development or Senior QA roles:

- **When Hiring for Backend Developer Roles:**
  - **No Process Hand-Holding Needed:** Unlike college freshers, I have 7+ years of experience working inside software teams. I know how sprint planning, sprint retros, PR reviews, CI/CD pipelines, and cross-functional handoffs work in practice.
  - **Defensive, Edge-Case-Aware Coding:** Having spent 7 years finding edge cases in other people’s code, I naturally write backend logic with input validation, graceful error handling, and concurrency safeguards upfront.
  - **Built-in Quality & Testing:** Every API and model I build is developed with automated verification and Postman collections from day one.

- **When Hiring for Senior QA / SDET Roles:**
  - **Code-Level Understanding:** I do not treat backends as black boxes. I can read Python/Django source code, trace ORM queries, inspect Celery worker queues, and debug issues at the code level.
  - **Stronger Developer Collaboration:** Knowing how to write backend services means I speak the same technical language as developers, speeding up bug triages and root cause resolution.

---

### `07 / ENGINEERING PRINCIPLES`

- **Process & Reliability:** Established processes, clear code reviews, and structured testing produce stable production releases.
- **Defensive Engineering:** Anticipating edge cases, handling nulls/exceptions, and validating inputs early saves hours of debugging.
- **Continuous Learning:** Eager to grasp, learn, and implement modern backend technologies while leveraging established QA experience.
- **Clarity & Documentation:** Code should be readable, APIs should have clear contracts, and Postman collections should be reproducible.

---

<div align="center">

**Open to backend software developer roles or senior QA opportunities.**

<br/>

[![Portfolio](https://img.shields.io/badge/LIVE_PORTFOLIO-00E5FF?style=for-the-badge&logo=netlify&logoColor=0B1220)](https://portfolio-gaurang.netlify.app/)
[![LinkedIn](https://img.shields.io/badge/LINKEDIN-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/gaurang-agl/)
[![Email](https://img.shields.io/badge/EMAIL-gaurang.mragarwal@gmail.com-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:gaurang.mragarwal@gmail.com)

<br/>

<sub>Tested with discipline. Built with curiosity.</sub>

</div>

<p align="right"><a href="#top" title="Back to top"><b>⬆ Back to Top</b></a></p>
