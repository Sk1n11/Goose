# contributing.md

Topic: My GitHub knowledge

# CONTRIBUTING.md

Topic: Free SAP FICO sources — auto-fetched

// Repository: https://github.com/ninadtrivedi-finance/sap-s4hana-fico-implementation
// File: CONTRIBUTING.md

# Contributing to SAP S/4HANA FICO Implementation Skill

Thank you for your interest in improving this skill! This is used by SAP FICO consultants, finance transformation teams, and IT architects worldwide.

---

## Ways to Contribute

### 🐛 Report Issues
Found an inaccuracy? Missing transaction code? Outdated SPRO path?
Open a GitHub Issue with:
- Module affected (FI-GL, FI-AP, CO-PA, etc.)
- What the skill currently says
- What it should say (with SAP reference if possible)
- Which S/4HANA release this applies to

### 📝 Improve Module Content
The 31 reference files are the heart of the skill's accuracy:

**High-Value Improvements:**
- Add missing transaction codes or SPRO paths
- Update for latest S/4HANA release changes
- Add real-world configuration examples
- Enhance testing scenarios
- Add troubleshooting for common errors

**Module Enhancement Priority:**
1. FI modules (most frequently used)
2. CO-PA and CO-PC (high business value)
3. Integration modules (critical for end-to-end)
4. Country localizations (expand to more countries)
5. Testing guides (more scenarios)

y:**
1. FI modules (most frequently used)
2. CO-PA and CO-PC (high business value)
3. Integration modules (critical for end-to-end)
4. Country localizations (expand to more countries)
5. Testing guides (more scenarios)

### 🌍 Add Country Localizations
Current: 10 detailed countries. Target: 50+

📝 Improve Module Content — lue)
3. Integration modules (critical for end-to-end)
4. Country localizations (expand to more countries)
5. Testing guides (more scenarios)

### 🌍 Add Country Localizations
Current: 10 detailed countries. Target: 50+

**High-Priority Countries to Add:**
- Mexico, Argentina, Chile (Latin America)
- Singapore, Malaysia, Indonesia, Thailand (APAC)
- Saudi Arabia, UAE (Middle East)
- South Africa, Nigeria (Africa)
- Italy, Spain, Netherlands, Switzerland (Europe)

**Template:** Use `references/localizations/india-localization.md` as guide

### 🔗 Add Integration Scenarios
Expand external integrations:
- Salesforce integration
- Workday integration
- Oracle EPM integration
- SAP Ariba integration
- SAP Concur integration
- Additional treasury systems

### ✅ Add Eval Test Cases
Current: 3 test cases. Target: 20+

Add to `evals/evals.json`:
- Edge cases (e.g., Classic GL to S/4HANA migration)

SAP Ariba integration
- SAP Concur integration
- Additional treasury systems

### ✅ Add Eval Test Cases
Current: 3 test cases. Target: 20+

Add to `evals/evals.json`:
- Edge cases (e.g., Classic GL to S/4HANA migration)
- Complex scenarios (e.g., Multi-currency with multiple parallel ledgers)
- Industry-specific (e.g., Pharmaceutical GxP, Mining Asset Accounting)
- Integration scenarios (e.g., MM-FI with split valuation)

### 📊 Add Templates
Create Excel/Word templates in `references/templates/`:
- Configuration tracker (enhanced with formulas)
- Master data migration templates (with validations)

✅ Add Eval Test Cases — rios (e.g., MM-FI with split valuation)

### 📊 Add Templates
Create Excel/Word templates in `references/templates/`:
- Configuration tracker (enhanced with formulas)
- Master data migration templates (with validations)
- Test script templates (by module)
- Cutover checklist (detailed activities)
- Training materials (by role: AP Clerk, AR Clerk, GL Accountant)

---

## How to Submit a Contribution

1. **Fork** this repository
2. **Create a branch**: `git checkout -b feature/enhance-fi-ap-payment-program`
3. **Make your changes** - Keep them focused (one topic per PR)
4. **Test your changes:**
 - Verify transaction codes in S/4HANA system

