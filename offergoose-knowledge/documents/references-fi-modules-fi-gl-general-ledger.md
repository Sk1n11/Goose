# references-fi-modules-fi-gl-general-ledger.md

Topic: My GitHub knowledge

# references/fi-modules/fi-gl-general-ledger.md

Topic: Free SAP FICO sources — auto-fetched

// Repository: https://github.com/ninadtrivedi-finance/sap-s4hana-fico-implementation
// File: references/fi-modules/fi-gl-general-ledger.md

# FI-GL — General Ledger Configuration Guide

## Overview
General Ledger (FI-GL) is the foundation of SAP FICO. All financial transactions ultimately post to GL accounts. S/4HANA uses the **Universal Journal (ACDOCA)** which replaces 10+ ECC tables (BSEG, BSIS, BSAK, GLT0, FAGLFLEXT, COEP, etc.).

**Key S/4HANA Changes:**
- Single source of truth: ACDOCA
- Real-time financial reporting
- FI-CO reconciliation eliminated
- Document splitting mandatory
- Parallel ledgers built-in
- Embedded analytics via CDS views

---

## Configuration Roadmap (80 Steps Total)

### Phase 1: Enterprise Structure (Steps 1-7)
1. Define Company (OX15)
2. Define Company Code (OX02)
3. Assign Company ↔ Company Code (OX16)
4. Define Business Area (OX03)
5. Define Functional Area (OX10)
6. Define Fiscal Year Variant (OB29)
7. Define Posting Period Variant (OBBO)

### Phase 2: Chart of Accounts (Steps 8-12)
8. Define Chart of Accounts (OB13)
9. Assign CoA → Company Code (OB62)
10. Define Account Groups (OBD4)
11. Create GL Account Master (FS00)
12.

e Posting Period Variant (OBBO)

### Phase 2: Chart of Accounts (Steps 8-12)
8. Define Chart of Accounts (OB13)
9. Assign CoA → Company Code (OB62)
10. Define Account Groups (OBD4)
11. Create GL Account Master (FS00)
12. Define Retained Earnings Account (OB53)

### Phase 3: Document Control (Steps 13-17)
13. Define Document Types (OBA7)

Phase 2: Chart of Accounts (Steps 8-12) — gn CoA → Company Code (OB62)
10. Define Account Groups (OBD4)
11. Create GL Account Master (FS00)
12. Define Retained Earnings Account (OB53)

### Phase 3: Document Control (Steps 13-17)
13. Define Document Types (OBA7)
14. Define Posting Keys (OB41)
15. Define Field Status Variants (OBC4)
16. Define Number Ranges (FBN1)
17. Define Tolerance Groups (OBA4, OBA0)

### Phase 4: S/4HANA Universal Journal (Steps 18-20)
18. Configure Document Splitting (FAGL_SPLIT_CUST)
19. Define Parallel Ledgers (FINSC_LEDGER)
20. Assign Accounting Principles (FAGL_ACTIVATE_SAP_ACCOUNTING)

### Phase 5: Period Control (Steps 21-22)
21. Define Posting Period Variants (OBBO)
22. Open/Close Posting Periods (OB52)

---

## Detailed Configuration Steps

### 1. Define Company

**SPRO Path:** Enterprise Structure → Definition → Financial Accounting → Define Company

**Transaction:** `OX15` 
**IMG Activity:** `EC01`

g Periods (OB52)

---

## Detailed Configuration Steps

### 1. Define Company

**SPRO Path:** Enterprise Structure → Definition → Financial Accounting → Define Company

**Transaction:** `OX15` 
**IMG Activity:** `EC01` 
**Configuration Table:** `T880`

**Purpose:** Highest organizational unit for legal consolidation. A company can have multiple company codes.

**Prerequisites:** None - this is the starting point.

**Fields:**
- **Company (BUKRS)** [Required]: 4-char alphanumeric (e.g., `C001`)
- **Company Name** [Required]: Legal entity name (e.g., "Acme Corporation Ltd.")

1. Define Company — .

**Prerequisites:** None - this is the starting point.

**Fields:**
- **Company (BUKRS)** [Required]: 4-char alphanumeric (e.g., `C001`)
- **Company Name** [Required]: Legal entity name (e.g., "Acme Corporation Ltd.")
- **Street/City/Country** [Optional]: Address information

**Step-by-Step:**
1. Execute transaction `OX15`
2. Click "New Entries"
3. Enter Company: `C001`
4. Enter Name: `Acme Corporation Ltd.`
5. Enter address details
6. Save (Ctrl+S)

**Example:**
```
Company: C001
Name: Acme Corporation Ltd.
City: New York
Country: US
```

**Testing:**
- Display company (OX15)
- Verify appears in assignment screen (OX16)

**Common Mistakes:**

tails
6. Save (Ctrl+S)

**Example:**
```
Company: C001
Name: Acme Corporation Ltd.
City: New York
Country: US
```

