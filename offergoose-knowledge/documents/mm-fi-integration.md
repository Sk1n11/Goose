# Mm fi integration

Topic: Cybex

Here is the complete, detailed text and information transcribed from the third document provided:
Cybex – SAP S/4HANA MM-FI Integration (Procure-to-Pay)
From Purchase Requisition to Vendor Payment – Complete Guide
Configuration · Determination Logic · Accounting Entries · Examples · Reporting
cybex: Solutions for a Better Tomorrow | Right Process. Right Configuration. Right Accounting. Better Business.
1. End-to-End Procure-to-Pay (P2P) Process Flow
 * Purchase Requisition (ME51N)
 * Internal request for goods/services
 * No FI posting
 * Purchase Order (ME21N)
 * Legally binding contract with vendor
 * No FI posting
 * Goods Receipt (MIGO)
 * Receive goods into stock or service entry
 * FI & MM posting
 * Dr Inventory / Expense
 * Cr GR/IR (WRX)
 * Invoice Verification (MIRO)
 * Match PO + GR + Invoice
 * Post vendor liability
 * Dr GR/IR, Input Tax, PRO (if any)
 * Cr Vendor (AP)
 * Outgoing Payment (F110 / F-53)
 * Automatic or manual payment (SEPA, wire)
 * Dr Vendor (AP)
 * Cr Bank (House Bank)
 * Reporting (F.01)
 * Balance Sheet, P&L
 * Vendor open items (FBL1N)
 * Material ledger & costs
 * Audit trail (ACDOCA)
2. Key Master Data Elements (MM-FI)
| Object / Field | Example (Cybex) | Purpose / Description |
|---|---|---|

(F.01)
 * Balance Sheet, P&L
 * Vendor open items (FBL1N)
 * Material ledger & costs
 * Audit trail (ACDOCA)
2. Key Master Data Elements (MM-FI)
| Object / Field | Example (Cybex) | Purpose / Description |
|---|---|---|
| Company Code | DE01 (Germany) | Legal entity, currency, CoA |
| Plant / Valuation Area | DE01 | Inventory valuation level |
| Purchasing Org. (EKORG) | P01 | Responsible for purchasing |
| Purchasing Group (EKGRP) | G01 | Purchaser / team |
| Vendor (LFA1 / LFB1) | 300000 | Vendor master & recon account |
| Material (MARA / MARC) | 100001 | Material master (purchasing & accounting) |
| Valuation Class (MBEW) | 3000 / 7920 | Determines inventory G/L via OBYC |
| Chart of Accounts | GBGR | Group Chart of Accounts |
| Currency | EUR | Transaction and company currency |
| Tax Code | V1 | 19% Input VAT (Germany) |
3. Account Assignment Categories (ME21N)
| Category | Description | Accounting Impact |
|---|---|---|
| (Blank) | Standard (Stock) | Inventory (Balance Sheet) via OBYC (BSX/WRX) |
| K | Cost Center | P&L Expense + Cost Center (GBB + VBR) |
| A | Fixed Asset | Asset Under Construction / Fixed Asset (ANL) |
| P | WBS Element | Project cost (GBB + VBR) |
| F | Order | Internal order (GBB + VBR) |
| U | Unknown | Used in special scenarios |

nter (GBB + VBR) |
| A | Fixed Asset | Asset Under Construction / Fixed Asset (ANL) |
| P | WBS Element | Project cost (GBB + VBR) |
| F | Order | Internal order (GBB + VBR) |
| U | Unknown | Used in special scenarios |
| L | Subcontracting | Components to subcontractor (BSV, KBS) |
| N | Consignment | Consignment stock (KBS) |
| S | Service | Service entry sheet (ML81N/MIRO) P&L Expense |
4. OBYC – Automatic Account Determination (MM \rightarrow FI)
| Transaction Key | Meaning | Typical G/L Account (Cybex Example) | Account Modifier | Usage |
|---|---|---|---|---|
| BSX | Inventory posting (Balance Sheet) | 1213000000 | – | Stock increase at GR (movement 101, 105...) |
| GBB | Offsetting entry (Consumption) | 5000000000 | VAX / VAY / VBR | COGS or expense posting (GI, consumption, cost center) |
| PRD | Price differences | 5190000000 | PRA / PRF | Price variances (PO vs. Invoice) |
| WRX | GR/IR clearing | 3215000000 | – | Temporary clearing between GR and Invoice |
| BSV | Change in stock (Subcontracting) | 4030000000 | – | Subcontracting stock change |
| KBS | Consignment liability | 2110000000 | – | Vendor liability for consignment |
| MWS | Input tax (MM) | 1540000000 | – | |
5. Material Master – 5 Level Hierarchy
 * Level 1: Product Category (e.g. Strollers)

