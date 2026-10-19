# framework.md

Topic: My GitHub knowledge

# FRAMEWORK.md

Topic: Free SAP FICO sources — auto-fetched

// Repository: https://github.com/ninadtrivedi-finance/sap-s4hana-fico-implementation
// File: FRAMEWORK.md

# SAP S/4HANA FICO Implementation Skill - Framework Guide

This document explains how to expand the skill with additional modules, localizations, and integrations.

---

## Reference File Structure Standard

Every reference file should follow this template:

### Module Reference Files (references/fi-modules/, references/co-modules/)

```markdown
# [Module Name] — [Full Name] Configuration Guide

## Overview
[1-2 paragraphs: What is this module, business purpose, when used]

## L1-L5 Business Capabilities Covered
[List the SAP business capability hierarchy this module addresses]

Example:
- **L4:** General Ledger Accounting
 - **L5:** Capture Source Transactions
 - **L5:** Create Chart of Accounts
 [...]

## Configuration Steps (End-to-End)

### 1. [Config Step Name]

**SPRO Path:** 
[Full menu path from SAP Customizing Implementation Guide]

**Transaction Code:** `[T-CODE]`

**IMG Activity:** `[IMG_CODE]` (if applicable)

**Configuration Table:** `[TABLE_NAME]`

**Purpose:** 
[What this config does, when it's needed, business context]

**Prerequisites:**
[What must be configured first - with transaction codes]

MG_CODE]` (if applicable)

**Configuration Table:** `[TABLE_NAME]`

**Purpose:** 
[What this config does, when it's needed, business context]

**Prerequisites:**
[What must be configured first - with transaction codes]

**Fields:**

1. [Config Step Name] — f applicable)

**Configuration Table:** `[TABLE_NAME]`

**Purpose:** 
[What this config does, when it's needed, business context]

**Prerequisites:**
[What must be configured first - with transaction codes]

**Fields:**
- **[Field Name] (Field Technical Name)** [Required/Optional]: [What it does, example values, impact]
- **[Field Name]** [Required/Optional]: [...]

**Step-by-Step Instructions:**
1. Navigate to transaction `[T-CODE]`
2. [Action with screenshot placeholder marker]
3. Fill in fields:
 - **[Field]**: [Value]
4. Save

**Example Configuration:**
```
[Show realistic example with actual values]
```

**Testing:**
- **Unit Test:**
 1. [How to verify this config]
 2. Transaction: `[T-CODE]`
 3. Expected result: [What you should see]

- **Integration Test:** [If applicable - end-to-end scenario]

**Dependencies:**
- **Depends on:** [Prior config with T-code]
- **Affects:** [Downstream config]
- **Used in:** [Business processes that rely on this]

**Common Mistakes:**
- ❌ [Mistake 1]
- ❌ [Mistake 2]

nd scenario]

**Dependencies:**
- **Depends on:** [Prior config with T-code]
- **Affects:** [Downstream config]
- **Used in:** [Business processes that rely on this]

**Common Mistakes:**
- ❌ [Mistake 1]
- ❌ [Mistake 2]
- ✅ Best practice: [...]

**Troubleshooting:**
| Issue | Cause | Solution |
|-------|-------|----------|
| [Error message] | [Root cause] | [Fix with T-code] |

**S/4HANA Specifics:**
[Any differences from ECC, new features, deprecated functions]

---

leshooting:**
| Issue | Cause | Solution |
|-------|-------|----------|
| [Error message] | [Root cause] | [Fix with T-code] |

**S/4HANA Specifics:**
[Any differences from ECC, new features, deprecated functions]

---

[Repeat for each major config step in sequence]

## Advanced Configurations

### [Niche Scenario 1]
[How to handle complex requirements]

### [Niche Scenario 2]
[...]

## Country-Specific Considerations
[If module has localization aspects]

## Integration Points
[How this module integrates with others - with T-codes]

## Performance Considerations
[Volume thresholds, indexing, archiving]

## Maintenance & Support
[Common support issues, how to troubleshoot]

## Quick Reference

### Transaction Codes Summary
| T-Code | Description | Purpose |
|--------|-------------|---------|

holds, indexing, archiving]

## Maintenance & Support
[Common support issues, how to troubleshoot]

## Quick Reference