**Testing:**
- Display company (OX15)
- Verify appears in assignment screen (OX16)

**Common Mistakes:**
❌ Using same code for Company and Company Code 
❌ Creating company after company codes 
✅ Create company first, plan structure

---

### 2. Define Company Code

**SPRO Path:** Enterprise Structure → Definition → Financial Accounting → Edit, Copy, Delete, Check Company Code

**Transaction:** `OX02` 
**IMG Activity:** `EC02` 
**Table:** `T001`

**Purpose:** Central organizational unit in FI. Every transaction posts to a company code. Represents independent accounting entity with own balance sheet and P&L.

**Prerequisites:** Company exists (OX15)

**Fields:**
- **Company Code (BUKRS)** [Required]: 4-char (e.g., `1000`)

2. Define Company Code — ction posts to a company code. Represents independent accounting entity with own balance sheet and P&L.

**Prerequisites:** Company exists (OX15)

**Fields:**
- **Company Code (BUKRS)** [Required]: 4-char (e.g., `1000`)
- **Company Code Name** [Required]: Descriptive name
- **City** [Required]: Location
- **Country** [Required]: 2-char ISO code (US, IN, DE, GB, CN)
 - **CRITICAL:** Cannot change after transactions exist

(e.g., `1000`)
- **Company Code Name** [Required]: Descriptive name
- **City** [Required]: Location
- **Country** [Required]: 2-char ISO code (US, IN, DE, GB, CN)
 - **CRITICAL:** Cannot change after transactions exist
 - Drives country-specific functionality
- **Currency** [Required]: Local currency (USD, INR, EUR, GBP, CNY)
 - **CRITICAL:** Cannot change after transactions exist
- **Language** [Required]: Default language (EN, DE, FR, JA, ZH)

**Step-by-Step:**
1. Transaction `OX02`
2. Click "New Entries"
3. Enter Company Code: `1000`
4. Enter all required fields
5. Save

**Example:**
```
Company Code: 1000
Name: Acme US Operations
City: New York
Country: US
Currency: USD
Language: EN
```

**Testing:**
- Display company code (OX02)
- Verify all fields populated
- Post test transaction (FB50) - verify CoCode 1000 available

**Common Mistakes:**
❌ Wrong currency - all transactions post in wrong currency 
❌ Wrong country - tax config incorrect 
❌ Forgetting to assign Chart of Accounts (OB62) 
✅ Triple-check Country and Currency

**Dependencies:**

mon Mistakes:**
❌ Wrong currency - all transactions post in wrong currency 
❌ Wrong country - tax config incorrect 
❌ Forgetting to assign Chart of Accounts (OB62) 
✅ Triple-check Country and Currency

**Dependencies:**

mon Mistakes:**
❌ Wrong currency - all transactions post in wrong currency 
❌ Wrong country - tax config incorrect 
❌ Forgetting to assign Chart of Accounts (OB62) 
✅ Triple-check Country and Currency

**Dependencies:**
- Assign to Company (OX16) - next step
- Assign Chart of Accounts (OB62)
- Assign Fiscal Year Variant (OB29 or in CoCode data)

---

### 8. Define Chart of Accounts

**SPRO Path:** Financial Accounting → General Ledger Accounting → Master Records → G/L Accounts → Preparations → Edit Chart of Accounts List

**Transaction:** `OB13` 
**Table:** `SKA1`

**Purpose:** Chart of Accounts (CoA) is the list of all GL accounts. Defines GL structure.

**Fields:**
- **Chart of Accounts (KTOPL)** [Required]: 4-char (e.g., `INT`, `US01`, `IN01`)
- **Description** [Required]: Name
- **Maintenance Language** [Required]: EN, DE, FR
- **Length of GL Account Number** [Required]: Max 10 digits
 - **CRITICAL:** Cannot change once accounts exist
- **Block Indicator** [Optional]: Usually unchecked

**Account Numbering Best Practices:**

**Range-Based Structure:**
```
100000-199999: Assets
 100000-109999: Current Assets (Cash, Bank, AR)
 110000-119999: Inventory
 120000-199999: Fixed Assets
200000-299999: Liabilities
 200000-209999: Current Liabilities (AP, Accruals)

8.

ucture:**
```
100000-199999: Assets
 100000-109999: Current Assets (Cash, Bank, AR)
 110000-119999: Inventory
 120000-199999: Fixed Assets
200000-299999: Liabilities
 200000-209999: Current Liabilities (AP, Accruals)

8. Define Chart of Accounts — Structure:**
```
100000-199999: Assets
 100000-109999: Current Assets (Cash, Bank, AR)
 110000-119999: Inventory
 120000-199999: Fixed Assets
200000-299999: Liabilities
 200000-209999: Current Liabilities (AP, Accruals)
 210000-299999: Long-term Liabilities
300000-399999: Equity
400000-499999: Revenue
500000-599999: Cost of Goods Sold
600000-699999: Operating Expenses
```