ange |
| KBS | Consignment liability | 2110000000 | – | Vendor liability for consignment |
| MWS | Input tax (MM) | 1540000000 | – | |
5. Material Master – 5 Level Hierarchy
 * Level 1: Product Category (e.g. Strollers)
 * Level 2: Product Family (e.g. Priam, Balios)
 * Level 3: Product Group (e.g. Seat, Frame, Accessories)
 * Level 4: Material Group (e.g. Textile, Metal, Plastic)
 * Level 5: Material (MATNR) (e.g. 520001 – Priam Seat)
Valuation Class
 * Determines inventory accounts (OBYC)
 * Linked to material type and chart of accounts
 * Maintained at plant level (MM02)
 * Different classes for raw material, finished goods, trading
 * Can be split by plant, material group, etc.
6. OBYC Determination Logic (Step-by-Step)
 * System reads movement type (e.g. 101, 102, 122).
 * Reads transaction key from movement string (OMJJ).
 * Reads valuation class from material master (MBEW).
 * Reads account modifier (e.g. VAX) if required.
 * Reads valuation grouping code from plant (OMWD).
 * Searches OBYC (T030) with Chart of Accounts + Val. Class + Trans. Key (+ Mod.).
 * Retrieves G/L account and posts to ACDOCA.
 * MM and FI documents are created simultaneously.
> Key Tables: T156 (Movement type), T156SY (Transaction key), T030 (OBYC), T001K (Valuation area), T030K (Mod. acct.

Mod.).
 * Retrieves G/L account and posts to ACDOCA.
 * MM and FI documents are created simultaneously.
> Key Tables: T156 (Movement type), T156SY (Transaction key), T030 (OBYC), T001K (Valuation area), T030K (Mod. acct. determination).
> 
6. Process Highlights
 * Integrated MM and FI
 * Automatic account determination
 * Real-time postings to ACDOCA
 * Supports stock, services, assets
 * Handles tax, discounts, variances
 * Works for local and group reporting
7. Tax Determination on Procurement (TAXD / MWS)
 * Define tax procedure (OBYZ)
 * Define tax codes (FTXP) e.g. V1 = 19%
 * Assign accounts (OB40) Tax type MWST \rightarrow MWS
 * Maintain tax classification (customer/vendor/material)
 * System calculates tax during MIRO and posts to FI
Example Tax Codes (Cybex)
| Tax Code | Description | Rate | Country |
|---|---|---|---|
| V1 | Input VAT | 19% | Germany |
| V0 | 0% (Export) | 0% | EU |
| Z0 | Intra-Community | 0% | EU |
| E0 | Exempt | 0% | Germany |
| TR1 | Input VAT | 20% | Turkey |
 * Tax account determination uses OBYZ/OB40 (MWST) - not VKOA.
8. Pricing in Purchase Order (MM)
 * Info Records (ME11) store vendor, material, and pricing conditions.
 * Standard condition types: PB00 (Net price), Rabatt (discount), Fracht (freight), etc.

Z/OB40 (MWST) - not VKOA.
8. Pricing in Purchase Order (MM)
 * Info Records (ME11) store vendor, material, and pricing conditions.
 * Standard condition types: PB00 (Net price), Rabatt (discount), Fracht (freight), etc.
 * Pricing procedure (OMUM/OMQ2) defines sequence.
 * Conditions are not posted to FI until MIRO.
Common MM Condition Types
| Cond. Type | Description | Calc. Type | Typical Use |
|---|---|---|---|
| PB00 | Net price | B | Base price (PO) |
| SK04 / K004 | Cash discount | B | % or amount |
| ZPRO | Price (gross) | C | Alternative price |
| FRA1 | Freight | B | Amount |
| ZDIS | Header discount | B | % or amount |
9. Complete Accounting Entries – P2P Example (Cybex)
A. Goods Receipt (MIGO – 101)
 * Receive 100 pcs @ 10 EUR (Material 3000, V1 19%)