### Transaction Codes Summary
| T-Code | Description | Purpose |
|--------|-------------|---------|
| [CODE] | [Name] | [When to use] |

### Configuration Tables
| Table | Description | Key Fields |
|-------|-------------|------------|
| [TABLE] | [Purpose] | [Primary keys] |

---

This concludes the [Module Name] configuration guide.
```

---

## Integration Reference Files (references/integrations/)

```markdown
# [Module A]-[Module B] Integration Guide

## Overview
[What data flows between modules, business scenarios]

## Integration Points (L5 Level)

### Integration Point 1: [Name]

Integration Reference Fi — les (references/integrations/)

```markdown
# [Module A]-[Module B] Integration Guide

## Overview
[What data flows between modules, business scenarios]

## Integration Points (L5 Level)

### Integration Point 1: [Name]
**Business Scenario:** [When this happens]

**Data Flow:** [Module A] → [Module B]

**Transaction Codes:**
- Source: `[T-CODE]` in [Module A]
- Destination: `[T-CODE]` in [Module B]

**Configuration Required:**

#### Step 1: [Config Activity]
**SPRO Path:** [...]
**Transaction:** `[T-CODE]`
**Table:** `[TABLE]`

ion Codes:**
- Source: `[T-CODE]` in [Module A]
- Destination: `[T-CODE]` in [Module B]

**Configuration Required:**

#### Step 1: [Config Activity]
**SPRO Path:** [...]
**Transaction:** `[T-CODE]`
**Table:** `[TABLE]`

[Full config instructions]

#### Step 2: [...]

**Testing:**
1. Create test transaction in [Module A]
2. Verify automatic posting in [Module B]
3. Check GL document (FB03)
4. Verify account determination

**Troubleshooting:**
[Common integration errors]

---

[Repeat for each integration point]

## Automatic Account Determination
[Detailed table-by-table config]

## End-to-End Test Scenarios
[Complete business process flows]

## Common Issues
[Typical problems with solutions]
```

---

## Localization Reference Files (references/localizations/)

### Detailed Country Files (Top 10)

```markdown
# [Country Name] Localization Guide

## Overview
[Country-specific regulatory requirements, tax system, statutory reporting]

## Legal & Regulatory Context

Localization Reference Files (references/lo — calizations/)

### Detailed Country Files (Top 10)

```markdown
# [Country Name] Localization Guide

## Overview
[Country-specific regulatory requirements, tax system, statutory reporting]

## Legal & Regulatory Context
- **Tax Authority:** [Name]

Country Files (Top 10)

```markdown
# [Country Name] Localization Guide

## Overview
[Country-specific regulatory requirements, tax system, statutory reporting]

## Legal & Regulatory Context
- **Tax Authority:** [Name]
- **Tax Types:** [VAT, Income Tax, WHT, etc.]
- **Fiscal Year:** [Standard calendar or variant]
- **Statutory Reports:** [Required reports]
- **E-Filing Requirements:** [Yes/No, system]

## Configuration Steps

### 1. Tax Configuration

#### 1.1 Tax Procedure Setup
**SPRO Path:** [Country-specific path]
**Transaction:** `OBYZ`, `FTXP`
**Table:** `T007S`, `T001`, `T007V`

[Detailed setup]

#### 1.2 Tax Codes
**Transaction:** `FTXP`

[Table of tax codes with rates]

### 2. Withholding Tax (if applicable)

[Configuration steps]

### 3. Country-Specific GL Accounts

[Required statutory accounts]

### 4. Statutory Reporting

[How to generate required reports]

### 5. E-Filing Integration

[API connections, file formats]

## Business Process Examples

### Example 1: [Vendor Invoice with Tax]
[Step-by-step with screenshots markers]

### Example 2: [...]

## Compliance Checklist
☐ [Requirement 1]
☐ [Requirement 2]
[...]

## SAP Notes
[Relevant SAP Notes for this country]

## External References
[Links to tax authority websites, documentation]

ers]

### Example 2: [...]

## Compliance Checklist
☐ [Requirement 1]
☐ [Requirement 2]
[...]

## SAP Notes
[Relevant SAP Notes for this country]

## External References
[Links to tax authority websites, documentation]

Example 1: [Vendor Invoice with Tax] — kers]

### Example 2: [...]

## Compliance Checklist
☐ [Requirement 1]
☐ [Requirement 2]
[...]

## SAP Notes
[Relevant SAP Notes for this country]

## External References
[Links to tax authority websites, documentation]
```

