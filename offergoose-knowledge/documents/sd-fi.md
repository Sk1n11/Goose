# sd-fi.md

Topic: My GitHub knowledge

# Sd fi

Topic: Turkey

Here is the complete, detailed text and information transcribed directly from the SAP S/4HANA SD-FI Integration document:
Cybex – SAP S/4HANA SD-FI Integration
From Order to Cash – Complete Process, Configuration, Accounting and Reporting
One Order. Many Steps. Full Integration. Correct Accounting.
Cybex Solutions for a Better Tomorrow | Same data. Integrated process. Accurate accounting. Better decisions.
Key Integration (Sidebar)
 * SD → FI (Billing)
 * MM → FI (Goods Issue)
 * Customer & Material master data
 * Pricing → Revenue account (VKOA)
 * Tax → FI (OBYC)
 * Automatic postings (RD00/RD04)
1. End-to-End Process Flow (Order to Cash)
 * Create Sales Order
 * VA01 / Fiori
 * Pricing, availability, ATP
 * Delivery & Picking
 * VL01N
 * Picking, packing, GI
 * Goods Issue (PGI)
 * Post GI
 * Inventory ↓
 * COGS to FI
 * Billing
 * VF01 / Fiori
 * Generate invoice
 * Revenue & Tax to FI
 * Accounts Receivable
 * Customer open items
 * Incoming payment
 * Clearing (F-28)
 * Reporting
 * GL, Customer, Sales
 * COGS, Revenue, Tax
 * Analysis (e.g. RD00/RD04)
1. Sales Order – Key Elements
| Field / Element | Description / Example |
|---|---|
| Sales Organization (VKORG) | e.g. DE01 (Germany), TR01 (Turkey) |
| Distribution Channel (VTWEG) | e.g.

x
 * Analysis (e.g. RD00/RD04)
1. Sales Order – Key Elements
| Field / Element | Description / Example |
|---|---|
| Sales Organization (VKORG) | e.g. DE01 (Germany), TR01 (Turkey) |
| Distribution Channel (VTWEG) | e.g. WH (Wholesale), DT (DTC) |

4)
1. Sales Order – Key Elements
| Field / Element | Description / Example |
|---|---|
| Sales Organization (VKORG) | e.g. DE01 (Germany), TR01 (Turkey) |
| Distribution Channel (VTWEG) | e.g. WH (Wholesale), DT (DTC) |
| Division (SPART) | e.g. PR (Products) |
| Customer (KUNNR) | Sold-to, Ship-to, Bill-to, Payer |
| Material (MATNR) | From material master (5-level hierarchy) |
| Pricing Procedure (KALSM) | Determines condition types and sequence |
| Account Determination | VKOA (revenue), OBYC |
2. Pricing – Conditions and Determination
| Condition Type | Example | Purpose | Input / Basis |
|---|---|---|---|
| PR00 | Base Price | List price | Material / Customer / Price list |
| K007 | Customer Discount | % or amount | Customer / Material |
| K008 | Material Discount | % or amount | Material |
| K017 | Header Discount | % or amount | Sales order header |
| BRTO | Gross Value | System | Calculated |
| MWST | Output Tax | VAT / KDV | Tax code, country, region |
| SKTO | Cash Discount | Payment terms | Term of payment |

Header Discount | % or amount | Sales order header |
| BRTO | Gross Value | System | Calculated |
| MWST | Output Tax | VAT / KDV | Tax code, country, region |
| SKTO | Cash Discount | Payment terms | Term of payment |
| FRA1 | Freight | Delivery charges | Shipment / Incoterms |
3. Discount & Tax Determination
Ways to Determine Discounts
 * By percentage (%)
 * By fixed amount
 * By value scale (condition record)
 * By customer/material group
 * By pay. terms (cash discount)

pment / Incoterms |
3. Discount & Tax Determination
Ways to Determine Discounts
 * By percentage (%)
 * By fixed amount
 * By value scale (condition record)
 * By customer/material group
 * By pay. terms (cash discount)
 * By promotion / campaign
 * By manual entry (with authorization)
Tax Determination
 * Tax code in material / order
 * Ship-to country and region
 * Customer tax classification
 * Account determination (OBYC)
 * Procedure (e.g. MWST / KDV)
 * Exemptions / zero-rated
 * Reversing tax (returns/credits)