**Testing:**
- Display CoA (OB13)
- Assign to company code (OB62)
- Create GL account (FS00) - verify CoA appears

---

### 11. Create GL Account Master

**Transaction:** `FS00` (Create/Change/Display) 
**Tables:** `SKA1` (CoA segment), `SKB1` (Company Code segment)

**Purpose:** Define properties and behavior of each GL account.

**Two-Level Structure:**
1. **Chart of Accounts Segment (SKA1)** - Defined once
2. **Company Code Segment (SKB1)** - Company-specific

**Chart of Accounts Segment Fields:**
- **GL Account Number** [Required]: Up to 10 digits
- **Account Group** [Required]: Determines number range, field status
- **Short Text** [Required]: 20 characters

ompany-specific

**Chart of Accounts Segment Fields:**
- **GL Account Number** [Required]: Up to 10 digits
- **Account Group** [Required]: Determines number range, field status
- **Short Text** [Required]: 20 characters
- **Long Text** [Optional]: 50 characters
- **P&L Statement Account Type** [Required if P&L]: Sales Revenue, Cost of Sales, Admin Expense
- **Account Type** [Required]: Balance Sheet or P&L

**Company Code Segment Fields:**

11. Create GL Account Master — Long Text** [Optional]: 50 characters
- **P&L Statement Account Type** [Required if P&L]: Sales Revenue, Cost of Sales, Admin Expense
- **Account Type** [Required]: Balance Sheet or P&L

**Company Code Segment Fields:**
- **Currency** [Required]: Usually same as company code
- **Tax Category** [Required if tax-relevant]: Input Tax, Output Tax, Non-Taxable
- **Reconciliation Account** [Optional]: For subledger (customer/vendor)
- **Line Item Display** [Required]: ☑ for accounts needing line-item reporting
- **Open Item Management** [Optional]: ☑ for clearing accounts (GR/IR, customer, vendor)
- **Post Automatically Only** [Optional]: For automatic postings (tax, exchange rate)

**Example - Cash Account:**
```
CoA Segment:
- GL Account: 100100
- Account Group: BETR (Balance Sheet)
- Short Text: Cash in Hand

)
- **Post Automatically Only** [Optional]: For automatic postings (tax, exchange rate)

**Example - Cash Account:**
```
CoA Segment:
- GL Account: 100100
- Account Group: BETR (Balance Sheet)
- Short Text: Cash in Hand
- Account Type: Balance Sheet - Asset

Company Code Segment:
- Company Code: 1000
- Currency: USD
- Tax Category: Not Tax Relevant
- Line Item Display: ☑
- Open Item Management: ☐
```

**Testing:**
- Display account (FS00)
- Post document (FB50) using account
- Display line items (FBL3N)

**Common Mistakes:**
❌ Line Item Display unchecked - cannot report line items 
❌ Wrong Tax Category - tax posting incorrect 
❌ Open Item Management checked unnecessarily - performance issue

Display line items (FBL3N)

**Common Mistakes:**
❌ Line Item Display unchecked - cannot report line items 
❌ Wrong Tax Category - tax posting incorrect 
❌ Open Item Management checked unnecessarily - performance issue 
✅ Plan account properties before creation

---

### 18. Configure Document Splitting (S/4HANA MANDATORY)

**SPRO Path:** Financial Accounting (New) → General Ledger Accounting (New) → Business Transactions → Document Splitting

**Transaction:** `FAGL_SPLIT_CUST` 
**Table:** Various (T8G**, FAGL_SPLIT*)

(S/4HANA MANDATORY)

**SPRO Path:** Financial Accounting (New) → General Ledger Accounting (New) → Business Transactions → Document Splitting

**Transaction:** `FAGL_SPLIT_CUST` 
**Table:** Various (T8G**, FAGL_SPLIT*)

**Purpose:** Document splitting ensures documents balance at Profit Center, Segment, or other dimensions. Enables real-time P&L by profit center without allocation runs.

**Key Concepts:**
- **Zero Balance:** Document must balance by company code AND by profit center/segment
- **Splitting Characteristics:** Profit Center, Segment, Business Area
- **Splitting Method:** 001 (standard) or custom

**Configuration Steps:**
1. **Activate Document Splitting:**
 - SPRO → Document Splitting → Activate Document Splitting
 - Select Company Code
 - Activate flag

2. **Define Document Splitting Characteristics:**
 - Standard: Profit Center, Segment
 - Optional: Business Area, Functional Area

3. **Classify GL Accounts:**
 - Balance Sheet accounts: Asset, Liability, Equity

18. Configure Document Splitting (S/4HANA MANDATORY) — e flag

2. **Define Document Splitting Characteristics:**
 - Standard: Profit Center, Segment
 - Optional: Business Area, Functional Area

3. **Classify GL Accounts:**
 - Balance Sheet accounts: Asset, Liability, Equity
 - P&L accounts: Expense, Revenue

ting Characteristics:**
 - Standard: Profit Center, Segment
 - Optional: Business Area, Functional Area

3. **Classify GL Accounts:**
 - Balance Sheet accounts: Asset, Liability, Equity
 - P&L accounts: Expense, Revenue
 - Transaction: FAGL_ACCOUNT_CLASSIFICATION

4. **Define Zero Balance Clearing Account:**
 - For incomplete assignments
 - Temporary clearing during posting

5. **Define Splitting Rules:**
 - Standard rules usually sufficient
 - Custom rules for complex scenarios

6. **Test Extensively:**
 - Every transaction type
 - Cross-profit center postings
 - Verify zero balance by profit center

**Example Scenario:**
```
Posting: Salary Expense
Line 1: Debit Salary Expense 100000 (Profit Center PC01)
Line 2: Debit Salary Expense 50000 (Profit Center PC02)
Line 3: Credit Bank 150000 (No PC assigned)