### Localization Framework (For other countries)

```markdown
# Country Localization Framework

## How to Configure Any Country

### Step 1: Identify Country Version
**Transaction:** `SPRO` → [Country Versions path]
**Table:** `T005`

### Step 2: Research SAP Notes
- Search: "Country [XX] localization S/4HANA"
- SAP Support Portal
- Country-specific user groups

### Step 3: Tax Configuration Framework
[Generic approach applicable to any country]

### Step 4: Chart of Accounts Considerations
[Statutory account requirements]

### Step 5: Reporting Requirements
[How to identify and configure]

---

[Continue with generic framework]
```

---

## Testing Reference Files (references/testing/)

```markdown
# Unit Testing Guide

## Testing Methodology

For every config step:
1.

ents
[How to identify and configure]

---

[Continue with generic framework]
```

---

## Testing Reference Files (references/testing/)

```markdown
# Unit Testing Guide

## Testing Methodology

For every config step:
1. **Positive Test:** Config works as expected
2. **Negative Test:** System prevents incorrect data
3. **Integration Test:** Config affects downstream correctly

## Module-by-Module Test Scripts

### FI-GL Unit Tests

#### Test 1: Post Simple GL Journal
**Test ID:** FI-GL-UT-001

Testing Methodology — Test:** System prevents incorrect data
3. **Integration Test:** Config affects downstream correctly

## Module-by-Module Test Scripts

### FI-GL Unit Tests

#### Test 1: Post Simple GL Journal
**Test ID:** FI-GL-UT-001
**Purpose:** Verify GL accounts and posting keys work
**Prerequisites:** GL accounts created, periods open
**Steps:**
1. Transaction `FB50`
2. Enter: CoCode, Doc Date, Posting Date
3. Line 1: Debit GL [Account], Amount [X], Posting Key 40
4. Line 2: Credit GL [Account], Amount [X], Posting Key 50
5. Save
**Expected Result:** Document posted, number assigned
**Verification:** Transaction `FBL3N` - line items visible

---

[Continue for all modules]

## Integration Test Scenarios

### Procure-to-Pay (P2P)

Key 50
5. Save
**Expected Result:** Document posted, number assigned
**Verification:** Transaction `FBL3N` - line items visible

---

[Continue for all modules]

## Integration Test Scenarios

### Procure-to-Pay (P2P)

**Scenario:** Purchase of material with invoice and payment

**Test Steps:**
1. Create Purchase Order (ME21N)
 - Material: [X]
 - Vendor: [Y]
 - Quantity: [Z]
 - Save → Note PO number

2. Goods Receipt (MIGO)
 - Movement Type: 101
 - Reference: PO number from step 1
 - Post GR → Note Material Document

3. Verify GL Posting (FB03)
 - Search by Material Document
 - Expected: Debit Inventory, Credit GR/IR Clearing
 - Accounts: [Specific GL accounts]

4. Invoice Verification (MIRO)
 - Reference: PO number
 - Amount matches GR
 - Post IR → Note Accounting Document

5.

Procure-to-Pay (P2P) — rial Document
 - Expected: Debit Inventory, Credit GR/IR Clearing
 - Accounts: [Specific GL accounts]

4. Invoice Verification (MIRO)
 - Reference: PO number
 - Amount matches GR
 - Post IR → Note Accounting Document

5. Verify GL Posting (FB03)
 - Expected: Debit GR/IR Clearing, Credit Vendor
 - Accounts: [Specific GL accounts]

6. Automatic Payment (F110)
 - Run payment proposal
 - Execute payment run
 - Generate payment file

7. Verify GL Posting (FB03)

B03)
 - Expected: Debit GR/IR Clearing, Credit Vendor
 - Accounts: [Specific GL accounts]

6. Automatic Payment (F110)
 - Run payment proposal
 - Execute payment run
 - Generate payment file

7. Verify GL Posting (FB03)
 - Expected: Debit Vendor, Credit Bank
 - Accounts: [Specific GL accounts]

8. End-to-End Verification
 - Transaction `FBL3N` - Inventory GL should show net debit
 - Transaction `FBL1N` - Vendor account should be cleared
 - Transaction `FK10N` - Vendor balance should be zero

**Expected Final State:**
- Inventory increased by [Amount]
- Bank decreased by [Amount]
- Vendor cleared (zero balance)
- GR/IR cleared (zero balance)

---

[Continue for O2C, R2R, etc.]

## Test Data Templates
[Sample vendors, customers, materials, etc.]

## Test Result Documentation
[How to document test outcomes]
```