| Account | Debit | Credit |
|---|---|---|
| Inventory (BSX) | 1,000 | - |
| GR/IR (WRX) | - | 1,000 |
 * No tax at GR (for stock materials).
B. Invoice Receipt (MIRO)
 * Invoice 1,000 EUR + 19% VAT
| Account | Debit | Credit |
|---|---|---|
| GR/IR (WRX) | 1,000 | - |
| Input Tax (MWS) | 190 | - |
| Vendor (AP) | - | 1,190 |
C. Price Variance (PO 1,000 / Inv. 1,050)
 * Invoice higher by 50 EUR + 19% VAT
| Account | Debit | Credit |
|---|---|---|
| GR/IR (WRX) | 1,000 | - |
| Price Diff. (PRD) | 50 | - |

190 | - |
| Vendor (AP) | - | 1,190 |
C. Price Variance (PO 1,000 / Inv. 1,050)
 * Invoice higher by 50 EUR + 19% VAT
| Account | Debit | Credit |
|---|---|---|
| GR/IR (WRX) | 1,000 | - |
| Price Diff. (PRD) | 50 | - |
| Input Tax (MWS) | 199.50 | - |
| Vendor (AP) | - | 1,249.50 |
D. Outgoing Payment (F110)
 * Pay vendor 1,249.50 EUR
| Account | Debit | Credit |
|---|---|---|
| Vendor (AP) | 1,249.50 | - |
| Bank (House Bank) | - | 1,249.50 |
10. RD00 and RD04 – Automatic Postings
RD00 – Master Data
 * Maintains G/L account determination data
 * Replicates to all company codes
 * Update control tables (e.g. T030)
 * Run after master data changes
RD04 – Open Items
 * Automatically posts open items
 * Sales orders (billing doc list)
 * Purchase orders (GR/IR, Invoice)
 * Intercompany postings
 * Proposals can be reviewed before posting
 * Schedule as background job
11. Key Configuration Steps (Summary)
 * Maintain material master and valuation class
 * Maintain vendor master (recon account)
 * Define purchasing org. / group (OME1, OME4)
 * Configure movement types and account grouping (OMJJ, T156SY)
 * Maintain OBYC – automatic account determination (T030)
 * Configure tax procedure and accounts (OBYZ, OB40, FTXP)
 * Define pricing procedure and condition types (OMUM, MPO)

types and account grouping (OMJJ, T156SY)
 * Maintain OBYC – automatic account determination (T030)
 * Configure tax procedure and accounts (OBYZ, OB40, FTXP)
 * Define pricing procedure and condition types (OMUM, MPO)
 * Maintain account assignment settings (OKB9, OKBB)
 * Test end-to-end process (ME21N \rightarrow MIGO \rightarrow MIRO \rightarrow F110)
 * Run RD00/RD04 and reconcile (FBL1N, MBSB, F.01)
12. Reporting & Reconciliation
 * FBL1N – Vendor open items
 * MB5B – Stock overview
 * MIR4 – Invoice verification log
 * MRBR – Purchase order history
 * F.01 – Financial statements (ACDOCA)
 * Material ledger / CO-PA for cost analysis
 * Reconcile GR/IR (WRX) balance
 * Reconcile vendor statements
 * Analyze price variances (PRD)
13. Key Takeaways
 * OBYC and valuation class determine inventory and expense accounts.
 * GR posts inventory and GR/IR; MIRO posts vendor and tax.
 * Discounts, freight and price variances are handled via condition types.
 * Tax determination uses TAXD (OBYZ/OB40) – not VKOA.
 * Account assignment category drives posting logic (stock, expense, asset, etc.).
 * RD00/RD04 enable automatic and mass postings.
 * End-to-end integration ensures accurate, compliant financial reporting.
Footer Notes & Useful SAP T-Codes

category drives posting logic (stock, expense, asset, etc.).
 * RD00/RD04 enable automatic and mass postings.
 * End-to-end integration ensures accurate, compliant financial reporting.
Footer Notes & Useful SAP T-Codes
> Important: G/L accounts, tax codes and configuration may vary by country, company code and business requirements. Always refer to official SAP documentation and consult a qualified SAP consultant.
> 
> Useful SAP T-Codes: ME21N, MIGO, MIRO, F110, OMWD, OMJJ, OBYC, OBYZ, OB40, FTXP, RD00, RD04, FBL1N, F.01
> 
> Tagline: Same Data. Connected Processes. Real Value for Cybex.
>