Document Splitting:
System auto-splits Line 3:
- Credit Bank 100000 (PC01)
- Credit Bank 50000 (PC02)

Result: Document balances by CoCode AND by each PC
```

**Testing:**
- Post cross-PC transaction (FB50)
- Display document (FB03)
- Verify splitting occurred
- Run PC balance sheet (S_ALR_87013611)

**Common Issues:**
❌ Accounts not classified - splitting fails 
❌ Clearing account not defined - posting error

ction (FB50)
- Display document (FB03)
- Verify splitting occurred

- Run PC balance sheet (S_ALR_87013611)

**Common Issues:**
❌ Accounts not classified - splitting fails 
❌ Clearing account not defined - posting error

ction (FB50)
- Display document (FB03)
- Verify splitting occurred
- Run PC balance sheet (S_ALR_87013611)

**Common Issues:**
❌ Accounts not classified - splitting fails 
❌ Clearing account not defined - posting error 
❌ Incompatible profit center assignments 
✅ Test EVERY business transaction type

---

### 19. Define Parallel Ledgers (S/4HANA)

**SPRO Path:** Financial Accounting (New) → General Ledger Accounting (New) → Ledgers → Ledger → Define Ledgers for General Ledger Accounting

**Transaction:** `FINSC_LEDGER`

**Purpose:** Parallel ledgers allow multiple accounting principles (IFRS, Local GAAP, Tax) in one system.

**Standard Ledgers:**
- **0L:** Leading Ledger (e.g., IFRS)
- **2L:** Non-Leading Ledger (e.g., Local GAAP)
- **3L:** Non-Leading Ledger (e.g., Tax)

**Configuration:**
1. Define Ledgers
2. Assign Accounting Principles (IFRS, US-GAAP, Local GAAP)
3. Define Ledger Groups
4. Assign Fiscal Year Variants per Ledger
5. Configure Parallel Valuation (if needed)

**Use Cases:**
- IFRS for group reporting
- Local GAAP for statutory reporting
- Tax basis for tax returns
- Management accounting (internal)

---

### 22.

Variants per Ledger
5. Configure Parallel Valuation (if needed)

**Use Cases:**
- IFRS for group reporting
- Local GAAP for statutory reporting
- Tax basis for tax returns
- Management accounting (internal)

---

### 22. Open/Close Posting Periods

**Transaction:** `OB52` 
**Table:** `T001B`

**Purpose:** Controls which periods are open for posting by account type.

19. Define Parallel Ledgers (S/4HANA) — basis for tax returns
- Management accounting (internal)

---

### 22. Open/Close Posting Periods

**Transaction:** `OB52` 
**Table:** `T001B`

**Purpose:** Controls which periods are open for posting by account type.

**Configuration:**
```
Company Code: 1000
From Period: 001 / To Period: 003 (Jan-Mar open)
From Account: + / To Account: + (all accounts)
Account Type: + (all types: A=Asset, D=Customer, K=Vendor, M=Material, S=GL)
```

**Testing:**
- Post in open period → Success
- Post in closed period → Error "Posting period is not open"

---

## Advanced Topics

### Foreign Currency Valuation

**Transaction:** `FAGL_FC_VAL`

Revalue open foreign currency items at period-end:
- Balance sheet accounts (OB09)
- Open item accounts (OB10)

### Universal Journal (ACDOCA) Architecture

**ECC vs S/4HANA:**
| Feature | ECC | S/4HANA |
|---------|-----|---------|

foreign currency items at period-end:
- Balance sheet accounts (OB09)
- Open item accounts (OB10)

### Universal Journal (ACDOCA) Architecture

**ECC vs S/4HANA:**
| Feature | ECC | S/4HANA |
|---------|-----|---------|
| Tables | BSEG, BSIS, BSAK, GLT0, FAGLFLEXT, COEP | **ACDOCA only** |
| FI-CO Recon | Required (KALC) | **Eliminated** |
| Reporting | Multiple tables | Single table (faster) |
| Real-time | No | Yes |

**ACDOCA Key Fields:**
- RBUKRS - Company Code
- GJAHR - Fiscal Year
- BELNR - Document Number
- DOCLN - Line Item
- RACCT - Account Number
- PRCTR - Profit Center
- SEGMENT - Segment
- HSLVT - Amount in Local Currency

Universal Journal (ACDOCA) Architecture — **ACDOCA Key Fields:**
- RBUKRS - Company Code
- GJAHR - Fiscal Year
- BELNR - Document Number
- DOCLN - Line Item
- RACCT - Account Number
- PRCTR - Profit Center
- SEGMENT - Segment
- HSLVT - Amount in Local Currency
- HSLBT - Amount in Group Currency

---

## Quick Reference

### Critical Transactions
| T-Code | Description | When to Use |
|--------|-------------|-------------|
| OX15 | Define Company | First step |
| OX02 | Define Company Code | Second step |
| OB13 | Chart of Accounts | Before GL accounts |
| FS00 | GL Account Master | Create accounts |
| OBA7 | Document Types | Before posting |

15 | Define Company | First step |
| OX02 | Define Company Code | Second step |
| OB13 | Chart of Accounts | Before GL accounts |
| FS00 | GL Account Master | Create accounts |
| OBA7 | Document Types | Before posting |
| OB52 | Open/Close Periods | Period control |
| FAGL_SPLIT_CUST | Document Splitting | S/4HANA mandatory |
| FB50 | Post Journal Entry | Manual posting |
| FB03 | Display Document | Verify postings |
| FBL3N | GL Line Items | Reporting |

### Configuration Tables
| Table | Description | Key Data |
|-------|-------------|----------|
| T880 | Company | Legal entities |
| T001 | Company Code | Accounting units |
| SKA1 | GL Master (CoA) | Account definitions |
| SKB1 | GL Master (CoCode) | Company-specific |
| T003 | Document Types | Doc control |
| ACDOCA | Universal Journal | All postings (S/4HANA) |

---

This concludes FI-GL configuration.

Configuration Tables — ter (CoA) | Account definitions |
| SKB1 | GL Master (CoCode) | Company-specific |
| T003 | Document Types | Doc control |
| ACDOCA | Universal Journal | All postings (S/4HANA) |

---

This concludes FI-GL configuration. See separate files for FI-AP, FI-AR, FI-AA, CO modules.

--- LINKED SOURCE READ FROM: https://github.com/ninadtrivedi-finance/sap-s4hana-fico-implementation ---

ings (S/4HANA) |

---

This concludes FI-GL configuration. See separate files for FI-AP, FI-AR, FI-AA, CO modules.

--- LINKED SOURCE READ FROM: https://github.com/ninadtrivedi-finance/sap-s4hana-fico-implementation ---
GitHub - ninadtrivedi-finance/sap-s4hana-fico-implementation: Comprehensive SAP S/4HANA FICO implementation skill for Claude. Covers all FI & CO modules to L5, integrations, 50+ countries. Production-grade quality. · GitHub

Skip to content

Navigation Menu

Sign in Appearance settings

Platform AI CODE CREATION GitHub Copilot Write better code with AI
GitHub Copilot app Direct agents from issue to merge
MCP Registry Integrate external tools

DEVELOPER WORKFLOWS Actions Automate any workflow
Codespaces Instant dev environments
Issues Plan and track work
Code Review Manage code changes
Code Quality Enforce quality at merge

APPLICATION SECURITY GitHub Advanced Security Find and fix vulnerabilities
Code security Secure your code as you build
Secret protection Stop leaks before they start

EXPLORE Why GitHub
Documentation
Blog
Changelog
Marketplace

View all features

Solutions BY COMPANY SIZE Enterprises
Small and medium teams
Startups
Nonprofits

BY USE CASE App Modernization
DevSecOps
DevOps
CI/CD
View all use cases

BY INDUSTRY Healthcare
Financial services

ce

View all features

Solutions BY COMPANY SIZE Enterprises
Small and medium teams
Startups
Nonprofits

BY USE CASE App Modernization
DevSecOps
DevOps
CI/CD
View all use cases

BY INDUSTRY Healthcare
Financial services
Manufacturing
Government
View all industries

View all solutions

Resources EXPLORE BY TOPIC AI
Software Development
DevOps
Security
View all topics

EXPLORE BY TYPE Customer stories
Events & webinars
Ebooks & reports
Business insights
GitHub Skills

SUPPORT & SERVICES Documentation
Customer support
Community forum
Trust center
Partners

View all resources

Open Source COMMUNITY GitHub Sponsors Fund open source developers

PROGRAMS Security Lab
Maintainer Community
GitHub Stars
Archive Program

REPOSITORIES Topics
Trending
Collections

Enterprise ENTERPRISE SOLUTIONS Enterprise platform AI-powered developer platform

AVAILABLE ADD-ONS GitHub Advanced Security Enterprise-grade security features
Copilot for Business Enterprise-grade AI features
Premium Support Enterprise-grade 24/7 support

Pricing
Search /

Sign in
Sign up Appearance settings

You signed in with another tab or window. Reload to refresh your session.
You signed out in another tab or window. Reload to refresh your session.
You switched accounts on another tab or window.

n up Appearance settings

You signed in with another tab or window. Reload to refresh your session.
You signed out in another tab or window. Reload to refresh your session.
You switched accounts on another tab or window. Reload to refresh your session.

Dismiss alert

{{ message }}

ninadtrivedi-finance
sap-s4hana-fico-implementation

Repository navigation

Code
Issues
Pull requests
Actions
Projects
Security and quality
Insights

More items

[Image description: ninadtrivedi-finance]
sap-s4hana-fico-implementation
Public

Notifications You must be signed in to change notification settings
Fork 2  ( 2 )
Star 4  ( 4 ) You must be signed in to star a repository

About
Comprehensive SAP S/4HANA FICO implementation skill for Claude. Covers all FI & CO modules to L5, integrations, 50+ countries. Production-grade quality.
Resources
Readme
MIT license
Contributing
Contributing
Activity

Stars
4 stars
Watchers
0 watching
Forks
2 forks

Report repository

main

Branches Tags

Go to file

Code Open more actions menu

Latest commit
 

History
2 Commits
2 Commits

Folders and files
Name | Name | Last commit message
| Last commit date
|
evals

| evals

|  
|  

|
references

| references

|  
|  

|
.gitignore

| .gitignore

|  
|  

|
COMPLETE_MODULES_SUMMARY.md

| COMPLETE_MODULES_SUMMARY.md

iles
Name | Name | Last commit message
| Last commit date
|
evals

| evals

|  
|  

|
references

| references

|  
|  

|
.gitignore

| .gitignore

|  
|  

|
COMPLETE_MODULES_SUMMARY.md

| COMPLETE_MODULES_SUMMARY.md

|  
|  

|
CONTRIBUTING.md

| CONTRIBUTING.md

|  
|  

|
DOWNLOAD_GUIDE.md

| DOWNLOAD_GUIDE.md

|  
|  

|
FILE_MANIFEST.md

| FILE_MANIFEST.md

|  
|  

|
FRAMEWORK.md

| FRAMEWORK.md

|  
|  

|
GITHUB_UPLOAD_GUIDE.md

| GITHUB_UPLOAD_GUIDE.md

|  
|  

|
LICENSE

| LICENSE

|  
|  

|
README.md

| README.md

|  
|  

|
SKILL.md

| SKILL.md

|  
|  

|
push-to-github.sh

| push-to-github.sh

|  
|  

|
sap-s4hana-fico-implementation.skill

| sap-s4hana-fico-implementation.skill

|  
|  

|
View all files
|

Repository files navigation

README
Contributing
MIT license

More items

🚀 SAP S/4HANA FICO Implementation Skill

The most comprehensive FICO implementation guide for SAP S/4HANA — serves both freshers learning greenfield implementations and professionals tackling complex configurations.

[Image description: SAP S/4HANA]

[Image description: FICO]

[Image description: License: MIT]

[Image description: Implementation Guide]

🎯 What This Skill Does

This skill transforms Claude into a senior SAP S/4HANA FICO implementation consultant providing:

escription: FICO]

[Image description: License: MIT]

[Image description: Implementation Guide]

🎯 What This Skill Does

This skill transforms Claude into a senior SAP S/4HANA FICO implementation consultant providing:

For Freshers/Learners 👨‍🎓

Step-by-step teaching with business context

End-to-end greenfield implementation guidance

All FI & CO modules to L5 process level

Testing guidance (unit + integration)

Real-world examples and templates

For Professionals 👨‍💼

Direct config paths for complex scenarios

Country-specific localizations (50+ countries)

Advanced integrations (MM, SD, PP, PS, HR + external)

Multiple solution approaches with trade-offs

Performance & maintenance considerations

✨ Key Features

📚 Comprehensive Coverage

✅ All FI Modules: GL, AP, AR, AA, BL, TR

✅ All CO Modules: Cost Centers, Internal Orders, CO-PA, Product Costing, Profit Centers

✅ L5 Process Depth: Every SPRO path, transaction code, IMG activity, config table

✅ Field-Level Guidance: What each field does, example values, impact

✅ Dependencies Mapped: What must be configured first, what this affects

🌍 Global Localization

✅ Top 10 Countries Detailed: India (TDS, GST), USA (Sales Tax, 1099), Germany (VAT), UK (MTD), China (Golden Tax), France, Japan, Brazil, Canada, Australia

e configured first, what this affects

🌍 Global Localization

✅ Top 10 Countries Detailed: India (TDS, GST), USA (Sales Tax, 1099), Germany (VAT), UK (MTD), China (Golden Tax), France, Japan, Brazil, Canada, Australia

✅ 50+ Countries Framework: How to find and configure any country

✅ Statutory Reporting: Country-specific financial statements, tax returns

🔗 Integration Mastery

✅ SAP-Native: MM-FI (MIRO, GR/IR, OBYC), SD-FI (Billing, Revenue, VKOA), PP-CO, PS-FI, HR-FI

✅ External Banking: SWIFT MT940, EDI, Payment Gateways

✅ External Treasury: Bloomberg, Kyriba, Reval

✅ Tax Engines: Vertex, Avalara

📄 Multi-Format Output

📄 Word Documents: Config workbooks with screenshot placeholders

📊 Excel Trackers: SPRO checklists with status and sign-off

📝 Markdown Guides: Copy to Confluence/Notion

📋 Templates: GL Master, Cost Center, Test Scripts, Cutover Checklists

🧪 Testing Built-In

✅ Unit Testing: How to verify each config step

✅ Integration Testing: P2P, O2C, R2R end-to-end scenarios

✅ Test Data: Sample vendors, customers, materials

✅ Expected Results: What success looks like

🚀 Quick Start

Installation

Download sap-s4hana-fico-implementation.skill

Install in your Claude environment

Start with: "I need help with FI-GL configuration" or "How do I set up CO-PA?"

s: What success looks like

🚀 Quick Start

Installation

Download sap-s4hana-fico-implementation.skill

Install in your Claude environment

Start with: "I need help with FI-GL configuration" or "How do I set up CO-PA?"

First-Time Use

The skill will ask:

Are you learning FICO (step-by-step teaching), or

Are you a professional with specific requirements (direct solutions)?

This adapts the response style to your needs.

📋 Modules Covered

Financial Accounting (FI)

Module |
Coverage |
Key Configs |

FI-GL |
Chart of Accounts → Parallel Ledgers |
OB13, FS00, FAGL_SPLIT_CUST, FINSC_LEDGER |

FI-AP |
Vendor Master → Payment Program |
FK01, FBZP, F110, OBXL |

FI-AR |
Customer Master → Credit Management |
FD01, UKM_CONFIG, F150, OBXR |

FI-AA |
Asset Master → Depreciation |
AS01, AFAMA, AO90, OADB |

FI-BL |
House Banks → Reconciliation |
FI12, FF67, FCHI |

FI-TR |
In-House Cash → Payment Factory |
IHC Config, FPY1 |

Controlling (CO)

Module |
Coverage |
Key Configs |

CO-OM |
Cost Elements → Cost Centers |
OKKP, OKA2, KS01, OKEON |

CO-IO |
Order Types → Settlement |
KOT2, KO01, KANK |

CO-PA |
Operating Concern → Profitability |
KEA0, KEA5, KEA6, KEDR |

CO-PC |
Material Ledger → Actual Costing |
CKMLCP, OMWM, OMG2 |

CO-PCA |
Profit Centers → Postings |
KCH1, KE51, KE59 |

ement |
KOT2, KO01, KANK |

CO-PA |
Operating Concern → Profitability |
KEA0, KEA5, KEA6, KEDR |

CO-PC |
Material Ledger → Actual Costing |
CKMLCP, OMWM, OMG2 |

CO-PCA |
Profit Centers → Postings |
KCH1, KE51, KE59 |

🌍 Localization Coverage

Detailed Country Files

✅ India: TDS, GST (GSTIN, Tax Procedure, HSN Codes), e-Invoice (IRN, QR Code), e-Way Bill

✅ USA: Sales Tax (jurisdiction codes), Withholding Tax (1099 forms), State requirements

✅ Germany: VAT, Tax on Sales/Purchases, DATEV export

✅ UK: VAT, MTD (Making Tax Digital), CIS

✅ China: Golden Tax, Fapiao, Export VAT

✅ France: VAT, DAS2, FEC

✅ Japan: Consumption Tax, J-SOX

✅ Brazil: NF-e, SPED, ICMS/IPI

✅ Canada: GST/HST/PST, Provincial variations

✅ Australia: GST, BAS, STP

Framework for Other Countries

🌐 50+ Countries: Localization framework explains how to find SAP Notes, country version, config tables for any country

🔗 Integration Scenarios

SAP-Native Integrations

MM-FI: Invoice Verification (MIRO) → Automatic Account Determination (OBYC) → GR/IR Clearing

SD-FI: Billing (VF01) → Revenue Recognition → Account Determination (VKOA) → Credit Management

PP-CO: Production Orders → Cost Object Controlling → Variance Analysis

PS-FI: WBS Settlement → Budget Management → Revenue Recognition (POC)

1) → Revenue Recognition → Account Determination (VKOA) → Credit Management

PP-CO: Production Orders → Cost Object Controlling → Variance Analysis

PS-FI: WBS Settlement → Budget Management → Revenue Recognition (POC)

HR-FI: Payroll Postings → Cost Center Assignment → Symbolic Accounts (OBMB)

External Integrations

Banking: SWIFT MT940 import, EDI formats (ACH, SEPA), Multi-Bank Connectivity

Treasury: Bloomberg, Kyriba, Reval integration for cash management, hedging

Tax: Vertex, Avalara for automated tax determination and compliance

📁 Repository Structure

sap-s4hana-fico-implementation/
│
├── SKILL.md ← Core skill logic and workflow
├── FRAMEWORK.md ← Template for creating additional modules
├── README.md ← This file
├── LICENSE ← MIT License
│
├── references/
│ ├── fi-modules/
│ │ ├── fi-gl-general-ledger.md ✅ COMPLETE (700+ lines, professional depth)
│ │ ├── fi-ap-accounts-payable.md [Use FRAMEWORK.md template]
│ │ ├── fi-ar-accounts-receivable.md [Use FRAMEWORK.md template]
│ │ ├── fi-aa-asset-accounting.md [Use FRAMEWORK.md template]
│ │ ├── fi-bl-bank-accounting.md [Use FRAMEWORK.md template]
│ │ └── fi-tr-treasury.md [Use FRAMEWORK.md template]
│ │
│ ├── co-modules/
│ │ ├── co-om-cost-centers.md [Use FRAMEWORK.md template]

e FRAMEWORK.md template]
│ │ ├── fi-bl-bank-accounting.md [Use FRAMEWORK.md template]
│ │ └── fi-tr-treasury.md [Use FRAMEWORK.md template]
│ │
│ ├── co-modules/
│ │ ├── co-om-cost-centers.md [Use FRAMEWORK.md template]
│ │ ├── co-io-internal-orders.md [Use FRAMEWORK.md template]
│ │ ├── co-pa-profitability-analysis.md [Use FRAMEWORK.md template]
│ │ ├── co-pc-product-costing.md [Use FRAMEWORK.md template]
│ │ └── co-pca-profit-centers.md [Use FRAMEWORK.md template]
│ │
│ ├── integrations/
│ │ ├── mm-fi-integration.md [Use FRAMEWORK.md template]
│ │ ├── sd-fi-integration.md [Use FRAMEWORK.md template]
│ │ ├── pp-co-integration.md [Use FRAMEWORK.md template]
│ │ ├── ps-fi-integration.md [Use FRAMEWORK.md template]
│ │ ├── hr-fi-integration.md [Use FRAMEWORK.md template]
│ │ ├── external-banking.md [Use FRAMEWORK.md template]
│ │ ├── external-treasury.md [Use FRAMEWORK.md template]
│ │ └── external-tax-engines.md [Use FRAMEWORK.md template]
│ │
│ ├── localizations/
│ │ ├── localization-framework.md [Use FRAMEWORK.md template]
│ │ ├── india-localization.md [Use FRAMEWORK.md template]
│ │ ├── usa-localization.md [Use FRAMEWORK.md template]
│ │ ├── germany-localization.md [Use FRAMEWORK.md template]
│ │ ├── uk-localization.md [Use FRAMEWORK.md template]

ndia-localization.md [Use FRAMEWORK.md template]
│ │ ├── usa-localization.md [Use FRAMEWORK.md template]
│ │ ├── germany-localization.md [Use FRAMEWORK.md template]
│ │ ├── uk-localization.md [Use FRAMEWORK.md template]
│ │ ├── china-localization.md [Use FRAMEWORK.md template]
│ │ └── [50+ more countries...]
│ │
│ ├── testing/
│ │ ├── unit-testing-guide.md [Use FRAMEWORK.md template]
│ │ └── integration-testing-guide.md [Use FRAMEWORK.md template]
│ │
│ └── templates/
│ ├── config-tracker-template.xlsx
│ ├── gl-master-template.xlsx
│ ├── cost-center-template.xlsx
│ ├── test-script-template.xlsx
│ └── [More templates...]
│
└── evals/
└── evals.json [Test cases]

🛠️ How to Expand This Skill

The skill is designed for incremental expansion. It works immediately with the current structure, and improves as you add modules.

Step-by-Step Expansion

Choose a module from the list above (e.g., FI-AP)

Copy the template from FRAMEWORK.md

Fill in SAP-accurate content:

SPRO paths from S/4HANA system

Transaction codes (verify in S/4HANA)

IMG activities and config tables

Field-by-field guidance with examples

Testing steps

Dependencies and common mistakes

Save as [module-name].md in appropriate folder

Skill automatically picks it up when users ask about that module

Estimated Effort

Field-by-field guidance with examples

Testing steps

Dependencies and common mistakes

Save as [module-name].md in appropriate folder

Skill automatically picks it up when users ask about that module

Estimated Effort

FI/CO Module: 4-6 hours (400-600 lines)

Integration: 2-3 hours (200-300 lines)

Country Localization: 3-4 hours (300-400 lines)

Testing Guide: 2-3 hours (200-300 lines)

Total for Complete Skill: ~113 hours (all modules + integrations + 10 countries + t