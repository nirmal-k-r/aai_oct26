# Brainstorming on Project: MoRecu
---------------------------
 - Project name: MoRecu
 - Project type: Progressive Web app
 - Date: 17/11/2026
 - Author/Developer: Nirmal Rampersand

# Description
The application will is an intelligent receipt management and expense-tracking application designed to automate the entire process of recording, organising and analysing financial transactions.

The application allows users to upload receipts as images, PDFs, or scanned documents. Using Optical Character Recognition (OCR) and AI-powered data extraction, the system automatically identifies relevant transaction details, structures the extracted information, and securely stores it in an internal database.

Beyond receipt digitisation, SmartReceipt provides a comprehensive financial analytics dashboard, enabling users to monitor expenditure, identify spending patterns, generate reports and gain actionable financial insights across different reporting periods.

# Tech Stack
 - Language: JS
 - Framework: Next
 - Database: Sqlite (local) with ORM support for mongodb (later)
 - UI Framework: Tailwind CSS
 - Deployment: Local, Will be deployed on Render later


# Objectives
 -  You are tasked with developing an SRS (software requirement specification) document
 -  The SRS will be used to draft an implementation to create the application.
 -  Follow the steps below to develop the SRS:
    1. Understand the project description and tech stack
    2. Identify the core features of the application
    3. Identify the non-core features of the application
    4. Identify the constraints of the application
    5. Identify the context of the application
    6. Identify the acceptance criteria of the application
    7. Identify the todo list for the application
    8. Based on everything above and mentionned in this document, write the SRS.md file

# Functionality
 - Automated Receipt Processing
    - Upload receipts through images, PDFs, or mobile camera captures.
    - Extract transaction details using OCR and AI.
    - Automatically identify merchant names, transaction dates, purchased items, quantities, prices, taxes, discounts, and totals.
    - Support multiple receipt formats, currencies, and layouts.
    - Detect duplicate receipts and prevent duplicate entries.
    - Allow users to review and correct extracted information.

 - Intelligent Expense Management
    - Automatically categorise expenses (groceries, transport, utilities, office supplies, subscriptions, etc.).
    - Support custom expense categories and tags.
    - Organise transactions by merchant, date, category, and payment method.
    - Maintain a searchable transaction history.
    - Store original receipt files alongside structured transaction records.
    - Support manual transaction entry and editing.

 - Financial Analytics & Reporting
    - Provide interactive dashboards and financial summaries covering:
        - Monthly: Spending summaries, expense distributions, and month-over-month comparisons.
        - Quarterly: Quarterly expenditure trends, category comparisons, and financial performance.
        - Half-yearly: Six-month spending patterns and budget evaluations.
        - Yearly: Annual expenditure analysis, historical comparisons, and spending trends.
        - Custom periods: User-defined reporting intervals.
    - Visualise financial information through charts, graphs, tables, and key performance indicators (KPIs).

 - AI-Powered Financial Insights
    - Identify recurring purchases and subscriptions.
    - Highlight unusual expenditure and spending anomalies.
    - Detect changes in purchasing behaviour.
    - Compare expenses across different periods.
    - Identify merchants and categories contributing most to total expenditure.
    - Generate automated financial summaries and recommendations.
    - Enable natural-language queries such as "How much did I spend on groceries over the last six months?"

 - Database & Document Management
    - Maintain a centralised, structured database of receipts, merchants, transactions, and expense categories.
    - Search and filter receipts using multiple criteria.
    - Retrieve original documents instantly.
    - Maintain data integrity through validation and duplicate detection.
    - Track changes to transaction records.
    - Support secure data storage, backups, and recovery.

 - Reporting & Export
    - Generate downloadable financial reports in PDF, Excel, and CSV formats.
    - Export transaction histories for accounting purposes.
    - Produce expense summaries grouped by merchant, category, or reporting period.
    - Support tax-related reporting based on extracted and verified transaction data.

 - Additional Enhancements
    - Budget allocation and spending-limit notifications.
    - Receipt uploads via email forwarding.
    - Bulk uploading and batch processing.
    - Multi-user accounts and access controls.
    - Personal and business expense separation.
    - Multi-currency support.
    - Scheduled financial summaries and notifications.
    - Receipt image quality checks and extraction-confidence indicators.


# Constraints
 - The app must be a PWA (Progressive Web App)
 - The app must have the ability of working without any external API
 - The app and AI models should run on apple silicon hardware (macos)
 - The app should be snappy and fast (should be optimised for speed)
 - The app should look very modern and should not look AI-generated


# Context
 - Will run locally on M4 macbook pro and m4 mac mini server
 - App should have both light and dark modes


# Acceptance criteria
- [ ] Users can install MoRecu as a Progressive Web App (PWA) on mobile (iOS/Android) and desktop (macOS/Chrome/Safari).
- [ ] PWA supports direct mobile camera capture and file selection (JPEG, PNG, WebP, PDF).
- [ ] System performs OCR and extracts merchant, date, total, line items, taxes, and currency 100% locally on Apple Silicon (M4) without requiring external cloud APIs.
- [ ] Duplicate receipts are identified using perceptual hashing and transactional deduplication (merchant + date + amount).
- [ ] Interactive dashboard displays financial metrics across Monthly, Quarterly, Half-Yearly, Yearly, and Custom intervals with sub-second responsiveness.
- [ ] Natural language query engine provides instant answers to spending queries using local LLM integration (e.g. Ollama).
- [ ] Data layer operates on local SQLite with zero external dependencies, architected with an ORM abstraction layer to facilitate seamless MongoDB migration.
- [ ] Dark mode and Light mode switch smoothly with bespoke, premium typography and design (non-generic UI).
- [ ] Data export available in CSV, Excel, and structured PDF formats.

# Todo list
- [ ] Phase 1: Foundation & PWA Scaffold (Next.js, Tailwind CSS, PWA Manifest, Service Worker, SQLite ORM setup).
- [ ] Phase 2: Local OCR & Document Ingestion Pipeline (Camera capture, PDF/Image parser, Apple Vision / Tesseract / Ollama integration, deduplication).
- [ ] Phase 3: Expense Management & Verification UI (Transaction review drawer, line-item editor, categorizer, manual entry).
- [ ] Phase 4: Analytics Engine & Dashboard (KPI cards, interactive charts, period selector, multi-currency support).
- [ ] Phase 5: Local AI Insights & Natural Language Assistant (Spending anomalies, recurring subscription detection, local conversational query interface).
- [ ] Phase 6: Document Vault, Export & Reporting (CSV/XLSX/PDF generation, full-text search, backup/restore).
- [ ] Phase 7: Polish, Offline Sync, Render Deployment Configuration & Performance Optimization.