> Important Note: Condition records (VK11/12/13) maintain values for condition types. Pricing procedure (V/08, V/07) defines sequence, calculation type and account key.
> 
4. Material – 5 Level Hierarchy (Example)
 * Level 1: Product Category (e.g. Strollers)
 * Level 2: Product Family (e.g.

dition types. Pricing procedure (V/08, V/07) defines sequence, calculation type and account key.
> 
4. Material – 5 Level Hierarchy (Example)
 * Level 1: Product Category (e.g. Strollers)
 * Level 2: Product Family (e.g. Priam, Balios)
 * Level 3: Product Group (e.g. Seat, Frame, Accessories)
 * Level 4: Material Group (e.g. Textile, Metal, Plastic)
 * Level 5: Material (MATNR) (e.g. 520001 – Priam Seat)
Valuation Class
 * Determines inventory accounts (OBYC BSX/GBB/PRD)
 * Linked to material type and chart of accounts
5. Account Determination
VKOA – Revenue Account Determination
| Key | Meaning | Example G/L |
|---|---|---|
| ERL | Domestic sales revenue | 400000 |

s (OBYC BSX/GBB/PRD)
 * Linked to material type and chart of accounts
5. Account Determination
VKOA – Revenue Account Determination
| Key | Meaning | Example G/L |
|---|---|---|
| ERL | Domestic sales revenue | 400000 |
| ERS | Export sales revenue | 410000 |
| ERF | Intercompany revenue | 420000 |
| ER3 | Returns / Credit memo | 409000 |
OBYC – Automatic Postings (FI)
| Transaction | OBYC Key | Example G/L |
|---|---|---|
| Customer posting | D | 140000 (A/R) |
| Output tax (sales) | MWS / KDV | 177000 (VAT) |
| Inventory (BSX) | | 300000 |
| GR/IR (WRX) | | 310000 |
| Expense (PRO) | | 500000 |

n | OBYC Key | Example G/L |
|---|---|---|
| Customer posting | D | 140000 (A/R) |
| Output tax (sales) | MWS / KDV | 177000 (VAT) |
| Inventory (BSX) | | 300000 |
| GR/IR (WRX) | | 310000 |
| Expense (PRO) | | 500000 |
| Stock clearing (GBB) | | 300000 |
6. Automatic Postings – RD00 & RD04
 * RD00 – Master Data:
 * Assigns G/L accounts to master data automatically
 * Customers (reconciliation account)
 * Vendors (reconciliation account)
 * Materials (inventory, expense accounts)
 * Uses OBYC and account groups
 * Useful for mass updates and new records
 * RD04 – Open Items:
 * Automatically posts open items
 * Sales orders (billing due list)
 * Purchase orders (GR/IR, invoice)
 * Proposals can be reviewed before posting
 * Schedules via background job
 * Reduces manual posting efforts
> Cybex Use Case: Factory invoice automation and periodic posting can be executed via RD04 (e.g.

/IR, invoice)
 * Proposals can be reviewed before posting
 * Schedules via background job
 * Reduces manual posting efforts
> Cybex Use Case: Factory invoice automation and periodic posting can be executed via RD04 (e.g. for intercompany or scheduled billing). Ensure account determination is correctly configured.
> 
7. MM Integration – Purchase Order to GR/IR

Factory invoice automation and periodic posting can be executed via RD04 (e.g. for intercompany or scheduled billing). Ensure account determination is correctly configured.
> 
7. MM Integration – Purchase Order to GR/IR
 * Create PO (ME21N, Account assignment (e.g. stock))
 * Goods Receipt (MIGO, Dr Inventory, Cr GR/IR (OBYC WRX))
 * Invoice Receipt (MIRO, Dr GR/IR, Cr Vendor (OBYC KBS))
8. Complete SD-FI Accounting Examples (Cybex Order)
 * Example Scenario: Cybex sells 10 units of stroller at EUR 100 each to German customer.
 * Discount: 10% (K007)
 * VAT: 19% (MWST)
 * Standard cost: EUR 60 per unit
Pricing Calculation
 * List price: 10 × 100 = 1,000
 * Discount 10%: -100 → Net: 900
 * VAT 19%: 171 → Total: 1,071
1. Goods Issue (PGI)
| Account | Debit | Credit |
|---|---|---|
| COGS (e.g. 500000) | 600.00 | - |
| Inventory (e.g. 300000) | - | 600.00 |
2. Billing (Invoice)
| Account | Debit | Credit |
|---|---|---|
| Accounts Receivable (140000) | 1,071.00 | - |
| Sales Revenue | - | 900.00 |
| Output Tax | - | 171.00 |
3. Incoming Payment
| Account | Debit | Credit |
|---|---|---|
| Bank (100000) | 1,071.00 | - |

|
|---|---|---|
| Accounts Receivable (140000) | 1,071.00 | - |
| Sales Revenue | - | 900.00 |
| Output Tax | - | 171.00 |
3. Incoming Payment

| Account | Debit | Credit |
|---|---|---|
| Bank (100000) | 1,071.00 | - |

|
|---|---|---|
| Accounts Receivable (140000) | 1,071.00 | - |
| Sales Revenue | - | 900.00 |
| Output Tax | - | 171.00 |
3. Incoming Payment
| Account | Debit | Credit |
|---|---|---|
| Bank (100000) | 1,071.00 | - |
| Accounts Receivable (140000) | - | 1,071.00 |
9. SAP Configuration Checklist (Key Steps)
 * SD Organizational Structure: OVX5 / OVX3 / OVXI / OVXB / OVXD
 * Customer Master Data: XD01 (account group, reconciliation acct)
 * Material Master Data: MM01 (valuation class, sales views)
 * Pricing Procedure: V/08, V/07 (condition types, sequence)
 * Condition Records: VK11 / VK12 / VK13 (customers/materials)
 * VKOA (Revenue): Define account keys and G/L mapping
 * OBYC (Tax & MM): Define tax, inventory, GR/IR, expense accounts
 * Copy Control: VTLA / VTFA (order → delivery → billing)
 * Billing & FI Integration: Document type, number range, posting keys
 * Automatic Posting Jobs: RD00 / RD04 (scheduling via SM35)
 * Reporting: FBL5N, VA05, MB5B, CD-PA (if used)
10. Reporting and Reconciliation
| Report | Purpose |
|---|---|
| FBL5N | Customer line items (A/R) |
| VA05 | Sales orders overview |
| VF03 | Billing document details |
| MB5B | Stock movements (Goods Issue) |

f used)
10. Reporting and Reconciliation
| Report | Purpose |
|---|---|
| FBL5N | Customer line items (A/R) |
| VA05 | Sales orders overview |
| VF03 | Billing document details |
| MB5B | Stock movements (Goods Issue) |
| CO-PA | Profitability analysis (if activated) |
| RD00 logs | Master data posting log |