---

## How to Expand This Skill

### Priority Order for Adding Content:

1. **FI Modules (Critical):**
 - ✅ FI-GL-general-ledger.md (DONE - 450+ lines provided as example)
 - ⏳ FI-AP-accounts-payable.md (Use framework above)

Test Result Documentation — # How to Expand This Skill

### Priority Order for Adding Content:

1. **FI Modules (Critical):**
 - ✅ FI-GL-general-ledger.md (DONE - 450+ lines provided as example)
 - ⏳ FI-AP-accounts-payable.md (Use framework above)

# How to Expand This Skill

### Priority Order for Adding Content:

1. **FI Modules (Critical):**
 - ✅ FI-GL-general-ledger.md (DONE - 450+ lines provided as example)
 - ⏳ FI-AP-accounts-payable.md (Use framework above)
 - ⏳ FI-AR-accounts-receivable.md
 - ⏳ FI-AA-asset-accounting.md
 - ⏳ FI-BL-bank-accounting.md
 - ⏳ FI-TR-treasury.md (if needed)

2. **CO Modules (Critical):**
 - ⏳ CO-OM-cost-centers.md
 - ⏳ CO-IO-internal-orders.md
 - ⏳ CO-PA-profitability-analysis.md
 - ⏳ CO-PC-product-costing.md
 - ⏳ CO-PCA-profit-centers.md

3. **Integrations (High Priority):**
 - ⏳ MM-FI-integration.md
 - ⏳ SD-FI-integration.md
 - ⏳ PP-CO-integration.md
 - ⏳ PS-FI-integration.md
 - ⏳ HR-FI-integration.md

4. **Top 10 Country Localizations:**
 - ⏳ india-localization.md
 - ⏳ usa-localization.md
 - ⏳ germany-localization.md
 - ⏳ uk-localization.md
 - ⏳ china-localization.md
 - ⏳ france-localization.md
 - ⏳ japan-localization.md
 - ⏳ brazil-localization.md
 - ⏳ canada-localization.md
 - ⏳ australia-localization.md

5. **Testing Guides:**
 - ⏳ unit-testing-guide.md
 - ⏳ integration-testing-guide.md

6. **External Integrations:**
 - ⏳ external-banking.md
 - ⏳ external-treasury.md
 - ⏳ external-tax-engines.md

### Time Estimate per File:
- FI/CO Module: 4-6 hours (400-600 lines)

md
 - ⏳ integration-testing-guide.md

6. **External Integrations:**
 - ⏳ external-banking.md
 - ⏳ external-treasury.md
 - ⏳ external-tax-engines.md

### Time Estimate per File:
- FI/CO Module: 4-6 hours (400-600 lines)

Priority Order for Adding Content: — .md
 - ⏳ integration-testing-guide.md

6. **External Integrations:**
 - ⏳ external-banking.md
 - ⏳ external-treasury.md
 - ⏳ external-tax-engines.md

### Time Estimate per File:
- FI/CO Module: 4-6 hours (400-600 lines)
- Integration: 2-3 hours (200-300 lines)
- Country Localization: 3-4 hours (300-400 lines)
- Testing Guide: 2-3 hours (200-300 lines)

### Total Estimated Effort:
- 6 FI modules × 5 hours = 30 hours
- 5 CO modules × 5 hours = 25 hours
- 5 Integrations × 2.5 hours = 12.5 hours
- 10 Countries × 3.5 hours = 35 hours
- 2 Testing guides × 2.5 hours = 5 hours
- 3 External integrations × 2 hours = 6 hours
**Total: ~113 hours of content creation**

This can be done incrementally - skill works immediately with current structure, improves as you add modules.

---

## Quick Start for Contributors

