# Implementation Plan: MoRecu
**Document:** `plan.md`  
**Target Region:** Mauritius (MUR `Rs`, 15% VAT, MRA compliance, EN/FR receipt formats, DD/MM/YYYY)  
**Architecture:** Next.js (App Router), Tailwind CSS, SQLite (Prisma ORM with MongoDB readiness), Local OCR + Ollama AI, PWA  

---

## Mauritius Localisation Baseline
- **Primary Currency:** Mauritian Rupee (`MUR` / `Rs`), secondary: `USD`, `EUR`, `GBP`.
- **Tax Configuration:** Standard 15% VAT rate, VAT invoice support (VAT No., BRN - Business Registration Number).
- **Language / Parsing:** Bilingual receipt support (English & French terms: *Total TTC, Sous-total, TVA, Espèces, Carte, Remise*).
- **Date Conventions:** `DD/MM/YYYY` primary standard.
- **Top Merchant Auto-Recognition:** Winners, Super U, Intermart, my.t, CEB, CWA, Shell, TotalEnergies, Engen, etc.

---

## Phase 1: Foundation, PWA Shell & Data Architecture
**Goal:** Establish an offline-ready, responsive application shell and local database layer.

1. **Project Scaffolding & Design Tokens:**
   - Initialize Next.js (App Router, TypeScript) with Tailwind CSS.
   - Configure Mauritian locale tokens, dark/light theme palette, and bespoke non-generic UI primitives.
2. **PWA & Offline Manifest:**
   - Configure PWA manifest (`name: MoRecu`, `theme_color`, icons, standalone mode).
   - Register Service Worker caching shell assets with offline capture queue in IndexedDB.
3. **Database & ORM Tier:**
   - Configure Prisma with SQLite (`file:./data/morecu.db`).
   - Define schema: `Receipt`, `LineItem`, `Merchant`, `Category`, `Tag`, `AuditLog`.
   - Seed default Mauritian categories (Alimentation/Groceries, Carburant/Transport, CEB/CWA/Utilities, my.t/Telecom, Santé/Healthcare, Loisirs).
   - Abstract database operations using a Repository layer to enable future MongoDB switching.
4. **Deliverables:** Working local app shell, PWA install prompt, seeded SQLite database, responsive navigation layout.

---

## Phase 2: Ingestion Engine & Local Bilingual OCR Pipeline
**Goal:** Process uploaded images, PDFs, and camera captures locally on Apple Silicon without cloud APIs.

1. **PWA Capture & Dropzone:**
   - Multi-format file uploader (JPEG, PNG, WebP, PDF) with drag-and-drop.
   - PWA camera integration (`capture="environment"` with mobile alignment frame).
2. **Local Multi-Tier Extraction Engine:**
   - *Tier 1 (Fast OCR):* Local `tesseract.js` (WASM) configured with English (`eng`) and French (`fra`) language packs.
   - *Tier 2 (Local LLM/VLM via Ollama):* Local API (`http://localhost:11434`) using `llama3.2-vision` / `mistral` to structure raw text into typed JSON.
   - *Tier 3 (Heuristic Parser):* Rule-based fallback extracting Mauritian date (`DD/MM/YYYY`), `Rs`/`MUR`, 15% VAT, and BRN/VAT numbers.
3. **Deduplication Engine:**
   - Perceptual image hashing (`pHash`) and composite key matching `(merchant, date, total_amount)`.
4. **Deliverables:** End-to-end receipt upload running 100% offline with structured JSON output and duplicate alerts.

---

## Phase 3: Verification Drawer & Expense Management
**Goal:** Provide an intuitive, rapid-review interface for verifying and editing transactions.

1. **Interactive Review Drawer:**
   - Side-by-side receipt image viewer (zoom, pan, rotate) and auto-populated transaction form.
   - Field-level confidence indicators highlighting unverified or low-confidence values.
2. **Line-Item & Tax Editor:**
   - Editable line items (description, quantity, unit price, item category).
   - Automatic 15% VAT computation and toggle for zero-rated / exempt items.
3. **Categorisation & Tax Tagging:**
   - Auto-categorisation based on learned merchant history.
   - Personal vs. Business expense toggle with MRA tax-deductible flag (`#MRA-Deductible`, `#BusinessExpense`).
4. **Manual Entry & History View:**
   - Fast manual transaction entry for paperless and cash transactions.
   - Searchable, filterable transaction table with multi-select bulk actions.
5. **Deliverables:** Complete verification workflow, transaction editing, receipt storage, and category assignment.

---

## Phase 4: Financial Analytics, KPIs & Local AI Insights
**Goal:** Transform receipt data into actionable financial intelligence and natural language queries.

1. **Analytics Engine:**
   - Aggregations across predefined periods: Monthly, Quarterly, Half-Yearly, Yearly, and Custom Date Range.
   - Key KPIs: Total Spent (MUR), Daily Average, Fixed vs. Discretionary ratio, VAT paid.
2. **Interactive Visualisations:**
   - Expense distribution (Donut / Treemap).
   - Monthly trend line & budget variance comparison.
   - Merchant leaderboard (top spending destinations).
3. **Local AI Insights (Ollama):**
   - Recurring bill detection (my.t subscriptions, insurance, recurring utilities).
   - Anomaly detection (unusual spikes compared to 3-month running median).
4. **Local Natural Language Querying:**
   - Chat input translating questions into local queries (e.g., *"How much did I spend at Winners in the last 3 months?"*).
5. **Deliverables:** High-speed financial dashboard and local conversational query interface.

---

## Phase 5: Vault, Reporting, Export & Deployment Readiness
**Goal:** Ensure data portability, compliance reporting, and production readiness.

1. **Document Vault & Full-Text Search:**
   - Secure local storage of original receipts with instant preview and download.
   - Instant search across merchant names, line items, notes, and tags.
2. **Accounting Export & Tax Reports:**
   - CSV & formatted Excel (`.xlsx`) export compliant with standard accounting packages.
   - Printable PDF summary report grouped by category with receipt thumbnails for MRA tax filing.
3. **Backup & Portability:**
   - One-click JSON database + receipt archive backup and restore utility.
4. **Render Cloud & MongoDB Readiness:**
   - Environment configuration abstraction (`DATABASE_URL`, storage provider switch).
   - Dockerfile and build scripts optimized for local M4 execution and Render cloud deployment.
5. **Deliverables:** Export engine, full-text document vault, backup/restore, and deployment documentation.