line items (A/R) |
| VA05 | Sales orders overview |
| VF03 | Billing document details |
| MB5B | Stock movements (Goods Issue) |
| CO-PA | Profitability analysis (if activated) |
| RD00 logs | Master data posting log |
| RD04 logs | Automatic posting results |
| Trial Balance | Reconcile revenue, COGS, tax |
11. Key Takeaways
 * Revenue is determined by VKOA based on pricing procedure account keys.
 * COGS is posted at Goods Issue using valuation class and OBYC.
 * Discounts and taxes are controlled by condition types and tax configuration.
 * OBYC ensures automatic account determination (FI & MM).
 * RD00 and RD04 help with automatic postings and mass processing.
 * Master data (customer, material, pricing) is critical for correct accounting.
 * The same order flows through SD, MM and FI with full transparency.
 * Always reconcile with reports and test to end-end scenarios.
Objective & References (Footer)

aterial, pricing) is critical for correct accounting.
 * The same order flows through SD, MM and FI with full transparency.
 * Always reconcile with reports and test to end-end scenarios.
Objective & References (Footer)
> Objective: A fully integrated SD-FI process in SAP S/4HANA for Cybex, ensuring correct revenue, COGS, tax postings and automated, compliant financial reporting.
> 
> References:
> * SAP S/4HANA Configuration Guide
> * Cybex - Adesso TR email (Depreciation Keys under VUK)
> * Cybex FI/CO Test Scenarios
> 
> Tagline: Process. People. Precision.
>