To add a new module:
1. Copy the template from this file
2. Fill in all sections with SAP-accurate content
3. Verify transaction codes in S/4HANA system
4. Test the configuration steps yourself
5.

Start for Contributors

To add a new module:
1. Copy the template from this file
2. Fill in all sections with SAP-accurate content
3. Verify transaction codes in S/4HANA system
4. Test the configuration steps yourself
5. Add screenshot placeholders: `[Screenshot: Transaction XYZ - Field ABC]`
6. Save as `[module-name].md` in appropriate folder
7. Skill automatically picks it up when users ask about that module

---

Quick Start for Contributors — on steps yourself
5. Add screenshot placeholders: `[Screenshot: Transaction XYZ - Field ABC]`
6. Save as `[module-name].md` in appropriate folder
7. Skill automatically picks it up when users ask about that module

---

This framework ensures consistency across all reference files and makes the skill expandable by multiple contributors.

--- LINKED SOURCE READ FROM: https://github.com/ninadtrivedi-finance/sap-s4hana-fico-implementation ---
GitHub - ninadtrivedi-finance/sap-s4hana-fico-implementation: Comprehensive SAP S/4HANA FICO implementation skill for Claude. Covers all FI & CO modules to L5, integrations, 50+ countries. Production-grade quality. · GitHub

Skip to content

Navigation Menu

Sign in Appearance settings

Platform AI CODE CREATION GitHub Copilot Write better code with AI

l FI & CO modules to L5, integrations, 50+ countries. Production-grade quality. · GitHub

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

l topics

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

ions
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

For Freshers/Learners 👨‍🎓

Step-by-step teaching with business context

End-to-end greenfield implementation guidance

All FI & CO modules to L5 process level

Testing guidance (unit + integration)

Real-world examples and templates

For Professionals 👨‍💼

Direct config paths for complex scenarios

Country-specific localizations (50+ countries)

modules to L5 process level

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

✅ 50+ Countries Framework: How to find and configure any country

✅ Statutory Reporting: Country-specific financial statements, tax returns

🔗 Integration Mastery

✅ SAP-Native: MM-FI (MIRO, GR/IR, OBYC), SD-FI (Billing, Revenue, VKOA), PP-CO, PS-FI, HR-FI

✅ External Banking: SWIFT MT940, EDI, Payment Gateways

y-specific financial statements, tax returns

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

ching), or

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

🌍 Localization Coverage

Detailed Country Files

✅ India: TDS, GST (GSTIN, Tax Procedure, HSN Codes), e-Invoice (IRN, QR Code), e-Way Bill

✅ USA: Sales Tax (jurisdiction codes), Withholding Tax (1099 forms), State requirements

✅ Germany: VAT, Tax on Sales/Purchases, DATEV export

GST (GSTIN, Tax Procedure, HSN Codes), e-Invoice (IRN, QR Code), e-Way Bill

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

HR-FI: Payroll Postings → Cost Center Assignment → Symbolic Accounts (OBMB)

External Integrations

Banking: SWIFT MT940 import, EDI formats (ACH, SEPA), Multi-Bank Connectivity

Treasury: Bloomberg, Kyriba, Reval integration for cash management, hedging

r Assignment → Symbolic Accounts (OBMB)

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
│ │ ├── co-io-internal-orders.md [Use FRAMEWORK.md template]
│ │ ├── co-pa-profitability-analysis.md [Use FRAMEWORK.md template]
│ │ ├── co-pc-product-costing.md [Use FRAMEWORK.md template]
│ │ └── co-pca-profit-centers.md [Use FRAMEWORK.md template]
│ │
│ ├── integrations/

late]
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
│ │ ├── china-localization.md [Use FRAMEWORK.md template]
│ │ └── [50+ more countries...]
│ │
│ ├── testing/
│ │ ├── unit-testing-guide.md [Use FRAMEWORK.md template]
│ │ └── integration-testing-guide.md [Use FRAMEWORK.md template]
│ │
│ └── templates/
│ ├── config-tracker-template.xlsx

0+ more countries...]
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

FI/CO Module: 4-6 hours (400-600 lines)

Integration: 2-3 hours (200-300 lines)

Country Localization: 3-4 hours (300-400 lines)

Testing Guide: 2-3 hours (200-300 lines)

Total for Complete Skill: ~113 hours (all modules + integrations + 10 countries + t