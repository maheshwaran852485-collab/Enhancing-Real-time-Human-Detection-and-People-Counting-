# CIAIFRS Command Center

> **Cyber Incident & Artifact Integrity Forensic Readiness System**

![Next.js](https://img.shields.io/badge/Next.js-16-black?logo=next.js) ![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript&logoColor=white) ![Prisma](https://img.shields.io/badge/Prisma-5-2D3748?logo=prisma) ![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-4-06B6D4?logo=tailwindcss&logoColor=white) ![License](https://img.shields.io/badge/License-MIT-green)

Enterprise-grade digital evidence management and forensic readiness platform designed for SOC teams, incident responders, auditors, and forensic investigators. Built to securely manage, track, and validate digital artifacts throughout the entire cyber incident lifecycle — from detection to court-ready reporting.

![CIAIFRS Dashboard](./screenshots/dashboard.png)

---

## Table of Contents

- [About the Project](#about-the-project)
- [Key Features](#key-features)
- [Screenshots](#screenshots)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Project Structure](#project-structure)
- [Domain Modules](#domain-modules)
- [Dashboard Pages](#dashboard-pages)
- [UI Components](#ui-components)
- [Database Schema](#database-schema)
- [Security & Access Control](#security--access-control)
- [Blockchain Integrity Ledger](#blockchain-integrity-ledger)
- [AI & Forensic Analysis](#ai--forensic-analysis)
- [Getting Started](#getting-started)
- [Operational Guide](./OPERATIONAL_GUIDE.md)
- [Default Credentials](#default-credentials)
- [Available Scripts](#available-scripts)
- [License](#license)
- [Acknowledgments](#acknowledgments)

---

## About the Project

CIAIFRS (Cyber Incident & Artifact Integrity Forensic Readiness System) is a **workflow-driven** platform that follows the incident lifecycle pipeline:

```
Intake → Verify → Monitor → Investigate → Report
```

The system is built around the concept that during a real-world cyber incident, digital evidence must be:
1. **Registered** with proper chain of custody
2. **Verified** for integrity using cryptographic hashes
3. **Monitored** for tampering or unauthorized access
4. **Investigated** through timeline reconstruction and correlation analysis
5. **Reported** with court-admissible documentation and export capabilities

The dashboard presents a **live incident scenario** that demonstrates how these modules work together during an active investigation, including real-time status indicators, role-based perspectives, and a correlation summary.

---

## Key Features

### 🔐 Evidence Management
- Register digital artifacts with metadata, file uploads, and voice notes
- SHA-256 file hashing at ingestion for tamper detection
- Geolocation tagging for evidence collection points
- Interactive evidence map visualization (Leaflet)
- QR code generation for physical-digital evidence linking
- Digital file viewer with multi-format support

### ⛓️ Blockchain-Style Integrity Ledger
- Immutable audit trail for all custody transfers
- Each log entry chains to the previous via hash linkage
- Digital signature simulation for transfer verification
- Visual blockchain explorer with chain validation UI
- Real-time blockchain sync status monitoring

### 🛡️ Access Control & Security
- Role-Based Access Control (RBAC) with 4 roles: ADMIN, SOC, RESPONDER, AUDITOR
- PIN-based custody transfer verification
- Route-level API protection via Next.js middleware
- Feature-level permission matrix enforcement
- All access attempts are logged for audit compliance

### 📊 Real-Time Monitoring & Alerts
- Security alert ingestion (Failed Login, Admin Login, Artifact Modification, Rule Trigger)
- Severity classification: LOW, MEDIUM, HIGH, CRITICAL
- Alert sidebar with real-time notifications
- Analytics dashboard with intake charts, status charts, and live terminal feeds

### 🔍 Investigation & Correlation
- Timeline reconstruction from custody logs and events
- AI-driven cross-artifact correlation engine
- Relationship graph visualization (force-directed)
- Pattern detection across evidence chains
- Incident timeline with step-by-step event tracking

### 📋 Forensic Readiness
- Readiness assessment scoring system
- Readiness trend graph over time (Recharts)
- Incident simulation panel with scenario testing
- Dark web exposure monitoring module
- Trust score calculation for evidence reliability

### 📄 Reporting & Export
- PDF report generation (jsPDF + jspdf-autotable)
- Court-ready evidence documentation export
- User management with role assignment interface
- Administrative controls and system configuration

### 🎨 UI/UX Design
- Dark mode glassmorphism design with animated backgrounds
- Framer Motion page transitions and micro-animations
- Collapsible sidebar with grouped navigation
- Role-based dashboard perspective cards
- Active incident scenario narrative on dashboard
- Responsive layout for desktop and tablet

---

## Screenshots

| Dashboard | Evidence Intake | Evidence Details |
|---|---|---|
| ![Dashboard](./screenshots/dashboard.png) | ![Intake](./screenshots/intake.png) | ![Details](./screenshots/details.png) |

| Investigation Hub | Correlation Analysis | Network Graph |
|---|---|---|
| ![Investigation](./screenshots/investigation.png) | ![Correlation](./screenshots/correlation.png) | ![Network](./screenshots/network.png) |

| Alerts Panel | Analytics Dashboard | Reports Center |
|---|---|---|
| ![Alerts](./screenshots/alerts.png) | ![Analytics](./screenshots/analytics.png) | ![Reports](./screenshots/reports.png) |

| Audit View |
|---|
| ![Audit](./screenshots/audit.png) |

---

## Tech Stack

| Layer          | Technology                                          |
| -------------- | --------------------------------------------------- |
| **Framework**  | Next.js 16 (App Router, Server Components, Server Actions) |
| **Language**   | TypeScript 5                                        |
| **Database**   | SQLite via Prisma ORM 5                             |
| **Auth**       | Cookie-based sessions with RBAC                     |
| **Styling**    | Tailwind CSS 4, custom glassmorphism                |
| **Animations** | Framer Motion 12                                    |
| **Charts**     | Recharts 3                                          |
| **Maps**       | Leaflet + React-Leaflet 5                           |
| **PDF**        | jsPDF + jspdf-autotable                             |
| **QR Codes**   | qrcode.react                                        |
| **Graph**      | react-force-graph-2d                                |
| **Icons**      | Lucide React                                        |
| **Toasts**     | Sonner                                              |
| **Utilities**  | clsx, tailwind-merge, date-fns                      |

---

## Architecture

The project follows a **domain-driven, layered architecture** with clear separation of concerns:

```
┌─────────────────────────────────────────────────────┐
│                    UI Layer                          │
│  (app/, components/) — React pages & components     │
├─────────────────────────────────────────────────────┤
│                  Logic Layer                         │
│  (modules/) — Domain controllers & server actions   │
├─────────────────────────────────────────────────────┤
│                 Service Layer                        │
│  (services/) — Business logic orchestration         │
├─────────────────────────────────────────────────────┤
│                  Data Layer                          │
│  (lib/db.ts, prisma/) — Prisma ORM & database       │
├─────────────────────────────────────────────────────┤
│                Security Layer                        │
│  (middleware/) — RBAC, auth guards, permissions      │
├─────────────────────────────────────────────────────┤
│                 Utility Layer                        │
│  (lib/) — Crypto, hashing, AI, forensics, PDF, etc. │
└─────────────────────────────────────────────────────┘
```

**Key Architectural Decisions:**

1. **Next.js App Router** — All pages use the new App Router with server components for data fetching and server actions for mutations.
2. **Server Actions as Controllers** — Each domain module has `*.controller.ts` files that use the `'use server'` directive, exposing server actions directly to UI components without needing API routes.
3. **Domain-Driven Modules** — Business logic is organized by domain (artifact, integrity, investigation, monitoring, readiness, admin) rather than by technical layer.
4. **Prisma ORM** — Single source of truth for the database schema, with a centralized client in `lib/db.ts`.
5. **Cookie-Based Auth** — Session data is stored in a `des_session` cookie containing `userId`, `role`, and `name`.

---

## Project Structure

```
proj/
├── prisma/
│   ├── schema.prisma           # Database schema (5 models)
│   ├── migrations/             # Migration history
│   └── seed.ts                 # Database seeding script
│
├── public/                     # Static assets
│
├── src/
│   ├── app/                    # Next.js App Router
│   │   ├── layout.tsx          # Root layout (fonts, Toaster, global CSS)
│   │   ├── globals.css         # Global styles & Tailwind directives
│   │   ├── login/              # Login page (role selector + PIN auth)
│   │   ├── auth/               # Auth server actions (login/logout)
│   │   └── (dashboard)/        # Authenticated dashboard routes
│   │       ├── layout.tsx      # Dashboard layout (sidebar wrapper)
│   │       ├── page.tsx        # Main dashboard (lifecycle, metrics, scenario)
│   │       ├── intake/         # Evidence registration form
│   │       ├── evidence/       # Evidence list + detail pages
│   │       ├── monitoring/     # Real-time monitoring NOC
│   │       ├── alerts/         # Alert management panel
│   │       ├── timeline/       # Event timeline reconstruction
│   │       ├── correlation/    # Cross-artifact correlation analysis
│   │       ├── investigation/  # Investigation workspace
│   │       ├── network/        # Network relationship graph
│   │       ├── lab/            # Tamper detection lab console
│   │       ├── readiness/      # Forensic readiness assessment
│   │       ├── readiness-analytics/ # Readiness trend analytics
│   │       ├── simulation/     # Incident simulation panel
│   │       ├── dark-web/       # Dark web exposure checks
│   │       ├── reports/        # Report export center
│   │       └── admin/          # User management (ADMIN only)
│   │
│   ├── components/             # Reusable UI components (39 files)
│   │   ├── Sidebar.tsx         # Collapsible navigation with role-based groups
│   │   ├── EvidenceForm.tsx    # Multi-field evidence registration form
│   │   ├── TransferForm.tsx    # PIN-verified custody transfer form
│   │   ├── AlertsPanel.tsx     # Alert list with severity filtering
│   │   ├── AlertSidebar.tsx    # Slide-out alert notifications
│   │   ├── CorrelationPanel.tsx # AI-powered correlation analysis
│   │   ├── SimulationPanel.tsx # Incident simulation controls
│   │   ├── TamperLabConsole.tsx # Tamper detection lab interface
│   │   ├── TamperReplay.tsx    # Tamper event replay viewer
│   │   ├── TrustScoreCard.tsx  # Evidence trust score display
│   │   ├── EvidenceTimeline.tsx # Visual timeline for evidence events
│   │   ├── EvidenceMap.tsx     # Leaflet map for geolocation
│   │   ├── IncidentTimeline.tsx # Full incident event timeline
│   │   ├── IntegrityPulse.tsx  # Real-time integrity status monitor
│   │   ├── BlockchainSync.tsx  # Blockchain ledger sync visualization
│   │   ├── BlockchainExplainer.tsx # Blockchain concept explainer UI
│   │   ├── BlockchainStatus.tsx # Blockchain chain status indicator
│   │   ├── QRCodeGenerator.tsx # QR code for evidence linking
│   │   ├── DigitalViewer.tsx   # Multi-format digital evidence viewer
│   │   ├── VoiceRecorder.tsx   # Audio voice note recorder
│   │   ├── RelationshipGraph.tsx # Force-directed relationship graph
│   │   ├── ReadinessTrendGraph.tsx # Recharts-based trend analysis
│   │   ├── ExportReports.tsx   # PDF/report export interface
│   │   ├── UserManagement.tsx  # Admin user CRUD panel
│   │   ├── AIDetectiveWidget.tsx # AI analysis assistant widget
│   │   ├── AnimatedBackground.tsx # Animated dark background effects
│   │   ├── CertificateButton.tsx # Certificate generation button
│   │   ├── PDFExportButton.tsx # PDF export trigger
│   │   ├── DashboardMetrics.tsx # Dashboard quick stats grid
│   │   ├── DashboardModules.tsx # Dashboard module cards
│   │   ├── DashboardLayout.tsx # Dashboard layout wrapper
│   │   ├── MotionWrapper.tsx   # Framer Motion animation wrapper
│   │   ├── Card.tsx            # Reusable card component
│   │   ├── StatusBadge.tsx     # Color-coded status badge
│   │   ├── SectionHeader.tsx   # Section header with styling
│   │   ├── MetricBox.tsx       # Metric display box
│   │   ├── TamperButton.tsx    # Tamper action trigger button
│   │   ├── LeafletFix.tsx      # Leaflet CSS/icon fix wrapper
│   │   ├── JudgeToggle.tsx     # Judge/Magistrate view toggle
│   │   ├── providers/          # React context providers
│   │   └── analytics/          # Analytics chart components
│   │       ├── IntakeChart.tsx  # Evidence intake trends
│   │       ├── StatusChart.tsx  # Evidence status breakdown
│   │       └── LiveTerminal.tsx # Simulated live terminal feed
│   │
│   ├── modules/                # Domain-driven server actions
│   │   ├── artifact/           # Evidence CRUD operations
│   │   │   ├── artifact.controller.ts
│   │   │   ├── artifact.service.ts
│   │   │   └── artifact.repository.ts
│   │   ├── integrity/          # Chain of custody & tamper detection
│   │   │   ├── custody.controller.ts
│   │   │   ├── integrity.controller.ts
│   │   │   ├── tamper.controller.ts
│   │   │   ├── integrity.service.ts
│   │   │   └── integrity.repository.ts
│   │   ├── investigation/      # Correlation & timeline analysis
│   │   │   ├── correlation.controller.ts
│   │   │   ├── timeline.controller.ts
│   │   │   ├── investigation.service.ts
│   │   │   └── investigation.repository.ts
│   │   ├── monitoring/         # Alerts & analytics
│   │   │   ├── alerts.controller.ts
│   │   │   ├── analytics.controller.ts
│   │   │   ├── monitoring.service.ts
│   │   │   └── monitoring.repository.ts
│   │   ├── readiness/          # Forensic readiness & simulations
│   │   │   ├── readiness.controller.ts
│   │   │   ├── simulation.controller.ts
│   │   │   ├── darkweb.controller.ts
│   │   │   ├── readiness.service.ts
│   │   │   └── readiness.repository.ts
│   │   └── admin/              # User management & reports
│   │       ├── users.controller.ts
│   │       ├── reports.controller.ts
│   │       ├── admin.service.ts
│   │       └── admin.repository.ts
│   │
│   ├── lib/                    # Shared libraries & utilities
│   │   ├── db.ts               # Prisma client singleton
│   │   ├── hash.ts             # SHA-256 hashing utility functions
│   │   ├── ai/
│   │   │   └── Analyzer.ts     # AI-powered evidence analysis engine
│   │   ├── crypto/
│   │   │   └── CryptoEngine.ts # Cryptographic operations engine
│   │   ├── forensics/
│   │   │   └── TrustScoreCalculator.ts  # Evidence trust scoring algorithm
│   │   ├── ledger/
│   │   │   ├── Blockchain.ts   # Blockchain chain management
│   │   │   └── ImmutableLog.ts # Immutable log entry creation
│   │   └── pdf/                # PDF generation utilities
│   │
│   ├── services/
│   │   └── artifact.service.ts # Business logic for artifact operations
│   │
│   ├── middleware/
│   │   └── permissions.ts      # RBAC permission matrix & helpers
│   │
│   └── middleware.ts           # Next.js root middleware (auth + API guards)
│
├── package.json
├── tsconfig.json
├── next.config.ts
├── postcss.config.mjs
└── eslint.config.mjs
```

---

## Domain Modules

Each module under `src/modules/` follows a **Controller → Service → Repository** layered pattern:

| File Pattern          | Responsibility                                    |
| --------------------- | ------------------------------------------------- |
| `*.controller.ts`     | Server action entry points (`'use server'`)       |
| `*.service.ts`        | Business logic & orchestration                    |
| `*.repository.ts`     | Database queries via Prisma                       |

### Module Details

| Module            | Controllers                           | What It Does                                                                 |
| ----------------- | ------------------------------------- | ---------------------------------------------------------------------------- |
| **artifact**      | `artifact.controller.ts`              | Evidence CRUD, file uploads, metadata management, geolocation tagging        |
| **integrity**     | `custody.controller.ts`, `integrity.controller.ts`, `tamper.controller.ts` | PIN-based custody transfers, chain validation, tamper detection & simulation |
| **investigation** | `correlation.controller.ts`, `timeline.controller.ts` | Cross-artifact correlation, AI pattern detection, timeline reconstruction    |
| **monitoring**    | `alerts.controller.ts`, `analytics.controller.ts` | Alert ingestion, severity tracking, analytics data aggregation               |
| **readiness**     | `readiness.controller.ts`, `simulation.controller.ts`, `darkweb.controller.ts` | Forensic readiness scoring, incident simulations, dark web exposure checks  |
| **admin**         | `users.controller.ts`, `reports.controller.ts` | User CRUD, role assignments, exportable PDF reports                          |

---

## Dashboard Pages

| Route                    | Page                  | Description                                                    |
| ------------------------ | --------------------- | -------------------------------------------------------------- |
| `/`                      | Dashboard Home        | Incident lifecycle pipeline, live scenario, role perspectives, metrics |
| `/intake`                | Evidence Intake       | Register new digital artifacts with metadata and file uploads  |
| `/evidence`              | Evidence List         | Browse all registered evidence with status and custodian info  |
| `/evidence/[id]`         | Evidence Detail       | Detailed view of a single artifact with custody chain          |
| `/monitoring`            | Monitoring NOC        | Real-time monitoring dashboard with live feeds                 |
| `/alerts`                | Alert Center          | Security alert management with severity filtering              |
| `/timeline`              | Event Timeline        | Chronological reconstruction of incident events                |
| `/correlation`           | Correlation Analysis  | Cross-artifact relationship and pattern detection              |
| `/investigation`         | Investigation Hub     | Central investigation workspace                                |
| `/network`               | Network Graph         | Force-directed relationship graph visualization                |
| `/lab`                   | Tamper Lab            | Tamper detection console with replay capability                |
| `/readiness`             | Readiness Assessment  | Forensic readiness scoring and evaluation                      |
| `/readiness-analytics`   | Readiness Analytics   | Trend analysis and historical readiness data                   |
| `/simulation`            | Incident Simulation   | Scenario-based incident simulation testing                     |
| `/dark-web`              | Dark Web Monitor      | Dark web exposure and threat intelligence checks               |
| `/reports`               | Report Center         | PDF export and court-ready documentation                       |
| `/admin`                 | Administration        | User management, role assignments (ADMIN only)                 |

---

## UI Components

### Core Layout
- **`Sidebar.tsx`** — Collapsible sidebar with role-based navigation groups, user info, and logout
- **`DashboardLayout.tsx`** — Dashboard layout wrapper
- **`AnimatedBackground.tsx`** — Animated dark background with subtle particle effects
- **`MotionWrapper.tsx`** — Framer Motion fade/slide animation wrapper

### Evidence & Artifacts
- **`EvidenceForm.tsx`** — Multi-field evidence registration form (13KB, most complex form)
- **`TransferForm.tsx`** — PIN-verified custody transfer form
- **`EvidenceTimeline.tsx`** — Visual timeline for evidence custody events
- **`EvidenceMap.tsx`** — Leaflet interactive map for geolocation visualization
- **`DigitalViewer.tsx`** — Multi-format digital evidence file viewer
- **`VoiceRecorder.tsx`** — Audio voice note recorder for evidence
- **`QRCodeGenerator.tsx`** — QR code for physical-digital evidence linking
- **`CertificateButton.tsx`** — Certificate of integrity generation

### Blockchain & Integrity
- **`BlockchainSync.tsx`** — Real-time blockchain ledger sync monitoring
- **`BlockchainExplainer.tsx`** — Educational blockchain concept visualization
- **`BlockchainStatus.tsx`** — Chain integrity status indicator
- **`IntegrityPulse.tsx`** — Live integrity heartbeat monitor
- **`TrustScoreCard.tsx`** — Evidence trust score display (8.5KB)
- **`TamperLabConsole.tsx`** — Interactive tamper detection lab
- **`TamperReplay.tsx`** — Tamper event replay viewer
- **`TamperButton.tsx`** — Tamper action trigger

### Investigation & Analysis
- **`CorrelationPanel.tsx`** — AI-powered cross-artifact correlation analysis
- **`RelationshipGraph.tsx`** — Force-directed network graph
- **`IncidentTimeline.tsx`** — Full incident event timeline
- **`AIDetectiveWidget.tsx`** — AI analysis assistant widget
- **`SimulationPanel.tsx`** — Incident simulation controls

### Monitoring & Alerts
- **`AlertsPanel.tsx`** — Alert list with severity-based filtering
- **`AlertSidebar.tsx`** — Slide-out real-time alert notifications

### Analytics & Charts
- **`ReadinessTrendGraph.tsx`** — Readiness trend over time (Recharts)
- **`analytics/IntakeChart.tsx`** — Evidence intake trends
- **`analytics/StatusChart.tsx`** — Evidence status breakdown pie chart
- **`analytics/LiveTerminal.tsx`** — Simulated SOC live terminal feed

### Reporting & Admin
- **`ExportReports.tsx`** — PDF/report export interface
- **`PDFExportButton.tsx`** — PDF export trigger button
- **`UserManagement.tsx`** — Admin user CRUD panel (13KB)

### Shared UI
- **`Card.tsx`** — Reusable glassmorphism card
- **`StatusBadge.tsx`** — Color-coded status badge (IN_CUSTODY, TRANSFERRED, etc.)
- **`SectionHeader.tsx`** — Styled section header
- **`MetricBox.tsx`** — Numeric metric display box
- **`DashboardMetrics.tsx`** — Quick stats grid for the dashboard
- **`DashboardModules.tsx`** — Module navigation cards for the dashboard

---

## Database Schema

Five core models defined in `prisma/schema.prisma`:

### `User`
| Field          | Type     | Description                                     |
| -------------- | -------- | ----------------------------------------------- |
| `id`           | String   | CUID primary key                                |
| `name`         | String   | Display name                                    |
| `email`        | String   | Unique email address                            |
| `role`         | String   | ADMIN, SOC, RESPONDER, or AUDITOR               |
| `pin`          | String   | Authentication PIN (default: "1234")            |
| `passwordHash` | String   | Password hash (reserved for future auth)        |

### `Evidence`
| Field              | Type     | Description                                  |
| ------------------ | -------- | -------------------------------------------- |
| `id`               | String   | CUID primary key                             |
| `caseNumber`       | String   | Associated case identifier                   |
| `title`            | String   | Evidence title                               |
| `description`      | String?  | Optional description                         |
| `fileHash`         | String?  | SHA-256 hash of the digital file             |
| `filePath`         | String?  | Local path to stored file                    |
| `fileType`         | String?  | MIME type                                    |
| `fileSize`         | Int?     | Size in bytes                                |
| `originalName`     | String?  | Original filename                            |
| `audioData`        | String?  | Base64 encoded voice note                    |
| `status`           | String   | IN_CUSTODY, TRANSFERRED, DESTROYED, DISPOSED |
| `locationLat/Lng`  | Float?   | Geolocation coordinates of collection        |
| `currentCustodianId` | String | FK to current custodian user                 |

### `ArtifactActivityLog`
| Field          | Type     | Description                                        |
| -------------- | -------- | -------------------------------------------------- |
| `id`           | String   | CUID primary key                                   |
| `evidenceId`   | String   | FK to evidence                                     |
| `fromUserId`   | String?  | FK to transferring user                            |
| `toUserId`     | String   | FK to receiving user                               |
| `timestamp`    | DateTime | When the transfer occurred                         |
| `details`      | String?  | Transfer notes/reason                              |
| `locationLat/Lng` | Float? | Geolocation of transfer                           |
| `hash`         | String   | SHA-256 hash of this log entry (unique)            |
| `previousHash` | String   | Hash of the previous entry (forms the chain)       |
| `signature`    | String?  | Digital signature of the from-user                 |

### `Alert`
| Field       | Type     | Description                                                |
| ----------- | -------- | ---------------------------------------------------------- |
| `id`        | String   | CUID primary key                                           |
| `artifactId`| String?  | Optional FK to related evidence                            |
| `alertType` | String   | FAILED_LOGIN, ADMIN_LOGIN, ARTIFACT_MODIFICATION, RULE_TRIGGER |
| `severity`  | String   | LOW, MEDIUM, HIGH, CRITICAL                                |
| `message`   | String   | Alert description                                          |
| `dismissed` | Boolean  | Whether alert has been acknowledged                        |

### `ReadinessAssessment`
| Field               | Type     | Description                       |
| ------------------- | -------- | --------------------------------- |
| `id`                | String   | CUID primary key                  |
| `finalReadinessScore` | Float  | Percentage readiness score        |
| `riskLevel`         | String   | LOW, MEDIUM, HIGH, CRITICAL       |
| `assessedAt`        | DateTime | Assessment timestamp              |

---

## Security & Access Control

### Authentication Flow
1. User selects their **role** on the login page (Admin, SOC Analyst, Responder, Auditor)
2. User enters their **PIN** (default: `1234`)
3. Server validates PIN against the user database
4. On success, a `des_session` cookie is set containing `{ userId, role, name }`
5. Next.js middleware intercepts all routes to enforce authentication

### RBAC Permission Matrix

| Feature                     | ADMIN | SOC | RESPONDER | AUDITOR |
| --------------------------- | :---: | :-: | :-------: | :-----: |
| Create Users                |  ✅   |  ❌  |    ❌     |   ❌    |
| Register Artifacts          |  ✅   |  ✅  |    ❌     |   ❌    |
| View Artifacts              |  ✅   |  ✅  |    ✅     |   ✅    |
| Modify Artifacts            |  ✅   |  ❌  |    ❌     |   ❌    |
| Run Simulations             |  ✅   |  ✅  |    ❌     |   ❌    |
| View Timeline               |  ✅   |  ✅  |    ✅     |   ❌    |
| Analyze Timeline            |  ❌   |  ✅  |    ❌     |   ❌    |
| View Alerts                 |  ✅   |  ✅  |    ❌     |   ❌    |
| Manage Alerts               |  ✅   |  ❌  |    ❌     |   ❌    |
| View Readiness              |  ✅   |  ✅  |    ❌     |   ✅    |
| Manage Readiness            |  ✅   |  ❌  |    ❌     |   ❌    |
| View Correlation            |  ✅   |  ✅  |    ✅     |   ❌    |
| Manage Correlation          |  ✅   |  ✅  |    ❌     |   ❌    |
| View Correlation Summary    |  ❌   |  ❌  |    ❌     |   ✅    |
| Export Reports              |  ✅   |  ❌  |    ✅     |   ❌    |
| Download Reports            |  ❌   |  ❌  |    ❌     |   ✅    |
| View Simulation             |  ❌   |  ❌  |    ✅     |   ✅    |
| View Audit Logs             |  ✅   |  ❌  |    ❌     |   ✅    |
| View Readiness Score        |  ✅   |  ✅  |    ✅     |   ✅    |

### Middleware Enforcement

The `src/middleware.ts` file provides two layers of protection:
1. **Route Guard**: Unauthenticated users are redirected to `/login`
2. **API RBAC**: API routes check the session role against a route permission map, returning HTTP 403 for unauthorized access

---

## Blockchain Integrity Ledger

The system implements a **blockchain-inspired immutable audit trail** for all evidence custody transfers:

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   Block #1  │───▶│   Block #2  │───▶│   Block #3  │
│             │    │             │    │             │
│ hash: abc.. │    │ hash: def.. │    │ hash: ghi.. │
│ prev: 000.. │    │ prev: abc.. │    │ prev: def.. │
│ from: UserA │    │ from: UserB │    │ from: UserC │
│ to:   UserB │    │ to:   UserC │    │ to:   UserA │
│ sig:  xxxxx │    │ sig:  yyyyy │    │ sig:  zzzzz │
└─────────────┘    └─────────────┘    └─────────────┘
```

**How it works:**
1. When a custody transfer occurs, a new `ArtifactActivityLog` entry is created
2. The entry's `hash` is computed from all its fields + the `previousHash`
3. The `previousHash` links to the last entry for that evidence, forming a chain
4. Chain integrity can be verified at any time by re-computing hashes
5. Any tampering breaks the hash chain, immediately detectable

**Key Files:**
- `src/lib/ledger/Blockchain.ts` — Chain management & validation
- `src/lib/ledger/ImmutableLog.ts` — Immutable log entry creation
- `src/lib/hash.ts` — SHA-256 hashing functions
- `src/lib/crypto/CryptoEngine.ts` — Cryptographic operations

---

## AI & Forensic Analysis

| File                               | Purpose                                               |
| ---------------------------------- | ----------------------------------------------------- |
| `src/lib/ai/Analyzer.ts`          | AI-powered evidence analysis and pattern detection    |
| `src/lib/forensics/TrustScoreCalculator.ts` | Trust score algorithm for evidence reliability |
| `src/lib/crypto/CryptoEngine.ts`  | Cryptographic hash computation and verification       |

The **Trust Score** evaluates evidence reliability based on:
- Chain of custody completeness
- Hash verification status
- Number of transfers
- Time gaps between events
- Digital signature presence

---

## Getting Started

### Prerequisites
- **Node.js** 18+ installed
- **npm** package manager
- **Git** (for cloning)

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/YOUR_USERNAME/CIAIFRS.git
cd CIAIFRS

# 2. Create environment file
cp .env.example .env

# 3. Install dependencies
npm install

# 4. Generate Prisma client
npx prisma generate

# 5. Run database migrations (creates SQLite file)
npx prisma migrate dev

# 6. Seed the database with default users
npx prisma db seed

# 7. Start the development server
npm run dev
```

The application will be available at **http://localhost:3000**

---

## Default Credentials

| Role               | PIN    | Access Level                            |
| ---------------    | ------ | --------------------------------------- |
| System Administrator | 1234 | Full access to all modules              |
| SOC Analyst        | 1234   | Monitoring, alerts, simulations         |
| Incident Responder | 1234   | View artifacts, timelines, reports      |
| Auditor            | 1234   | Read-only audit and compliance review   |

> **Note:** All roles use PIN `1234` by default. Change these in the database for production use.

---

## Available Scripts

| Command            | Description                            |
| ------------------ | -------------------------------------- |
| `npm run dev`      | Start Next.js development server       |
| `npm run build`    | Create production build                |
| `npm run start`    | Start production server                |
| `npm run lint`     | Run ESLint                             |
| `npx prisma studio`| Open Prisma database GUI browser       |
| `npx prisma migrate dev` | Run pending database migrations  |
| `npx prisma db seed`    | Seed database with default data   |
| `npx prisma generate`   | Regenerate Prisma client          |

---

## Important Notes

- **Database**: The project uses SQLite (`prisma/dev.db`) for simplicity. The database file is auto-created during migration.
- **Server Actions**: All data mutations use Next.js Server Actions (not API routes), making the code simpler and type-safe.
- **No External Auth Provider**: Authentication is handled internally via PIN + cookie sessions. No OAuth or external providers required.
- **Immutable Audit Trail**: The blockchain-style ledger ensures that evidence custody history cannot be retroactively modified.
- **Court-Ready**: PDF exports are formatted for legal proceedings with proper metadata, timestamps, and integrity proofs.
- **Authentication**: This project uses simplified cookie-based auth for demonstration. In production, use httpOnly, secure, and SameSite cookie flags with encrypted JWTs.

---

## License

This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for details.

---

## Acknowledgments

- Built as a Final Year B.Tech Project
- Inspired by real-world digital forensics workflows and NIST incident response guidelines
- UI design influenced by modern SOC dashboard aesthetics

---

*Built with Next.js 16, TypeScript, Prisma, and a commitment to digital forensic integrity.*