ory
2. **Create a branch**: `git checkout -b feature/enhance-fi-ap-payment-program`
3. **Make your changes** - Keep them focused (one topic per PR)
4. **Test your changes:**
 - Verify transaction codes in S/4HANA system
 - Check SPRO paths are accurate
 - Ensure formatting is consistent
5. **Update documentation** if adding new capabilities
6. **Submit a Pull Request** with clear description:
 ```
 ## What Changed
 Enhanced FI-AP Payment Program configuration with:
 - Additional payment methods (Real-Time Payments, SWIFT gpi)
 - Bank API integration steps
 - Testing scenarios for multi-currency payments
 
 ## Why This Matters
 Addresses gap in modern payment methods. Many clients now require
 real-time payments and SWIFT gpi tracking.
 
 ## Tested In
 SAP S/4HANA 2023 FPS02
 ```

---

## Content Quality Standards

What Changed — ents
 
 ## Why This Matters
 Addresses gap in modern payment methods. Many clients now require
 real-time payments and SWIFT gpi tracking.
 
 ## Tested In
 SAP S/4HANA 2023 FPS02
 ```

---

## Content Quality Standards

When contributing FICO content, follow these standards:

### Accuracy
- ✅ Use correct SAP terminology (transaction codes, table names, field names)
- ✅ Cite S/4HANA release where features were introduced (e.g., "New in 2022 FPS01")

uting FICO content, follow these standards:

### Accuracy
- ✅ Use correct SAP terminology (transaction codes, table names, field names)
- ✅ Cite S/4HANA release where features were introduced (e.g., "New in 2022 FPS01")
- ✅ Provide specific transaction codes and config tables (not vague descriptions)
- ✅ Test configuration steps in actual S/4HANA system before documenting

### Completeness
- ✅ Include SPRO path (full menu navigation)
- ✅ Include transaction code
- ✅ Include IMG activity code (if applicable)
- ✅ Include configuration table name
- ✅ Document all dependencies (what must be configured first)
- ✅ Provide testing steps (how to verify it works)
- ✅ Note common mistakes and how to avoid them

### Clarity
- ✅ Explain the "why" before the "how" (business context)
- ✅ Use clear, concise language
- ✅ Provide examples with realistic data
- ✅ Include screenshots placeholders where helpful: `[Screenshot: Transaction OB13 - Chart of Accounts field]`

### Honesty
- ✅ Be honest about complexity - FICO is hard

Clarity — language
- ✅ Provide examples with realistic data
- ✅ Include screenshots placeholders where helpful: `[Screenshot: Transaction OB13 - Chart of Accounts field]`

### Honesty
- ✅ Be honest about complexity - FICO is hard

language
- ✅ Provide examples with realistic data
- ✅ Include screenshots placeholders where helpful: `[Screenshot: Transaction OB13 - Chart of Accounts field]`

### Honesty
- ✅ Be honest about complexity - FICO is hard
- ✅ Provide pros AND cons for configuration approaches
- ✅ Note when multiple valid solutions exist
- ✅ Flag high-impact configurations that affect production systems
- ❌ No vendor-specific recommendations beyond SAP's own tooling
- ❌ No pricing information (changes too frequently)
- ❌ No unverified claims about S/4HANA capabilities

### Formatting
- ✅ Use consistent markdown formatting
- ✅ Follow template structure from FRAMEWORK.md
- ✅ Use tables for transaction code / field mappings
- ✅ Use code blocks for examples
- ✅ Use callouts for important notes:
 ```markdown
 **CRITICAL:** This configuration cannot be changed after go-live
 
 **Common Mistake:** Forgetting to assign Chart of Accounts (OB62)
 
 **S/4HANA Note:** Document splitting is mandatory
 ```

---

## Module Enhancement Guidelines

When enhancing an existing module:

### 1. Read Current Content First
Understand what's already documented before adding

### 2. Identify Gaps
Common gaps to address:
- Missing transaction codes
- Insufficient field-level guidance
- Weak testing procedures

# 1. Read Current Content First
Understand what's already documented before adding

### 2. Identify Gaps
Common gaps to address:
- Missing transaction codes
- Insufficient field-level guidance
- Weak testing procedures

Module Enhancement Guidelines — ## 1. Read Current Content First
Understand what's already documented before adding

### 2. Identify Gaps
Common gaps to address:
- Missing transaction codes
- Insufficient field-level guidance
- Weak testing procedures
- No troubleshooting section
- Missing S/4HANA-specific notes

### 3. Maintain Structure
Follow existing section headers:
- Overview
- Configuration Steps
- Testing
- Troubleshooting
- Quick Reference

### 4. Add Value, Don't Duplicate
If content exists, enhance it rather than rewriting

### 5. Cross-Reference Related Modules
Link to integration points:
```markdown
**Integration Point:** See MM-FI Integration for automatic account determination (OBYC)
```

---

## New Module Creation

If adding a completely new module:

### 1. Use FRAMEWORK.md Template
Copy the complete template structure

### 2. Determine Module Type
- FI Module: Save in `references/fi-modules/`
- CO Module: Save in `references/co-modules/`
- Integration: Save in `references/integrations/`
- Country: Save in `references/localizations/`

### 3.

. Determine Module Type
- FI Module: Save in `references/fi-modules/`
- CO Module: Save in `references/co-modules/`
- Integration: Save in `references/integrations/`
- Country: Save in `references/localizations/`

### 3. Naming Convention
- Use lowercase with hyphens
- Be descriptive but concise
- Examples: `fi-ca-contract-accounts.md`, `co-abc-activity-based-costing.md`

### 4. Include All Template Sections
Even if some sections are brief, include them all for consistency

3. Naming Convention — h hyphens
- Be descriptive but concise
- Examples: `fi-ca-contract-accounts.md`, `co-abc-activity-based-costing.md`

### 4. Include All Template Sections
Even if some sections are brief, include them all for consistency

### 5. Update Module Index
Add your new module to `references/MODULE_REFERENCE_INDEX.md`

---

## Country Localization Guidelines

When adding a new country:

### 1. Research Thoroughly
- Official tax authority websites
- SAP Help Portal for country version
- SAP Notes for localization
- Talk to local SAP consultants if possible

### 2. Cover Key Areas
- Tax system (VAT/GST/Sales Tax configuration)
- Withholding tax (if applicable)
- Statutory reporting (required reports, e-filing)
- Country-specific transactions
- Banking formats
- Chart of accounts considerations

as
- Tax system (VAT/GST/Sales Tax configuration)
- Withholding tax (if applicable)
- Statutory reporting (required reports, e-filing)
- Country-specific transactions
- Banking formats
- Chart of accounts considerations
- SAP Notes (list relevant OSS notes)

### 3. Provide Test Scenario
Complete end-to-end test with country-specific elements

### 4. Note Compliance Requirements
Flag mandatory vs optional configurations

---

## Testing Your Contribution

Before submitting:

### 1. Verify in SAP System
- Log into S/4HANA system (sandbox/demo)
- Navigate to transaction codes / SPRO paths
- Verify they exist and work as documented
- Check field names are accurate

### 2. Check Formatting
- No broken markdown

1. Verify in — SAP System
- Log into S/4HANA system (sandbox/demo)
- Navigate to transaction codes / SPRO paths
- Verify they exist and work as documented
- Check field names are accurate

### 2. Check Formatting
- No broken markdown
- Tables render correctly
- Code blocks formatted properly
- Links work (if any)

### 3. Run Through Skill
- Install skill in test environment
- Ask questions that would trigger your new content
- Verify skill provides correct guidance

### 4. Spell Check
- Use spell checker
- Pay attention to SAP terminology capitalization

- Install skill in test environment
- Ask questions that would trigger your new content
- Verify skill provides correct guidance

### 4. Spell Check
- Use spell checker
- Pay attention to SAP terminology capitalization
- Transaction codes should be UPPERCASE: FB50 (not fb50)

---

## Questions or Need Help?

- **General Questions:** Open a GitHub Discussion
- **Bug Reports:** Open a GitHub Issue
- **Feature Requests:** Open a GitHub Issue with "enhancement" label
- **Security Issues:** Email directly (don't post publicly)

---

## Recognition

Contributors will be:
- ✅ Acknowledged in README.md
- ✅ Listed in release notes for significant contributions
- ✅ Added to CONTRIBUTORS.md file
- ✅ Mentioned in project documentation

Significant contributions (new modules, major enhancements) will be highlighted in:
- Release announcements
- LinkedIn posts (with contributor attribution)
- SAP Community blog posts

---

## Code of Conduct

Recognition — mentation

Significant contributions (new modules, major enhancements) will be highlighted in:
- Release announcements
- LinkedIn posts (with contributor attribution)
- SAP Community blog posts

---

## Code of Conduct

- Be respectful and professional
- Focus on the content, not the person
- Provide constructive feedback

announcements
- LinkedIn posts (with contributor attribution)
- SAP Community blog posts

---

## Code of Conduct

- Be respectful and professional
- Focus on the content, not the person
- Provide constructive feedback
- Welcome newcomers
- Help others learn

This is a professional SAP community. Let's keep it that way.

---

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

---

**Thank you for helping make this the best SAP FICO implementation resource available!** 🙏

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

Registry Integrate external tools

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

Open Source COMMUNITY GitHub Sponsors Fund open source developers

PROGRAMS Security Lab
Maintainer Community
GitHub Stars
Archive Program

REPOSITORIES Topics
Trending
Collections

Enterprise ENTERPRISE SOLUTIONS Enterprise platform AI-powered developer platform

en source developers

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
Star 4  ( 4 ) You must be signed in to star a repository

About
Comprehensive SAP S/4HANA FICO implementation skill for Claude. Covers all FI & CO modules to L5, integrations, 50+ countries. Production-grade quality.
Resources
Readme
MIT license
Contributing

star a repository

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

-s4hana-fico-implementation.skill

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

Advanced integrations (MM, SD, PP, PS, HR + external)

Multiple solution approaches with trade-offs

Performance & maintenance considerations

✨ Key Features

📚 Comprehensive Coverage

✅ All FI Modules: GL, AP, AR, AA, BL, TR

integrations (MM, SD, PP, PS, HR + external)

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

✅ External Treasury: Bloomberg, Kyriba, Reval

✅ Tax Engines: Vertex, Avalara

📄 Multi-Format Output

📄 Word Documents: Config workbooks with screenshot placeholders

📊 Excel Trackers: SPRO checklists with status and sign-off

Treasury: Bloomberg, Kyriba, Reval

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
Chart of Accounts → Parallel Ledgers |
OB13, FS00, FAGL_SPLIT_CUST, FINSC_LEDGER |

FI-AP |
Vendor Master → Payment Program |
FK01, FBZP, F110, OBXL |

FI-AR |
Customer Master → Credit Management |
FD01, UKM_CONFIG, F150, OBXR |

FI-AA |

→ Parallel Ledgers |
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

✅ UK: VAT, MTD (Making Tax Digital), CIS

✅ China: Golden Tax, Fapiao, Export VAT

✅ France: VAT, DAS2, FEC

✅ Japan: Consumption Tax, J-SOX

✅ Brazil: NF-e, SPED, ICMS/IPI

✅ Canada: GST/HST/PST, Provincial variations

✅ Australia: GST, BAS, STP

igital), CIS

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

Tax: Vertex, Avalara for automated tax determination and compliance

📁 Repository Structure

sap-s4hana-fico-implementation/
│
├── SKILL.md ← Core skill logic and workflow
├── FRAMEWORK.md ← Template for creating additional modules
├── README.md ← This file
├── LICENSE ← MIT License
│

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
│ │ ├── mm-fi-integration.md [Use FRAMEWORK.md template]
│ │ ├── sd-fi-integration.md [Use FRAMEWORK.md template]
│ │ ├── pp-co-integration.md [Use FRAMEWORK.md template]
│ │ ├── ps-fi-integration.md [Use FRAMEWORK.md template]
│ │ ├── hr-fi-integration.md [Use FRAMEWORK.md template]

sd-fi-integration.md [Use FRAMEWORK.md template]
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
│ ├── gl-master-template.xlsx
│ ├── cost-center-template.xlsx
│ ├── test-script-template.xlsx
│ └── [More templates...]
│
└── evals/
└── evals.json [Test cases]

🛠️ How to Expand This Skill

The skill is designed for incremental expansion.

late.xlsx
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