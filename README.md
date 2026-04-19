Credit Lifecycle Management System
A full-stack application for managing a bank's credit operations — from client onboarding and eligibility scoring to loan disbursement, repayment tracking, and risk classification.
Built with MySQL (relational database) and PHP (web interface).

Overview
This system automates the core data workflows of a retail lending operation. It was designed to reflect real-world banking logic, including regulatory constraints (BNR debt-to-income rules), risk classification, and multi-client credit exposure.

Key Features
Client Onboarding (KYC)

Dual data model supporting both individuals (CNP, employer, salary) and legal entities (CUI, trade register number, revenue, profit)
Document upload and identity verification fields (photo, signature)
Auto-generated demo data for testing (ID series, historical income)

Credit Eligibility Scoring Engine

Queries historical incident data to check blacklist status
Calculates debt-to-income ratio against BNR regulatory threshold (40% cap)
Takes into account external credit exposure from other financial institutions
Blocks ineligible applicants before loan creation

Loan Amortization Schedule Generator

Computes monthly installments using the annuity method
Randomly distributes due dates across days 1–28 of each month
Generates a complete repayment schedule stored in the scadentar table

Payment & Arrears Management

FIFO enforcement: oldest overdue installment must be paid before current
Dynamic penalty calculation: 0.1% per day of overdue amount
Real-time tracking of days in arrears per installment

Risk Classification (Blacklist)

Automatic flagging of clients with arrears exceeding 60 days
Enforces a 4-year cooling-off period from the last incident
Blocks re-application until the restriction period expires

Web Interface (PHP)

Financial dashboard with portfolio overview
Global search across clients, loans, and repayment schedules
Full CRUD operations for all entities


Database Schema
clients (clienti)
    └── credits (credite)           [One-to-Many]
            └── schedule (scadentar) [One-to-Many]

external_credits (credite_externe)  [linked to clienti]
4 normalized tables, designed to 3NF. Referential integrity enforced via foreign keys.

Tech Stack
LayerTechnologyDatabaseMySQL / MariaDBBackendPHP 8.xInterfacephpMyAdmin + custom PHP web UISchema DesignNormalized relational model (3NF)

Business Logic Highlights

Eligibility check is fully automated — no manual override required
Penalty and arrears logic runs on every payment event
Blacklist classification is triggered by database state, not manual input
External credit data is factored into debt-to-income calculations, mirroring Credit Bureau (Biroul de Credit) logic


Author
Iulian Popa
Computer Science student, Politehnica University Timișoara
LinkedIn
