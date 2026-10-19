# NI01_FICO_Greenfield_Complete_v2-1.pdf

Topic: Germany

🟦 NI01 S/4HANA FICO Greenfield Implementation Book
v2 · Mobile-Fixed · ECC→S/4HANA · New GL · BPQ · 61 Real Table Extracts · DE02 Distribution
Hub
27 CoCodes 18,947 G/Ls 53,089 G/L 10k
ACDOCA
12,819 Assets 10k Billing
T001 GBGR K4 SKA1 COA SKB1 CoCode
WL 5310·DZ 1782·RV
1444
ANLA DE02 VBRK F2 7393
☰
🏢 NI01 — GREENFIELD S/4HANA
↓
🟦 0L IFRS
Leading Ledger
Mandatory
🟩 L1 HGB
Non-Leading
Parallel
🟨 TAX
German Tax
View
↓
ACDOCA — Universal Journal
↓
FI-GL
SKA1·SKB1
FI-AP
LFB1·843v
FI-AR
KNVV·1479c
FI-AA
ANLA·12819
BANK
T012·T012K
↓
0L→IFRS BS
IFRS P&L
L1→HGB BS
HGB P&L
E-Bilanz
↓
FAGL_011PC · 12,431 items
↓
PH00 Company PH01 COA PH02 Ledgers
PH03 G/L PH04 FY PH05 Docs
PH07 Tax PH10 AP PH11 AR
PH12 Assets PH13 Bank PH14 Pay
PH15 CO PH16 SD PH17 MM
PH18 HGB PH19 IFRS PH20 Close
↓
🟢 GO LIVE
📚 SAP Vocabulary — Know These Before Touching Config
Germany · EUR · NIOP · K4 · GBGR Template
10k rows · DE02 · RLDNR = 0L or L1
Financial Statement Structure
Company Code OX02
Legal entity that makes financial statements. NI01 = Germany teaching company.
T001: 27 CoCodes (DE02, GB01, US01, AE09…) all GBGR K4
Chart of Accounts OB13
The LIST of all G/L accounts. One COA → many company codes.
SKA1: 18,947 G/Ls in GBGR. Teaching COA = NIOP.
G/L Account FS00
ONE row inside the COA.

📚 SAP Vocabulary — Know These Before Touching Config — 27 CoCodes (DE02, GB01, US01, AE09…) all GBGR K4
Chart of Accounts OB13
The LIST of all G/L accounts. One COA → many company codes.
SKA1: 18,947 G/Ls in GBGR. Teaching COA = NIOP.
G/L Account FS00
ONE row inside the COA. FS00 maintains it at COA + CoCode level.
SKB1: 53,089 CoCode records. DE02: 1,143 G/Ls maintained.
Ledger FINSC_LEDGER
A COMPLETE accounting view. 0L = IFRS (leading). L1 = HGB (parallel).
ACDOCA RLDNR column = 0L or L1 on every posting line.
ACDOCA SE16N→ACDOCA
Universal Journal. THE central table in S/4HANA. Replaced BSEG+FAGLFLEXA+ANLP+COEP.
DE02: 10k rows. WL 5310 (GI) · DZ 1782 (payment) · RV 1444 (billing)
Subledger FBL1N/FBL5N/AW01N
Detail behind a G/L reconciliation account. AP→LFB1. AR→KNVV. AA→ANLA.
LFB1: 843 vendors · KNVV: 1,479 customers · ANLA: 12,819 assets
Reconciliation Account FS00 → Recon. Acct For
A G/L account that is updated AUTOMATICALLY from subledger. Cannot post directly.
160000 = AP Recon. 120000 = AR Recon. 700000 = Asset APC.
OB53 OB53
Maps P&L account type → Retained Earnings G/L. Used by FAGLGVTR at year-end.
Maps P&L (type X) → 210000 Retained Earnings for NIOP.
FAGLGVTR FAGLGVTR
Year-end carry-forward. Moves P&L net result → Retained Earnings G/L.
Run ONCE per year per ledger. Creates carry-forward document.

OB53 OB53 — R at year-end.
Maps P&L (type X) → 210000 Retained Earnings for NIOP.
FAGLGVTR FAGLGVTR
Year-end carry-forward. Moves P&L net result → Retained Earnings G/L.
Run ONCE per year per ledger. Creates carry-forward document.
Parallel Accounting FINSC_LEDGER
Two ledgers (0L IFRS + L1 HGB) posting in parallel for same transaction.
ACDOCA stores both rows per document. Different values possible.
Document FB03
Proof of business event. Header = BKPF. Lines = ACDOCA (universal).
BKPF: 40k docs. WL 16125 · KR 12286 · AB 9109 · DZ 901.
Posting Period OB52
Month 1-12 + special periods 13-16. OB52 controls open/close.
T001B: period variants. K4: Jan=01, Dec=12, Special: 13-16.
🏗 Master Architecture — One Picture
🆕 New General Ledger — What It Is and Why It Changed
Everything
What is the New General Ledger?
SAP introduced the "New General Ledger" (New GL) with SAP ECC 6.0. S/4HANA ALWAYS uses
New GL — it is mandatory, not optional. Understanding it is critical because it defines how parallel
accounting works.
❌ Classic GL (old ECC)
One GL table: GLT0
Parallel valuation ONLY via Special Purpose
Ledger (FI-SL)
Separate CO tables: COEP, COBK
AR/AP in BSEG (100M+ rows = slow)
Asset Accounting in separate ANLP table
Reconciliation between FI and CO needed
Period-end batch reporting

🆕 New General Ledger — What It Is and Why It Changed — luation ONLY via Special Purpose
Ledger (FI-SL)
Separate CO tables: COEP, COBK
AR/AP in BSEG (100M+ rows = slow)
Asset Accounting in separate ANLP table
Reconciliation between FI and CO needed
Period-end batch reporting
✅ New GL / Universal Journal
(S/4HANA)
ONE table: ACDOCA (Universal Journal)
Parallel accounting = ledgers 0L + L1 (RLDNR
column)
CO fully integrated in ACDOCA (KSTAR,
KOSTL, PRCTR)
BSEG = compatibility view only (reads
ACDOCA)
NI01 · ONE COMPANY · Germany
│
┌────────────┼────────────┐
↓ ↓ ↓
🟦 0L IFRS 🟩 L1 HGB 🟨 TAX
LEADING PARALLEL GERMAN
│
══ ACDOCA ══
Universal Journal
RLDNR=0L / L1
10k rows · DE02
│
┌────┬───────┼───────┬────┐
↓ ↓ ↓ ↓ ↓
FI-GL FI-AP FI-AR FI-AA BANK
SKA1 LFB1 KNVV ANLA T012
│
FINANCIAL STATEMENTS
FAGL_011PC 12,431 items
│
┌─────────┴─────────┐
↓ ↓
0L→IFRS BS L1→HGB BS
IFRS P&L HGB P&L
E-Bilanz
Segment reporting = extra work Asset values INSIDE ACDOCA (no separate
reconciliation)
FI = CO always, no reconciliation needed
Real-time line item reporting
Segment in ACDOCA → instant segment
reporting
New GL Configuration Path
SPRO → Financial Accounting → Financial Accounting
Global Settings → Ledgers → Ledger
Key transactions:
FINSC_LEDGER → Manage Ledgers
FINSC_ACCTG_PRNCPL → Accounting Principles
FAGL_SGEN → Activate New GL for CoCode

IFRS P&L HGB P&L — ath
SPRO → Financial Accounting → Financial Accounting
Global Settings → Ledgers → Ledger
Key transactions:
FINSC_LEDGER → Manage Ledgers
FINSC_ACCTG_PRNCPL → Accounting Principles
FAGL_SGEN → Activate New GL for CoCode
Document Splitting Decision
NEW GL KEY CONCEPTS:
LEDGER = A named accounting view (0L, L1, T1)
Stored in ACDOCA via RLDNR column
Leading ledger = 0L (gets all postings)
Non-leading = L1 (gets parallel postings)
LEDGER GROUP = A named group of ledgers
Posting to ledger group = posts to all
ledgers inside that group simultaneously
e.g. Ledger Group 0L+L1 → both ledgers
ACCOUNTING = The accounting rule assigned to a ledger
PRINCIPLE = 0L → IFRS
L1 → LOCGAAP (HGB)
Used in asset valuation, FX valuation,
provision calculation etc.
EXTENSION = A ledger that INHERITS from another
LEDGER = e.g. T1 Tax inherits 0L, adds tax adj
(Not used if tax = simple adjustments)
DOCUMENT = When you post an invoice:
SPLITTING = SAP can split the accounting line by
profit center / segment automatically
→ enables P&L by segment on Balance Sheet
📊 CEPC extract shows profit centers in your system. FAGL_SGEN would need to be active for
document splitting.
Document splitting adds a SEGMENT / PRCTR dimension to every accounting line item automatically.
Example:

IFRS P&L HGB P&L — et
📊 CEPC extract shows profit centers in your system. FAGL_SGEN would need to be active for
document splitting.
Document splitting adds a SEGMENT / PRCTR dimension to every accounting line item automatically.
Example:
Without splitting: Dr Expense 1000 | Cr Vendor 1000
With splitting: Dr Expense 500 (PC1) + 500 (PC2) | Cr Vendor 500 (PC1) + 500 (PC2)
Requires: Zero-balance clearing account (e.g. 999999) + Splitting rules in FAGL_SGEN
🟨 CUSTOMER DECISION
❓ Does NI01 need document splitting activated?
A — No — single profit center or CO-based reporting sufficient
Simpler setup. No zero-balance clearing account needed. Standard for many rollouts.
B — Yes — Balance Sheet per profit center/segment required
More config. Splitting rules. Zero-balance account. ALL postings must carry profit center.
Owner Decision Date
Finance Lead
⚡ ECC → S/4HANA: Key Differences with Real Examples
These are the most common exam/interview points AND the most common migration surprises. Every
difference below comes from real system behavior.
⚡ Central Accounting Table
ECC (OLD)
BSEG = FI document line items FAGLFLEXT = New GL totals COEP = CO line items ANLP =
Asset line items → Multiple tables, manual reconciliation
S/4HANA (NEW)

🟨 CUSTOMER DECISION — from real system behavior.
⚡ Central Accounting Table
ECC (OLD)
BSEG = FI document line items FAGLFLEXT = New GL totals COEP = CO line items ANLP =
Asset line items → Multiple tables, manual reconciliation
S/4HANA (NEW)
ACDOCA = Universal Journal ONE table for FI + CO + AA Real-time, no reconciliation BSEG =
compatibility view (reads ACDOCA)
→
📋 Real Example: DE02 ACDOCA: 10k rows with WL/DZ/RV/KR all in one table. CO fields (KSTAR,
KOSTL) are on the SAME row as FI fields (RACCT, BUKRS).
🟪 Config Change: No config change needed — ACDOCA is automatic in S/4. But reports referencing
BSEG directly (custom ABAP) must be rewritten to use ACDOCA.
⚡ Material Ledger (ML) / Inventory Valuation
ECC (OLD)
Material Ledger was OPTIONAL Profits not visible at material level GI valuation simple average
cost
S/4HANA (NEW)
Material Ledger is MANDATORY in S/4 Actual costing possible Multi-currency valuation at material
level CKMLRUNVAR for actual cost run
📋 Real Example: T001k (Valuation Area) extract shows 50 valuation areas. In S/4HANA, each valuation
area must have ML active. CKMVFM = material ledger balance.
🟪 Config Change: SPRO → Controlling → Product Cost Controlling → Actual Costing / Material Ledger →
Activate Material Ledger
⚡ Cost Element Accounting
ECC (OLD)

🟨 CUSTOMER DECISION — ea must have ML active. CKMVFM = material ledger balance.
🟪 Config Change: SPRO → Controlling → Product Cost Controlling → Actual Costing / Material Ledger →
Activate Material Ledger
⚡ Cost Element Accounting
ECC (OLD)
KA01 = Create Primary Cost Element Separate object from G/L account KA02 = Change cost
element CEPC → CSKA → CSKB separate maintenance
S/4HANA (NEW)
NO separate cost elements in S/4HANA G/L account IS the cost element FS00 → Cost element
tab replaces KA01 CSKA/CSKB = compatibility views
📋 Real Example: When you create a P&L G/L in FS00 (e.g. 500000 Salaries), it automatically becomes a
cost element. No KA01 needed. KA01/KA02 transactions still exist but create in FS00.
🟪 Config Change: No separate config. FS00 gains a Cost Element tab in S/4. Check: SE16N → CSKA →
verify G/L = cost element (now populated from SKA1).
⚡ Asset Accounting (New Asset Accounting)
→
→
ECC (OLD)
Classic Asset Accounting: Depreciation areas = separate ledger groups ANLP = asset periodic
values ANEP = line items Reconciliation report RAABST02 required Transaction AFBP for posting
S/4HANA (NEW)
New Asset Accounting (S/4): Depreciation areas directly linked to ledgers Asset values IN
ACDOCA (no ANLP primary) Real-time posting per period AFAB runs much faster No
reconciliation report needed

posting
S/4HANA (NEW)
New Asset Accounting (S/4): Depreciation areas directly linked to ledgers Asset values IN
ACDOCA (no ANLP primary) Real-time posting per period AFAB runs much faster No
reconciliation report needed
📋 Real Example: ANLB extract: depreciation areas 01 (IFRS→0L), 15 (HGB→L1). In S/4, AFAB posts
depreciation directly to ACDOCA with RLDNR = 0L (area 01) and RLDNR = L1 (area 15). Both visible realtime.
🟪 Config Change: SPRO → Asset Accounting → Valuation → Depreciation Areas → Define How
Depreciation Areas Post to General Ledger → Area 01 = Leading Ledger 0L, Area 15 = L1
⚡ Controlling Real-Time Integration
ECC (OLD)
FI-CO reconciliation ledger Batch jobs to reconcile FI with CO KALK = Reconciliation Ledger
Period-end reconciliation required
S/4HANA (NEW)
NO reconciliation ledger FI = CO always (same ACDOCA) CO posting = FI posting (same
document) No period-end reconciliation needed
📋 Real Example: ACDOCA row for expense invoice: RACCT=500000 (FI G/L) AND KSTAR=500000 (CO
cost element) on same row. KOSTL=ADMIN_CC. BUKRS=NI01. ONE row = FI + CO.
🟪 Config Change: No config change — automatic. But check: OKB9 (default account assignment) still
needed for accounts that need automatic cost center assignment.
⚡ BSEG Table Performance
ECC (OLD)

🟪 Config Change: SPRO → Asset Accounting → Valuation → Depreciation Areas → Define How — 1. ONE row = FI + CO.
🟪 Config Change: No config change — automatic. But check: OKB9 (default account assignment) still
needed for accounts that need automatic cost center assignment.
⚡ BSEG Table Performance
ECC (OLD)
BSEG = PRIMARY FI line item table With 100M+ rows: very slow FBL1N, FBL5N, FAGLL03 all hit
BSEG Custom reports using BSEG common
→
→
→
S/4HANA (NEW)
BSEG = COMPATIBILITY VIEW only Actual data in ACDOCA BSEG SELECTs auto-redirect to
ACDOCA FBL1N/FBL5N/FAGLL03H → ACDOCA directly Massive performance improvement
📋 Real Example: Run FAGLL03H in S/4 → instantly shows 10k DE02 rows from ACDOCA. Same as
FAGLL03 in ECC but 10x faster because ACDOCA is column-store in HANA DB.
🟪 Config Change: Custom ABAP must be reviewed: SELECT FROM BSEG... works via compatibility but
may be slow. Rewrite to SELECT FROM ACDOCA for performance. SAP Note 2217940.
⚡ Bank Account Management
ECC (OLD)
Bank accounts: BANK master + FI12 House Bank (T012) + Account ID (T012K) Separate bank
communication config MT940 bank statement most common
S/4HANA (NEW)
S/4HANA Bank Account Management (BAM): Central bank account repository (FCLM_BAM)
Enhanced signatory management Central payment (hub-based payment) Still uses T012/T012K
(compatible) CAMT.053 ISO standard preferred

📋 Real Example: Run FAGLL03H in S/4 → instantly shows 10k DE02 rows from ACDOCA. Same as — NEW)
S/4HANA Bank Account Management (BAM): Central bank account repository (FCLM_BAM)
Enhanced signatory management Central payment (hub-based payment) Still uses T012/T012K
(compatible) CAMT.053 ISO standard preferred
📋 Real Example: T012 and T012K extracts still valid in S/4. FEBKO/FEBEP bank statement tables still
used. Enhancement: FCLM_BAM provides better bank account governance for treasury teams.
🟪 Config Change: For basic S/4 implementation: FIBL FI12 (same as ECC). For advanced treasury:
activate FCLM_BAM via SPRO → Bank Account Management.
⚡ Vendor / Customer Master
ECC (OLD)
Vendor master: LFB1 + LFA1 (FK01) Customer master: KNB1 + KNA1 (XD01) Separate business
partner for CRM
S/4HANA (NEW)
BUSINESS PARTNER (BP) is MANDATORY Vendor = BP role FLVN01 Customer = BP role
FLCU01 MDG-BP if Master Data Governance LFB1/KNB1 populated from BP
📋 Real Example: LFB1 extract: 843 vendors. In S/4, these vendors MUST have a Business Partner
created. FK01 still works but creates via BP internally. SE16N → BUT000 = BP master.
→
→
🟪 Config Change: SPRO → Cross-Application Components → SAP Business Partner → Business Partner
Integration with Vendor. Run report PREC_BP_CHECK to validate BP consistency.
PH00 — Company Blueprint
NI01 Teaching Company
Field NI01 (Teaching) Real (DE02)

🟪 Config Change: SPRO → Cross-Appl — ication Components → SAP Business Partner → Business Partner
Integration with Vendor. Run report PREC_BP_CHECK to validate BP consistency.
PH00 — Company Blueprint
NI01 Teaching Company
Field NI01 (Teaching) Real (DE02)
Company Code NI01 DE02
Company Name NI01 GmbH CTP GmbH & Co KG
Country DE DE
Currency EUR EUR
COA NIOP GBGR
FY Variant K4 K4
Ledgers 0L + L1 0L + L1
Tax Procedure TAXD TAXD
Ctrl Area NI01 GBGR
Teaching values — replace with customer values at go-live
T001 — Your 27 Company Codes
📊 T001 extract: 27 CoCodes, all GBGR COA, K4 FY variant
CoCode Country Currency Note
DE02 DE EUR CTP Distribution Hub
DE01 DE EUR Cybex GmbH
GB01 GB GBP Cybex UK
US01 US USD Cybex USA
FR01 FR EUR Cybex France
AE09 AE AED IMEA Retail DTC
NI01 DE EUR Teaching CoCode
🟪 CONFIG CC01 — Create Company Code OX02
① WHAT IS IT?
Legal entity in SAP. Every FI document belongs to exactly one company code.
② WHY?
No company code = no accounting. First mandatory greenfield step.
③ WHERE?
SPRO → Enterprise Structure → Definition
→ Financial Accounting → Edit Company Code
T-code: OX02
④ ENTER:
Field Value
Company Code NI01
Company Name NI01 GmbH
City Bayreuth
Country DE
Currency EUR
Language DE
⑤ SAP CREATES:
NI01 entry in T001 table.
⑥ TEST:
SE16N → T001 → BUKRS = NI01
⑦ EXPECT:

🟪 CONFIG CC01 — Create Company Code OX02 — ny Code
T-code: OX02
④ ENTER:
Field Value
Company Code NI01
Company Name NI01 GmbH
City Bayreuth
Country DE
Currency EUR
Language DE
⑤ SAP CREATES:
NI01 entry in T001 table.
⑥ TEST:
SE16N → T001 → BUKRS = NI01
⑦ EXPECT:
BUKRS=NI01, LAND1=DE, WAERS=EUR, SPRAS=DE all visible
⑧ LANDS IN:
T001 → G/L accounts (FS00) → ACDOCA
🟥 MISTAKE:
Copying DE02 without cleaning dependent config. Wrong currency — cannot change after first
posting.
🟢 PASS:
SE16N → T001 → NI01 exists · OB62 assigns NIOP COA · OB37 assigns K4 FY variant
PH01 — Chart of Accounts
📊 REAL DATA: SKA1: 18,947 G/Ls in GBGR. SKB1: 53,089 CoCode-level masters. DE02 actively uses
1,143 G/Ls.
PH02 — Ledger Architecture (0L IFRS + L1 HGB)
NIOP — Teaching COA (GBGR: 18,947 G/Ls)
ASSETS (0xxxxx):
100000 Main Bank (OI:No)
100010 Bank Clearing (OI:YES)
120000 AR Recon (Customers)
150000 GR/IR Clearing (OI:YES)
700000 APC – Machinery (AA Recon)
750000 Accum Depr (AA contra)
LIABILITIES (1xxxxx):
154310 Input VAT 19% (Tax:-)
160000 AP Recon (Vendors)
175000 Output VAT 19% (Tax:+)
162000 Lease Liability IFRS16
EQUITY (2xxxxx):
210000 Retained Earnings ← OB53
REVENUE (3xxxxx):
300000 Revenue Products (Tax:+)
COGS/EXPENSE (4-5xxxxx):
410000 Raw Materials (Tax:-)
500000 Personnel Expense
600000 Depreciation
FINANCIAL (6xxxxx):

162000 Lease Liability IFRS1 — 6
EQUITY (2xxxxx):
210000 Retained Earnings ← OB53
REVENUE (3xxxxx):
300000 Revenue Products (Tax:+)
COGS/EXPENSE (4-5xxxxx):
410000 Raw Materials (Tax:-)
500000 Personnel Expense
600000 Depreciation
FINANCIAL (6xxxxx):
640000 FX Gain / Loss
🟦 0L — IFRS Leading Ledger
Property Value
Accounting Principle IFRS
Ledger Type Standard (Online)
Leading? YES — mandatory, always receives all postings
FX Valuation IAS 21 — revalue to closing rate
Depreciation IAS 16 — useful life = economic life
Provisions IAS 37 — best estimate
Revenue IFRS 15 — performance obligation
Reporting Group IFRS financial statements
vs
🟩 L1 — HGB Non-Leading Ledger
Property Value
Accounting Principle LOCGAAP (HGB)
PARALLEL LEDGERS — Vendor Invoice €1,000+VAT
SAP creates ONE document
BKPF: BUKRS=NI01, BELNR=190000001
│
ACDOCA gets MULTIPLE ROWS:
│
┌─────┴─────┐
↓ ↓
RLDNR=0L RLDNR=L1
IFRS HGB
Dr Exp 1000 Dr Exp 1000 ← same
Dr VAT 190 Dr VAT 190 ← same
Cr Vend1190 Cr Vend1190 ← same
THEY DIFFER FOR:
• Depreciation: Area 01→0L / Area 15→L1
• Provisions: 0L best est | L1 §249 strict
• Impairment: 0L IAS36 | L1 §253 permanent
• FX: 0L IAS21 | L1 §256a HGB
Ledger Type Standard
Leading? NO — parallel to 0L
FX Valuation § 256a HGB — only if lower
Depreciation § 253 HGB — often higher/faster

IFRS HGB — §249 strict
• Impairment: 0L IAS36 | L1 §253 permanent
• FX: 0L IAS21 | L1 §256a HGB
Ledger Type Standard
Leading? NO — parallel to 0L
FX Valuation § 256a HGB — only if lower
Depreciation § 253 HGB — often higher/faster
Provisions § 249 HGB — strict obligation required
Revenue Realization principle
Reporting German statutory + E-Bilanz
🟨 CUSTOMER DECISION
❓ Does NI01 need a separate tax ledger (T1)?
A — No tax ledger — handle via tax areas / deferred tax manual journals
Simpler. Good when tax differences are small or handled externally.
B — Tax ledger T1 — extension ledger inheriting from 0L with tax adjustments
Justified when: complex deferred tax, multiple tax jurisdictions, or tax reporting team needs separate view.
Owner Decision Date
Finance Lead
PH03 — G/L Master
FS00 — Critical Fields Explained
🔍 TROUBLESHOOT: G/L Account Cannot Be Posted To
Reconciliation account?
Recon accounts block direct posting. Use subledger (FB60/MIRO/F-28) or confirm 'recon account for' is wrong.
↓
Period open?
OB52 → check period 01-12 open for document type in NI01
↓
Field status blocking?
FS00 → CoCode view → Field Status Group → check required fields
↓
Account not extended to CoCode?
FS00 → BUKRS = NI01 → CoCode tab may be empty → create CoCode view
↓
Tax category mismatch?

🔍 TROUBLESHOOT: G/L Account Cannot Be Posted To — NI01
↓
Field status blocking?
FS00 → CoCode view → Field Status Group → check required fields
↓
Account not extended to CoCode?
FS00 → BUKRS = NI01 → CoCode tab may be empty → create CoCode view
↓
Tax category mismatch?
Posting with tax code but G/L has no tax category in FS00 → message FF868
FS00 → Account 160000 → NI01
COA VIEW (SKA1):
Account Group: PAYB
Account Type: Liabilities
P&L/BS: Balance Sheet
Recon Acct: Creditors ← !!
Short text: AP Recon
COCODE VIEW (SKB1):
Sort Key: 031
Line Item Disp: ✓
Open Item Mgmt: ✗ (recon — NO)
Tax Category: (blank)
Field Status: G067
WHY OPEN ITEM = NO on recon account?
→ Managed via subledger (FBL1N)
→ Bank clearing 100010: OI = YES
→ GR/IR 150000: OI = YES
PH04 — Fiscal Year & Posting Periods
T009 — K4 Fiscal Year Variant
📊 REAL DATA: T009 extract confirms K4 = calendar year. All 27 CoCodes use K4.
OB52 — Posting Period Control
📊 REAL DATA: T001B extract: Posting period variant with account type controls.
PH05 — Document Types & Posting Keys
T003 Document Types (51 in your system)
📊 REAL DATA: T003 extract: 51 doc types. BKPF counts: WL 16125 · KR 12286 · AB 9109 · DZ 901 ·
RV 301
Type Name Account Type Debit/Credit to
KR Vendor Invoice K Creditor
K4 Fiscal Year (Calendar Year):
Jan=01 Feb=02 Mar=03
Apr=04 May=05 Jun=06

📊 REAL DATA: T003 extrac — t: 51 doc types. BKPF counts: WL 16125 · KR 12286 · AB 9109 · DZ 901 ·
RV 301
Type Name Account Type Debit/Credit to
KR Vendor Invoice K Creditor
K4 Fiscal Year (Calendar Year):
Jan=01 Feb=02 Mar=03
Apr=04 May=05 Jun=06
Jul=07 Aug=08 Sep=09
Oct=10 Nov=11 Dec=12
Special: 13,14,15,16 (audit only)
OB52 Posting Periods:
Acct From To Year
+ 01 12 2026 ← All
A 01 12 2026
D 01 12 2026
K 01 12 2026
S 01 12 2026
Month-end: close → set From = next
Audit: open special period 13
KZ Vendor Payment K Creditor
RE GR Invoice (MIRO) K Creditor
AB Asset Posting A Asset
WL Goods Issue STO/Delivery M Material
WA Goods Issue standard M Material
SA G/L Posting G G/L accts
DR Customer Invoice D Debtor
DZ Customer Payment D Debtor
RV Billing → FI V SD billing
TBSL Posting Keys
📊 REAL DATA: TBSL extract: posting key definitions. Key rule: 40=GL debit, 50=GL credit. 31=vendor
credit, 25=vendor debit.
Key Name Acct Type Dr/Cr
01 Cust Invoice debit D Dr
11 Cust Credit Memo D Cr
15 Incoming Payment D Cr
25 Outgoing Payment K Cr
31 Vendor Invoice K Cr
40 G/L Debit S Dr
50 G/L Credit S Cr
70 Asset APC Debit A Dr
75 Asset Credit A Cr
PH06 — Retained Earnings
🟪 CONFIG RE01 — OB53 — Retained Earnings Account
① WHAT IS IT?
Maps P&L account type → retained earnings G/L for year-end carry-forward.
② WHY?

50 G/L Credit — S Cr
70 Asset APC Debit A Dr
75 Asset Credit A Cr
PH06 — Retained Earnings
🟪 CONFIG RE01 — OB53 — Retained Earnings Account
① WHAT IS IT?
Maps P&L account type → retained earnings G/L for year-end carry-forward.
② WHY?
Without OB53, FAGLGVTR cannot carry the P&L result to the Balance Sheet.
③ WHERE?
T-code: OB53
(or SPRO → FI → GL → Business Transactions
→ Annual Closing → Carry Forward
→ Define Retained Earnings Account)
④ ENTER:
Field Value
Chart of Accounts NIOP
P&L Account Type X
Retained Earnings G/L 210000
⑤ SAP CREATES:
T030B entry: KTOPL=NIOP, XBILK=X, SAKO=210000
⑥ TEST:
RETAINED EARNINGS — HOW IT WORKS
During Year:
Revenue 300000: Credit entries accumulate
Expense 500000: Debit entries accumulate
Expense 600000: Debit entries accumulate
P&L net: Revenue − Expenses = Net Profit/Loss
(shown in Trial Balance P&L section)
Year-End: FAGLGVTR (Carry Forward transaction)
↓
P&L accounts → ZEROED (carry-forward zeroes them)
↓
210000 Retained Earnings ← receives the NET result
(Balance Sheet equity section)
OB53 tells SAP: P&L account type X → G/L 210000
For 0L (IFRS): ACDOCA RLDNR=0L → 210000 IFRS retained earnings
For L1 (HGB): ACDOCA RLDNR=L1 → 210000 HGB retained earnings
SAME G/L NUMBER but DIFFERENT LEDGER ROWS → different balances

210000 Retained Earnings ← receives the NET result — P&L account type X → G/L 210000
For 0L (IFRS): ACDOCA RLDNR=0L → 210000 IFRS retained earnings
For L1 (HGB): ACDOCA RLDNR=L1 → 210000 HGB retained earnings
SAME G/L NUMBER but DIFFERENT LEDGER ROWS → different balances
Post revenue + expense → run FAGLGVTR → check 210000
⑦ EXPECT:
210000 balance = prior year P&L net. 0L and L1 may differ.
⑧ LANDS IN:
P&L → FAGLGVTR → 210000 → Balance Sheet Equity
🟥 MISTAKE:
G/L 210000 flagged as P&L type instead of Balance Sheet. FAGLGVTR fails.
🟢 PASS:
FAGLGVTR completes · 210000 has balance in ACDOCA for 0L and L1 · F.01 shows balance
PH07 — Tax Architecture
Input VAT
Purchase tax paid to vendor
Codes: V1 (19%) V7 (7%) V0 (0%)
GERMAN TAX ARCHITECTURE — NI01
BUSINESS EVENT
│
┌────────────┼────────────┐
↓ ↓ ↓
INPUT TAX OUTPUT TAX WITHHOLDING
(Purchases) (Sales) TAX
│ │ │
FTXP FTXP WHT
V1 = 19% A1 = 19% Config
V7 = 7% A7 = 7%
V0 = 0% A0 = 0%
│ │
T030k T030k
VST → 154310 MWS → 175000
│ │
ACDOCA line ACDOCA line
(Tax amt) (Tax amt)
│
BSET (tax doc line items)
│
VAT RETURN / EC Sales List
Law: § 15 UStG
G/L: 154310 / 154370
Output VAT
Sales tax charged to customer
Codes: A1 (19%) A7 (7%) A0 (0%)
Law: § 13 UStG
G/L: 175000 / 175700
Zero Rate
EU intra-community / Export
Codes: V0, A0 IG = EU acquisition
Law: § 4 UStG
G/L: No VAT G/L
Reverse Charge

FTXP FTXP WHT — VAT
Sales tax charged to customer
Codes: A1 (19%) A7 (7%) A0 (0%)
Law: § 13 UStG
G/L: 175000 / 175700
Zero Rate
EU intra-community / Export
Codes: V0, A0 IG = EU acquisition
Law: § 4 UStG
G/L: No VAT G/L
Reverse Charge
B2B EU services § 13b
Codes: IG, IL special codes
Law: § 13b UStG
G/L: 154800 / 175800
Withholding Tax
Source deduction on payments
Codes: W1
Law: § 50a EStG
G/L: 175900
Non-Deductible
VAT that cannot be reclaimed
Codes: NV codes
Law: § 15 (1a) UStG
G/L: To expense G/L
📊 REAL DATA: T007a: German tax keys. T007S: Tax codes with rates. T030k: Tax account determination.
BSET: Tax document line items per posting.
PH08 — Tax Codes (FTXP)
🟪 CONFIG TX01 — Tax Code V1 — Input VAT 19%
① WHAT IS IT?
Tax code that applies 19% German input VAT to vendor invoices/purchase orders.
② WHY?
Without V1, vendor invoice cannot carry VAT → wrong financial statements + illegal VAT return.
③ WHERE?
T-code: FTXP
Country: DE
Procedure: TAXD
Tax Code: V1
④ ENTER:
Field Value
Country DE
Tax Code V1
Description Input VAT 19%
Tax Type V (Input)
Tax Procedure TAXD
Percentage MWVSA 19.00
Account Key VST
Non-Deductible 0.00
⑤ SAP CREATES:
T007S entry for V1. Tax condition in TAXD procedure.
⑥ TEST:
FB60 → Vendor 1000001 → Amount 1000 → Tax Code V1
⑦ EXPECT:

🟪 CONFIG TX01 — Tax Code V1 — Input VAT 19% — nput)
Tax Procedure TAXD
Percentage MWVSA 19.00
Account Key VST
Non-Deductible 0.00
⑤ SAP CREATES:
T007S entry for V1. Tax condition in TAXD procedure.
⑥ TEST:
FB60 → Vendor 1000001 → Amount 1000 → Tax Code V1
⑦ EXPECT:
Dr Expense 1000 | Dr Input VAT 154310 → 190 | Cr Vendor 1190
⑧ LANDS IN:
BSET (tax lines) → ACDOCA → 0L+L1 → BS (VAT asset)
🟥 MISTAKE:
Tax procedure TAXD not assigned to country DE (OBBG). Input/output tax type mixed.
🟢 PASS:
BSET has MWSKZ=V1 · Tax amount = 190 · G/L 154310 posted · Vendor = 1190
🟧 TEST 01 — Vendor invoice €1,000 net + VAT 19%
Transaction: FB60 or MIRO
Dr 410000 Expense / Raw Materials 1,000.00
Dr 154310 Input VAT 19% 190.00
Cr 160000 Vendor (AP Recon) 1,190.00
G/L Accounts: 410000 (Expense), 154310 (Input VAT), 160000 (Vendor Recon)
Ledger: 0L IFRS + L1 HGB
Amount: Net €1,000 | VAT €190 | Gross €1,190
BS/P&L: P&L: Expense +1,000 | BS: Vendor liability +1,190, VAT recoverable +190
🟢 PASS: BSET MWSKZ=V1 · FBL1N vendor balance = 1,190 · ACDOCA 3 lines
PH09 — Automatic Account Determination
Key Determination Objects
Object Used For Key Field
T030 / OBYC MM→FI: GR, GI, invoice, GR/IR Valuation class + account modifier
T030k Tax→FI: VST/MWS → G/L Account key from tax procedure

🟢 PASS: BSET MWSKZ=V1 · FBL1N vendor balance = 1,190 · ACDOCA 3 lines — Automatic Account Determination
Key Determination Objects
Object Used For Key Field
T030 / OBYC MM→FI: GR, GI, invoice, GR/IR Valuation class + account modifier
T030k Tax→FI: VST/MWS → G/L Account key from tax procedure
AO90 Asset→FI: APC, Depr, Gain/Loss Asset class + account determination key
VKOA SD→FI: billing → revenue Account assignment group + condition type
T042I Payment program → bank G/L Payment method + house bank → G/L
OBA1 FX differences → G/L Currency + realized/unrealized gain/loss G/L
📊 REAL DATA: T030 extract: GBGR COA. BSX=inventory G/L, WRX=GR/IR clearing, PRD=price
difference. T030k: VST→154310, MWS→175000.
GR/IR Clearing — Full Explanation
PO Created (ME21N): no accounting
↓
Goods Receipt (MIGO): Dr Inventory | Cr GR/IR
150000
↓
Invoice Receipt (MIRO): Dr GR/IR 150000 | Cr
Vendor 160000
↓
GR/IR 150000 → nets to zero if PO price = invoice
price
↓
Price difference → OBYC PRD → Dr/Cr Price
Variance (P&L)
↓
MR11 = manual GR/IR clearing for old open items
PH10 — Accounts Payable
LFB1 — Vendor Master (843 DE02)
📊 REAL DATA: LFB1 extract: 843 vendors in DE02. LFC1: vendor balance summary. MISSING
DUPCHECK file: vendors without REPRF flag.
Field Description NI01 Value
LIFNR Vendor Number Key field
BUKRS Company Code NI01

📊 REAL DATA: T030 extract: GBGR COA. BSX=inventory G/L, WRX=GR/IR clearing, PRD=price — DE02)
📊 REAL DATA: LFB1 extract: 843 vendors in DE02. LFC1: vendor balance summary. MISSING
DUPCHECK file: vendors without REPRF flag.
Field Description NI01 Value
LIFNR Vendor Number Key field
BUKRS Company Code NI01
AKONT Reconciliation Account 160000 ← CRITICAL
ZTERM Payment Terms 0030 = 30 days net
ZWELS Payment Methods T = bank transfer
REPRF Duplicate Invoice Check ✓ MUST BE SET
ZAHLS Payment Block Blank = not blocked
AP FULL CYCLE — NI01
PURCHASE ORDER (ME21N)
│ no accounting
↓
GOODS RECEIPT (MIGO — WE doc type)
Dr Inventory / Expense OBYC BSX
Cr GR/IR Clearing 150000 OBYC WRX
│
↓
VENDOR INVOICE (MIRO — RE doc type)
Dr GR/IR Clearing 150000
Dr Input VAT 154310 T030k VST
Cr Vendor Recon 160000 LFB1.AKONT
│
↓
PAYMENT RUN (F110 — KZ doc type)
Dr Vendor Recon 160000
Cr Bank Clearing 100010 T042I
│
↓
BANK STATEMENT (FEBAN)
Dr Main Bank 100000 T012K G/L
Cr Bank Clearing 100010
│
↓
VENDOR ACCOUNT CLEARED (FBL1N = zero)
Payment Terms (ZTERM)
Code Description Due Discount
0001 Payable immediately 0 days -
0014 14 days 2% cash discount 14 days 2%
0030 30 days net 30 days -
SOFO Sofort fällig (German) 0 days -
Cash discount in Germany: OBB8 config. Discount G/L: FBKP → account determination for discount.
🔍 TROUBLESHOOT: Vendor Invoice Not Cleared After Payment

0014 14 days 2% cash discount 14 days 2 — %
0030 30 days net 30 days -
SOFO Sofort fällig (German) 0 days -
Cash discount in Germany: OBB8 config. Discount G/L: FBKP → account determination for discount.
🔍 TROUBLESHOOT: Vendor Invoice Not Cleared After Payment
Check vendor has the invoice open
FBL1N → vendor → Status: Open items only → see invoice
↓
Check payment run selected it
F110 → proposal log → was vendor / invoice selected?
↓
Check payment block
LFB1 → ZAHLS → payment block set? Or header block on invoice FB03
↓
Check payment method on invoice
Invoice must have same payment method as FBZP config
↓
Bank statement arrived?
FEBAN → imported statement → was clearing doc created?
↓
ACDOCA after clearing
SE16N → ACDOCA → AUGDT (clearing date) should be populated
PH11 — Accounts Receivable
📊 REAL DATA: KNVV: 1,479 customer-sales-area records. VBRK: 10k billing docs, F2=7393 (74%). VBFA:
40k document flow records.
PH12 — Asset Accounting (FI-AA)
AR FULL CYCLE — NI01
SALES ORDER (VA01 — TVAK Z010)
│ no accounting
↓
DELIVERY + GOODS ISSUE (VL01N)
Dr COGS 410000 OBYC GBB/VAX
Cr Inventory OBYC BSX
│
↓
BILLING (VF01 — billing type F2)
Dr Customer Recon 120000 KNVV.AKONT
Cr Revenue 300000 VKOA
Cr Output VAT 175000 T030k MWS
│
↓
BANK RECEIPT (CAMT.053 → FEBAN)
│
↓
CLEAR CUSTOMER (F-28 or auto via FEBAN)
Dr Main Bank 100000

🔍 TROUBLESHOOT: Vendor Invoice Not Cleared After Payment — LING (VF01 — billing type F2)
Dr Customer Recon 120000 KNVV.AKONT
Cr Revenue 300000 VKOA
Cr Output VAT 175000 T030k MWS
│
↓
BANK RECEIPT (CAMT.053 → FEBAN)
│
↓
CLEAR CUSTOMER (F-28 or auto via FEBAN)
Dr Main Bank 100000
Cr Customer Recon 120000 ← CLEARED
PAYMENT OPTIONS:
Full: Clear entire invoice
Partial: Partial payment — open item remains
Residual: New residual open item created
On-Account: No invoice matched — sits on account
ANKA Asset Classes (your extract)
📊 REAL DATA: ANKA extract: Asset class definitions. ANLB: depreciation terms per class and area.
Class Description Acct Det Useful Life
1000 Machinery & Equipment AD1000 5y IFRS / 6y HGB
1100 Office Equipment AD1100 3y IFRS / 3y HGB
1200 Vehicles AD1200 4y IFRS / 5y HGB
1300 Buildings AD1300 25y IFRS / 33y HGB
ASSET LIFECYCLE — NI01 (New Asset Accounting in S/4)
ASSET REQUIREMENT
│
↓
ASSET CLASS (ANKA) ← Class 1000 = Machinery
│
↓
AS01 → ASSET MASTER (ANLA) ← 12,819 assets in DE02
Description | Class | CoCode | Useful life | Dep area
│
↓
AO90 ACCOUNT DETERMINATION
APC G/L: 700000
Accum Depr: 750000
Depr Expense: 600000
Gain on Sale: 640010
Loss on Sale: 640020
│
↓
ACQUISITION (MIRO or F-90)
Dr APC 700000 60,000
Cr Vendor 160000 60,000
│
↓
DEPRECIATION (AFAB — monthly)
0L IFRS L1 HGB
Area 01 Area 15

AO90 ACCOUNT DETERMINATION — um Depr: 750000
Depr Expense: 600000
Gain on Sale: 640010
Loss on Sale: 640020
│
↓
ACQUISITION (MIRO or F-90)
Dr APC 700000 60,000
Cr Vendor 160000 60,000
│
↓
DEPRECIATION (AFAB — monthly)
0L IFRS L1 HGB
Area 01 Area 15
Dr Depr Exp 600000 1,000.00 833.33
Cr Accum Depr 750000 1,000.00 833.33
│
↓
BOTH IN ACDOCA:
RLDNR=0L → Depr 1,000 → NBV 59,000
RLDNR=L1 → Depr 833 → NBV 59,167
2000 Intangibles AD2000 3-5y IFRS / 5y HGB
3000 Assets Under Construction AD3000 No depr until complete
4000 Low Value Assets GWG AD4000 Immediate write-off DE
Depreciation Areas (ANLB extract)
📊 REAL DATA: ANLB: Depreciation terms per asset and area. Area 01 = IFRS, Area 15 = HGB.
Area Type Ledger Method Useful Life
01 Book (IFRS) 0L Leading LINR SL 5y / economic life
15 Tax/HGB L1 Non-leading DG Degressive or LINR 6y / HGB max
20 Cost Accounting Internal only Same as 01 CO purposes
30 Investment Support Special Custom If applicable
🟧 TEST 03 — Machine purchase €60,000 + AFAB depreciation month 1
Transaction: AS01 → MIRO → AFAB
ACQUISITION (F-90 or MIRO):
Dr 700000 APC – Machinery 60,000.00
Dr 154310 Input VAT 19% 11,400.00
Cr 160000 Vendor 71,400.00
DEPRECIATION MONTH 1 — 0L IFRS (5yr SL):
Dr 600000 Depreciation Expense 1,000.00
Cr 750000 Accum Depreciation 1,000.00

🟧 TEST 03 — Machine purchase €60,000 + AFAB depreciation month 1 — O):
Dr 700000 APC – Machinery 60,000.00
Dr 154310 Input VAT 19% 11,400.00
Cr 160000 Vendor 71,400.00
DEPRECIATION MONTH 1 — 0L IFRS (5yr SL):
Dr 600000 Depreciation Expense 1,000.00
Cr 750000 Accum Depreciation 1,000.00
DEPRECIATION MONTH 1 — L1 HGB (6yr SL):
Dr 600000 Depreciation Expense 833.33
Cr 750000 Accum Depreciation 833.33
G/L Accounts: 700000 (APC), 750000 (Accum Depr), 600000 (Depr Expense), 154310 (VAT)
Ledger: 0L IFRS: Area 01 | L1 HGB: Area 15
Amount: Acquisition: €60,000 | Monthly depr: €1,000 (0L) vs €833 (L1)
BS/P&L: BS: APC 60,000 − Accum Depr 1,000 = NBV 59,000 (0L) | P&L: Depr 1,000
🟢 PASS: ANLA master exists · AO90 correct · AFAB runs clean · ACDOCA both 0L and L1
depr rows · AW01N shows both areas
PH13 — Bank / Treasury
🟥 Bank Clearing — Correcting the #1 Beginner Mistake
BANK ARCHITECTURE — NI01
PHYSICAL BANK (Deutsche Bank, Commerzbank...)
│
↓
HOUSE BANK (T012)
HBKID = DEBA
Bank Country: DE
Bank Key: BLZ (e.g. 37040044)
│
↓
BANK ACCOUNT (T012K)
HKTID = MAIN
G/L = 100000 (Main Bank) ← OT account
G/L = 100010 (Clearing) ← OI account
│
↓
BANK STATEMENT (CAMT.053 or MT940)
│
FEBKO (header) + FEBEP (line items)
│
↓
EBS PROCESSING CONFIG:
Account Symbol → G/L account
Posting Rule → Dr/Cr logic
External Transaction Type → Bank's code

🟥 Bank Clearing — Correcting the #1 Beginner Mistake — aring) ← OI account
│
↓
BANK STATEMENT (CAMT.053 or MT940)
│
FEBKO (header) + FEBEP (line items)
│
↓
EBS PROCESSING CONFIG:
Account Symbol → G/L account
Posting Rule → Dr/Cr logic
External Transaction Type → Bank's code
Interpretation Algorithm → matching logic
Search Strategy → which open items to find
│
┌──────┴──────┐
↓ ↓
INCOMING OUTGOING
Cust clears Vendor clears
Dr Bank 100000 Dr Vendor 160000
Cr Cust 120000 Cr Bank 100000
📊 REAL DATA: FEBKO (bank statement headers) and FEBEP (EBS line items) extracts show real bank
statement processing in DE02. T012 and T012K extracts confirm house bank and account ID setup.
PH14 — Payment Program (F110 / FBZP)
FBZP — 5 Configuration Screens
📊 REAL DATA: FBZP All company codes, FBZP Paying company codes, FBZP Bank determination,
FBZP Payment method country, Payment method in company code — all 5 extracts in your GitHub.
WRONG: "Bank clearing = Asset (money came in)"
CORRECT:
Bank Clearing 100010 = TEMPORARY
Holds value for hours/1 day only
Outgoing payment example:
Step 1 (F110 runs):
Dr Vendor 160000 100,000
Cr Clear 100010 100,000
→ 100010 = CREDIT (interim)
Step 2 (Bank statement FEBAN):
Dr Clear 100010 100,000
Cr Bank 100000 100,000
→ 100010 = ZERO ✓
NOT an asset. NOT a liability.
= TIMING between F110 and statement.

📊 REAL DATA: FBZP All company codes, FBZP Paying company codes, FBZP Bank determination, — 000
Cr Clear 100010 100,000
→ 100010 = CREDIT (interim)
Step 2 (Bank statement FEBAN):
Dr Clear 100010 100,000
Cr Bank 100000 100,000
→ 100010 = ZERO ✓
NOT an asset. NOT a liability.
= TIMING between F110 and statement.
Month-end balance → statement missing
T042Z — Payment Methods
📊 REAL DATA: Payment method T042Z.xlsx + T042z 1409 full extract.xlsx
Method Name Country Use Format
T Wire Transfer DE EUR domestic SEPA pain.001
Z Foreign Transfer DE Foreign currency SWIFT MT103
U Direct Debit DE B2B debit SEPA pain.008
S Check DE Manual checks Local
📊 REAL DATA: T042I (account determination): maps payment method + house bank → posting G/L.
Key link between FBZP and G/L accounts.
F110 — Full Payment Run Sequence
↓
Create run: F110 → Date + ID + CoCode NI01 + Doc
type KZ
↓
FBZP Screen 1: All Company Codes
NI01 → Sending CoCode ✓
FBZP Screen 2: Paying Company Codes
NI01 → Outgoing pmts allowed
Min: €0.01 Max: unlimited
FBZP Screen 3: Payment Methods Country
DE → T (wire/SEPA credit transfer)
Format: pain.001 (SEPA)
Required fields: IBAN, BIC
FBZP Screen 4: Payment Methods Company Code
NI01 → T → Min €1 / Max €999,999
House bank: DEBA
FBZP Screen 5: Bank Determination
NI01 → Ranking: DEBA MAIN EUR
→ Account 100000 (cleared via 100010)
Parameters: Vendor type K, Method T, House bank

📊 REAL DATA: Payment method T042Z.xlsx + T042z 1409 full extract.xlsx — ethods Company Code
NI01 → T → Min €1 / Max €999,999
House bank: DEBA
FBZP Screen 5: Bank Determination
NI01 → Ranking: DEBA MAIN EUR
→ Account 100000 (cleared via 100010)
Parameters: Vendor type K, Method T, House bank
DEBA
↓
Proposal (FKOPF): SAP selects all due invoices
↓
Review proposal: edit vendors if needed
↓
Execute payment: KZ doc → Dr Vendor 160000 | Cr
Bank Clearing 100010
↓
Print/transmit: SEPA pain.001 file to bank
↓
Bank executes → next day statement arrives
↓
FEBAN → import statement → clears 100010 → Dr
Main Bank 100000
PH15 — FI/CO Integration
📊 REAL DATA: TKA01: GBGR controlling area. CSKS: cost center master. CEPC: profit center master data.
PH16 — SD/FICO Integration
📊 REAL DATA: TVAK: 156 sales order types (Z010: 2368 occurrences). VBRK: 10k billing docs (F2=7393,
DE02=6590). VBFA: 40k document flow.
FI / CO INTEGRATION IN S/4HANA
VENDOR INVOICE (FB60) → ACDOCA ROW:
BUKRS = NI01 (FI: company code)
RACCT = 500000 (FI: G/L account)
RLDNR = 0L (FI: ledger)
HSL = 1000.00 (FI: amount)
KSTAR = 500000 (CO: cost element)
KOSTL = HR_CC (CO: cost center)
PRCTR = EURH (CO: profit center)
SEGMT = SEG01 (CO: segment)
→ ONE ROW = FI + CO (S/4 change)
→ No FI-CO reconciliation needed
→ G/L = cost element (no KA01)
OKB9: G/L 500000 → default CC HR_CC

FI / CO INTEGRATION IN S/4HANA — = HR_CC (CO: cost center)
PRCTR = EURH (CO: profit center)
SEGMT = SEG01 (CO: segment)
→ ONE ROW = FI + CO (S/4 change)
→ No FI-CO reconciliation needed
→ G/L = cost element (no KA01)
OKB9: G/L 500000 → default CC HR_CC
Without OKB9: "No cost assignment" error
SD → FI FLOW:
VA01 Sales Order (TVAK: Z010)
│
VL01N Delivery → VL02N Goods Issue
Dr COGS 410000 OBYC GBB/VAX (account modifier)
Cr Finished Goods OBYC BSX
│
VF01 Billing → VF02 Release (TVFK: F2 standard)
Dr Customer 120000 KNVV.AKONT
Cr Revenue 300000 VKOA (KOFI condition)
Cr Output VAT 175000 T030k MWS
→ Creates RV document in BKPF
→ ACDOCA: RBELN = billing doc number
│
F-28 / FEBAN Incoming Payment
Dr Main Bank 100000
Cr Customer 120000 ← cleared (FBL5N = zero)
PH17 — MM/FICO Integration
📊 REAL DATA: EKKO: PO headers. T161: PO types (NB=standard). RBKP: Invoice receipt headers.
RSEG: Invoice receipt line items with G/L assignments.
PH18 — HGB Architecture (L1 Ledger)
MM → FI INTEGRATION (P2P):
ME21N PO (T161: NB standard, UB stock transfer)
│
MIGO Goods Receipt (WE / WL doc type)
Dr Inventory / Expense OBYC BSX
Cr GR/IR Clearing 150000 OBYC WRX
│
MIRO Invoice (RE doc type — RBKP header, RSEG lines)
Dr GR/IR Clearing 150000
Dr Input VAT 154310 T030k VST
Cr Vendor 160000 LFB1.AKONT
│
Price difference (if PO ≠ invoice):

OBYC BSX
Cr GR/IR Clearing 150000 OBYC WRX
│
MIRO Invoice (RE doc type — RBKP header, RSEG lines)
Dr GR/IR Clearing 150000
Dr Input VAT 154310 T030k VST
Cr Vendor 160000 LFB1.AKONT
│
Price difference (if PO ≠ invoice):
Dr/Cr Price Variance OBYC PRD → P&L
│
F110 → SEPA → Bank → FEBAN → Vendor cleared
PH19 — IFRS Architecture (0L Ledger)
HGB PRINCIPLES → SAP CONFIG (L1 Ledger)
§ 252 VORSICHTSPRINZIP (Prudence):
HGB: Lower asset values, higher liabilities when uncertain
SAP: L1 depreciation rate HIGHER than 0L
L1 provisions HIGHER than 0L
FB50 with Ledger Group L1 only for HGB adjustments
§ 252(4) REALISATIONSPRINZIP (Realization):
HGB: Only REALIZED gains recognized
SAP: No fair value uplift on L1
Revenue recognized on billing/delivery only
§ 253(1)(4) NIEDERSTWERTPRINZIP (Lower of Cost/Market):
HGB: Write down if market < cost (MANDATORY)
Write-up allowed if reason for write-down ceases
SAP: ABAA (unplanned depreciation on L1)
Cannot recover on L1 if HGB rules don't allow
§ 249 RÜCKSTELLUNGEN (Provisions):
HGB: Must recognize provisions for all probable obligations
SAP: FB50 → ledger group L1 → provision posting
Different amount from 0L (IAS 37 best estimate)
§ 256a FREMDWÄHRUNGSBEWERTUNG (FX):
HGB: Recognize FX loss always
FX gain ONLY if realized

ons for all probable obligations
SAP: FB50 → ledger group L1 → provision posting
Different amount from 0L (IAS 37 best estimate)
§ 256a FREMDWÄHRUNGSBEWERTUNG (FX):
HGB: Recognize FX loss always
FX gain ONLY if realized
SAP: FAGL_FCV with different valuation method for L1
IMPARITÄTSPRINZIP (Asymmetry):
Losses anticipated | Gains only when certain
SAP: Conservative provisions on L1 vs 0L
PH19b — Parallel Accounting Deep Dive: 0L vs L1 Side by Side
The Same Machine — Two Completely Different Stories
KEY IFRS STANDARDS → SAP IMPLEMENTATION
IFRS 15 — REVENUE RECOGNITION
Recognize when performance obligation satisfied
SAP: VF01 billing → RV document → 300000 Revenue
5-step: Contract→Obligation→Price
→Allocate→Recognize
IFRS 16 — LEASES (no more operating lease off-balance-sheet)
Right-of-Use Asset + Lease Liability on Balance Sheet
SAP: Create asset in class 9000 (IFRS 16 ROU)
G/L 162000 = Lease Liability
Month: Dr Lease Liability + Dr Interest | Cr Bank
Depreciation: AFAB runs on ROU asset (0L only, area 01)
L1 (HGB): Operating lease → expense only (no asset)
IAS 36 — IMPAIRMENT
Test annually (or when trigger exists)
Recoverable amount = higher of VIU or FVLCD
SAP: ABAA → Unplanned depreciation on area 01 (0L)
REVERSIBLE: If impairment reason disappears (unlike HGB)

o asset)
IAS 36 — IMPAIRMENT
Test annually (or when trigger exists)
Recoverable amount = higher of VIU or FVLCD
SAP: ABAA → Unplanned depreciation on area 01 (0L)
REVERSIBLE: If impairment reason disappears (unlike HGB)
IAS 21 — FOREIGN CURRENCY
Initial: Record at spot rate
Period-end: Revalue monetary items (FAGL_FCV)
Exchange differences → 640000 FX Gain/Loss (P&L)
SAP: TCURR exchange rates → OB08 / TCURR table
IAS 37 — PROVISIONS
Recognize: Present obligation
+ probable outflow
+ reliable estimate
SAP: FB50 → 0L only if > L1
Amount = BEST ESTIMATE (not maximum unlike HGB)
IAS 12 — DEFERRED TAX
Temporary differences between carrying amount and tax base
SAP: Manual calculation → FB50 journal
Deferred Tax Asset: 170000 (BS)
Deferred Tax Liability: 180000 (BS)
Deferred Tax Expense: 650000 (P&L)
How to Post L1-Only Adjustment
Step 1: 0L (IFRS) posting already done
↓
Step 2: Calculate HGB difference
↓
FB50 → G/L Document
↓
Select Ledger Group: L1 (non-leading ledger only)
EXAMPLE: Machine purchased 01-Jan-2026 for €60,000
0L (IFRS) L1 (HGB)
───────────────── ─────────────────
Useful Life: 5 years 6 years
Method 0L: Straight Line (IAS 16)
Method L1: Declining or SL (§253)
Dep/Year: €12,000 €10,000 (or more if DB)
After Year 1:
APC: 60,000 60,000
Accum Depr: (12,000) (10,000)

─────────────────
Useful Life: 5 years 6 years
Method 0L: Straight Line (IAS 16)
Method L1: Declining or SL (§253)
Dep/Year: €12,000 €10,000 (or more if DB)
After Year 1:
APC: 60,000 60,000
Accum Depr: (12,000) (10,000)
NBV: 48,000 ← DIFFERENT → 50,000
After Year 3:
APC: 60,000 60,000
Accum Depr: (36,000) (30,000)
NBV: 24,000 ← DIFFERENT → 30,000
ACDOCA stores BOTH:
RLDNR=0L, RACCT=750000, HSL=-12000 (IFRS depr year 1)
RLDNR=L1, RACCT=750000, HSL=-10000 (HGB depr year 1)
IMPAIRMENT in Year 2 (machine partially damaged):
0L: IAS 36 → Write down to recoverable amount €30,000
ABAA: Dr Impairment Loss 640030 18,000
Cr Accum Depr 750000 18,000
(Can be REVERSED if value recovers)
L1: § 253 → Lower of cost/market
Same or different write-down
But typically CANNOT be reversed once written down
↓
Post HGB-specific adjustment
↓
Result: L1 has additional/different entry
↓
0L unchanged — IFRS not affected
↓
ACDOCA: new row RLDNR=L1 for this adjustment
Typical 0L vs L1 Differences to Expect
Topic 0L IFRS L1 HGB SAP Tool
Fixed Assets IFRS SL 5y HGB often faster/higher Area 01 vs Area 15
Provisions Best estimate (lower) Strict § 249 (higher) L1-only provision
Impairment Reversible IAS 36 Permanent § 253 ABAA on each ledger
FX
(monetary)
Always revalue Only if loss FAGL_FCV L1 flag

her Area 01 vs Area 15
Provisions Best estimate (lower) Strict § 249 (higher) L1-only provision
Impairment Reversible IAS 36 Permanent § 253 ABAA on each ledger
FX
(monetary)
Always revalue Only if loss FAGL_FCV L1 flag
Leases ROU asset IFRS 16 Operating expense
HGB
Asset on 0L, expense on
L1
Goodwill Annual impairment
test
5-15y amortization Different depr area
Inventory NRV if > cost OK Only lower of cost/NRV CKMVFM check
PH20 — Period End & Year End Close
Month-End Checklist (run in order)
01 Close all invoices (MIRO deadline)
↓
02 Bank statements imported (FEBAN)
↓
03 GR/IR cleared (MR11 — review old items)
↓
04 Post accruals (FB50 recurring entries)
↓
05 Fixed assets depreciation (AFAB test first)
↓
06 FX revaluation FAGL_FCV (monetary items)
↓
07 Intercompany reconciliation
↓
08 Trial balance review (FAGLL03H / FS10N)
↓
09 ACDOCA completeness check
↓
10 Close period OB52
Year-End Close Sequence
Complete period 12 month-end
↓
Asset depreciation AFAB (period 12, all areas)
↓
Inventory valuation / stock count
↓
AR/AP FX valuation F.05
↓
Impairment review (0L IAS 36 + L1 § 253)
↓
Provisions (0L IAS 37 + L1 § 249)
↓
↓
Deferred tax calculation + FB50
↓
HGB-only adjustments on L1
↓
IFRS-only adjustments on 0L
↓
Trial balance BOTH ledgers (F.01)
↓

10 Close period OB52 — on F.05
↓
Impairment review (0L IAS 36 + L1 § 253)
↓
Provisions (0L IAS 37 + L1 § 249)
↓
↓
Deferred tax calculation + FB50
↓
HGB-only adjustments on L1
↓
IFRS-only adjustments on 0L
↓
Trial balance BOTH ledgers (F.01)
↓
FAGLGVTR → P&L → 210000 Retained Earnings
↓
FAGLGVTR runs SEPARATELY for 0L and L1
↓
Open period 01 next year (OB52)
↓
Financial statements 0L (IFRS) + L1 (HGB)
PH21 — Financial Statements
📊 REAL DATA: FAGL_011PC: 12,431 items in financial statement version. Maps G/Ls to Balance Sheet
and P&L nodes.
Key Financial Reporting Transactions
T-code Description Note
F.01 Financial Statements Select ledger 0L or L1
FAGLL03H G/L Line Items (S/4) Direct ACDOCA report
FS10N G/L Account Balances Period-by-period
FBL1N Vendor Line Items AP subledger
FBL5N Customer Line Items AR subledger
AW01N Asset Explorer Full asset lifecycle
F.05 FX Valuation Year-end mandatory
FAGLGVTR Carry Forward Year-end mandatory
S_ALR_87013588 Balance Sheet Report Standard report
GLT0 vs ACDOCA (ECC vs S/4)
📊 REAL DATA: GLT0 - New GL.xlsx in your extract: legacy G/L totals table. In S/4HANA, this is a
compatibility view.
Table ECC Role S/4HANA Role
ACDOCA → FINANCIAL STATEMENTS
ALL ACDOCA ENTRIES
│
┌────┴────┐
↓ ↓
RLDNR=0L RLDNR=L1
│ │
IFRS F.01 HGB F.01
│ │
FAGL_011PC FAGL_011PC

📊 REAL DATA: GLT0 - New GL.xlsx in your extract: legacy G/ — L totals table. In S/4HANA, this is a
compatibility view.
Table ECC Role S/4HANA Role
ACDOCA → FINANCIAL STATEMENTS
ALL ACDOCA ENTRIES
│
┌────┴────┐
↓ ↓
RLDNR=0L RLDNR=L1
│ │
IFRS F.01 HGB F.01
│ │
FAGL_011PC FAGL_011PC
FS Structure FS Structure
│ │
IFRS Balance HGB Balance
Sheet Sheet
IFRS P&L HGB P&L
↓
E-BILANZ
XBRL → Finanzamt
GLT0 ECC: G/L totals table (primary) S/4HANA: compatibility view only — reads
ACDOCA
FAGLFLEXT ECC: New GL totals S/4HANA: compatibility view → ACDOCA
BSEG ECC: FI line items (primary) S/4HANA: compatibility view → ACDOCA
ACDOCA S/4HANA: Universal Journal
(primary)
Contains all FI + CO + AA data in one table
🔵 Story 1 — Buy a Machine
NI01 buys production machine €60,000 + 19% VAT
1. ME21N Purchase Order Vendor 1000001 · PO price €60,000 No accounting yet
↓
2. MIGO Goods Receipt Dr APC 700000 → 60,000 Cr GR/IR 150000 → 60,000
↓
3. MIRO Vendor Invoice Dr GR/IR 150000 → 60,000 Dr Input VAT 154310 → 11,400 Cr
Vendor 160000 → 71,400
↓
4. F110 Payment Run Dr Vendor 160000 → 71,400 Cr Bank Clearing 100010 → 71,400
↓
5. FEBAN Bank Statement Dr Main Bank 100000 → 71,400 Cr Bank Clearing 100010
→ 71,400
↓
6. AFAB Monthly Depreciation 0L: Dr 600000 1,000 | Cr 750000 1,000 L1: Dr 600000
833 | Cr 750000 833
↓
7.

🔵 Story 1 — Buy a Machine — Clearing 100010 → 71,400
↓
5. FEBAN Bank Statement Dr Main Bank 100000 → 71,400 Cr Bank Clearing 100010
→ 71,400
↓
6. AFAB Monthly Depreciation 0L: Dr 600000 1,000 | Cr 750000 1,000 L1: Dr 600000
833 | Cr 750000 833
↓
7. Year 1 Balance Sheet 0L NBV: 60,000 − 12,000 = 48,000 L1 NBV: 60,000 − 9,996 =
50,004
🟢 Story 2 — Sell a Product
NI01 sells stroller to customer €500 + 19% VAT
1. VA01 Sales Order Z010 Customer 2000001 · €500 Payment terms 30 days
↓
2. VL01N Delivery + Goods Issue Dr COGS 410000 → 250 Cr Inventory → 250
↓
3. VF01 Billing F2 → RV document Dr Customer 120000 → 595 Cr Revenue 300000 →
500 Cr Output VAT 175000 → 95
↓
4. CAMT.053 Bank Statement Customer paid
↓
5. FEBAN / F-28 Clear Customer Dr Main Bank 100000 → 595 Cr Customer 120000 →
595 (CLEARED)
↓
RESULT: Revenue P&L +500 · COGS −250 · Margin 250 Customer FBL5N = zero ✓
🟡 Story 3 — Pay a Vendor
NI01 pays €15,000 due vendor invoices via SEPA
1. Vendor invoices posted (MIRO) FBL1N: vendor balance 15,000 open
↓
2. F110 Proposal CoCode NI01 · Method T · due date filter
↓
3. Review Proposal Check vendor list · confirm amounts
↓
4. F110 Execute Dr Vendor 160000 → 15,000 Cr Bank Clearing 100010 → 15,000 SEPA
pain.001 file → bank
↓
5. Next Day Bank Statement Bank confirms transfer
↓
6.

🟡 Story 3 — Pay a Vendor — ter
↓
3. Review Proposal Check vendor list · confirm amounts
↓
4. F110 Execute Dr Vendor 160000 → 15,000 Cr Bank Clearing 100010 → 15,000 SEPA
pain.001 file → bank
↓
5. Next Day Bank Statement Bank confirms transfer
↓
6. FEBAN Import Dr Bank Clearing 100010 → 15,000 Cr Main Bank 100000 → 15,000
↓
7. RESULT FBL1N: vendor = zero ✓ Bank G/L 100000 reduced by 15,000 ✓
⭐ Story 4 — Year End 2026
NI01 closes fiscal year 2026
1. Complete all Dec transactions + month-end
↓
2. AFAB: Period 12 depreciation 0L + L1 separately (areas 01 and 15)
↓
3. FAGL_FCV: FX revaluation at closing rate 640000 FX Gain/Loss P&L entries
↓
4. FB50 L1-only: HGB provisions above IFRS
↓
5. F.05: AR/AP FX valuation
↓
6. Trial balance: F.01 → 0L | F.01 → L1
↓
7. FAGLGVTR: Balance carry-forward Runs for 0L separately Runs for L1 separately
P&L net → 210000 Retained Earnings
↓
8. OB52: Open 2027 period 01
↓
9. Financial Statements: F.01 0L → IFRS Group Reporting F.01 L1 → HGB Statutory +
E-Bilanz → Finanzamt
🎓 Business Process Q&A — 40 Key Questions
These are real implementation, interview, and UAT questions. Use them to test your understanding
before go-live.
❓ What is the Universal Journal (ACDOCA) and why does it matter?
ACDOCA is the central accounting table in S/4HANA that replaced BSEG, FAGLFLEXA, ANLP,

🎓 Business Process Q&A — 40 Key Questions — UAT questions. Use them to test your understanding
before go-live.
❓ What is the Universal Journal (ACDOCA) and why does it matter?
ACDOCA is the central accounting table in S/4HANA that replaced BSEG, FAGLFLEXA, ANLP,
and COEP. Every FI posting — from vendor invoices to asset depreciation to customer payments
— creates rows in ACDOCA. The key column RLDNR identifies which ledger (0L=IFRS, L1=HGB)
each row belongs to. Because FI and CO are in the same table, there is no FI-CO reconciliation
needed.
📋 EXAMPLE: DE02 ACDOCA: 10k rows. WL (STO goods issue) = 5,310 rows, all with RLDNR=0L and
RLDNR=L1 where parallel accounting applies.
💡 TIP: Use SE16N → ACDOCA to verify any posting. Check RLDNR, RACCT, HSL, KSTAR, KOSTL
on the same row.
❓ What is the difference between a leading ledger and a non-leading ledger?
The leading ledger (0L) is the primary accounting view. ALL postings automatically go to the
leading ledger. Non-leading ledgers (L1, T1) receive postings either in parallel (same document) or
via separate ledger-group-specific postings. In NI01: 0L = IFRS (leading), L1 = HGB (non-leading,
statutory). Both are stored in ACDOCA with their own RLDNR value.
📋 EXAMPLE: Depreciation: AFAB posts to area 01 → 0L (IFRS) and area 15 → L1 (HGB). Same

💡 TIP: Use SE16N → ACDOCA to verify any posting. Check RLDNR, RACCT, HSL, KSTAR, KOSTL — c postings. In NI01: 0L = IFRS (leading), L1 = HGB (non-leading,
statutory). Both are stored in ACDOCA with their own RLDNR value.
📋 EXAMPLE: Depreciation: AFAB posts to area 01 → 0L (IFRS) and area 15 → L1 (HGB). Same
asset, two different depreciation amounts in ACDOCA.
💡 TIP: Check FINSC_LEDGER for ledger setup. Check FINSC_ACCTG_PRNCPL for which
accounting principle is assigned to each ledger.
❓ A vendor invoice has been posted but the wrong tax code was used. What do you do?
You cannot change the tax code on a posted document. Options: (1) Reverse the invoice (FB08 or
MR8M for MIRO) and re-post with correct code. (2) For small amounts, post a correction document
with the tax difference. Check BSET to see the posted tax code and MWSTE (tax amount). Always
check FTXP to confirm the correct tax rate first.
📋 EXAMPLE: V1 (19%) posted instead of A1 (19%) — wrong type (input vs output). Must reverse KR
document and repost with correct code.
💡 TIP: FB08 → Reverse document → Enter reason → Repost with correct tax code. Check BSET
after reversal: tax amount should flip sign.
❓ What happens at year-end with the P&L accounts?
FAGLGVTR (balance carry-forward) closes all P&L accounts (Revenue and Expense) to zero and

💡 TIP: FB08 → Reverse document → Enter reason → Repost — with correct tax code. Check BSET
after reversal: tax amount should flip sign.
❓ What happens at year-end with the P&L accounts?
FAGLGVTR (balance carry-forward) closes all P&L accounts (Revenue and Expense) to zero and
transfers the net result to the retained earnings account (210000) configured in OB53. This runs
SEPARATELY for each ledger: once for 0L (IFRS result) and once for L1 (HGB result). The 210000
balance will be different per ledger if IFRS and HGB P&L results differ.
📋 EXAMPLE: NI01 P&L 2026: Revenue 500k − Expenses 350k = Net Profit 150k → FAGLGVTR →
210000 gets 150k. On L1, if HGB provisions are higher, net profit might be 120k → 210000 L1 = 120k.
💡 TIP: Run FAGLGVTR in test mode first. Check log. Then run in update mode for 0L, then for L1.
Verify 210000 balance in ACDOCA.
❓ What is the GR/IR clearing account and when does it go out of balance?
GR/IR (150000) is a clearing account that sits between Goods Receipt and Invoice Receipt in the
P2P cycle. GR posts a credit, IR posts a debit — they net to zero when the invoice matches the
PO price. The account goes out of balance when: (1) goods received but invoice not yet posted
(timing difference), (2) invoice posted but goods not received (e.g. ordering error), (3) price

📋 EXAMPLE: NI01 P&L 2026: Revenue 500k − Expenses 350k = Net Profit 150k → FAGLGVTR → — when the invoice matches the
PO price. The account goes out of balance when: (1) goods received but invoice not yet posted
(timing difference), (2) invoice posted but goods not received (e.g. ordering error), (3) price
difference between PO and invoice (goes to price variance). MR11 is used to clear old GR/IR open
items.
📋 EXAMPLE: Month-end: GR/IR 150000 shows €50,000 balance = goods received December, invoice
arrives January. Normal timing — investigate if balance is from prior months.
💡 TIP: MB5S = GR/IR balance report. MR11 = GR/IR maintenance (clear old items). Matching: MIRO
automatically matches against the PO EKKO/EKKN.
❓ Why can't you post directly to a reconciliation account?
A reconciliation account (like 160000 for AP) is linked to the subledger. When you post a vendor
invoice, the system automatically updates 160000 via the subledger posting — you never touch it
directly. If you could post directly to 160000, the subledger (FBL1N) would go out of sync with the
G/L balance. SAP enforces this with error FF786 if you try to post directly.
📋 EXAMPLE: FS00 → 160000 → 'Reconciliation Account for' = Creditors. If you try FB50 with 160000,
SAP gives error: 'Posting to account 160000 not possible directly'.

📋 EXAMPLE: NI01 P&L 2026: Revenue 500k − Expenses 350k = Net Profit 150k → FAGLGVTR → — s this with error FF786 if you try to post directly.
📋 EXAMPLE: FS00 → 160000 → 'Reconciliation Account for' = Creditors. If you try FB50 with 160000,
SAP gives error: 'Posting to account 160000 not possible directly'.
💡 TIP: To post a manual adjustment to the AP recon: use FB60/MIRO (via vendor) not FB50. For a
one-sided G/L adjustment, use a special G/L indicator or consult your FI lead.
❓ What is the difference between OB52 and OB53?
OB52 = Posting Period Maintenance. Controls which accounting periods are open or closed for
each document type. Example: close period 09 after September month-end. OB53 = Retained
Earnings Account. Maps P&L account types to the retained earnings G/L. Used ONLY by
FAGLGVTR at year-end. Completely different purposes.
📋 EXAMPLE: OB52 mistake: leaving period 09 open during October = users backpost to wrong period.
OB53 mistake: not configured = FAGLGVTR fails with 'no retained earnings account found'.
💡 TIP: OB52: open period 12 before December postings. Close period 12 after month-end. OB53: set
once during implementation, rarely changed.
❓ Explain the automatic payment program F110 step by step.
F110 runs in two phases. Phase 1 = Proposal: SAP looks at all vendor open items, applies due

💡 TIP: OB52: open period 12 before December postings. Close period 12 aft — er month-end. OB53: set
once during implementation, rarely changed.
❓ Explain the automatic payment program F110 step by step.
F110 runs in two phases. Phase 1 = Proposal: SAP looks at all vendor open items, applies due
date filter, payment method filter, selects eligible invoices. You review and can edit. Phase 2 =
Payment: creates KZ payment documents (Dr Vendor, Cr Bank Clearing), generates SEPA file.
After bank executes, bank statement arrives. FEBAN imports statement and clears bank clearing
account. Vendor = zero balance.
📋 EXAMPLE: FBZP must be configured first: 5 screens (company codes, paying company codes,
payment method country, payment method CoCode, bank determination). T042I assigns G/L accounts
to payment methods.
💡 TIP: F110 → Parameters → Proposal (review) → Edit if needed → Payments → Print/transmit
SEPA → Monitor payment → FEBAN when statement arrives
❓ What is ACDOCA RLDNR and how do you use it?
RLDNR = Ledger ID in ACDOCA. Every line in ACDOCA has RLDNR = '0L' (IFRS leading) or 'L1'
(HGB parallel). When you run a report, you filter by RLDNR to get the IFRS or HGB view. F.01
financial statements = select ledger 0L for IFRS, L1 for HGB. Same G/L account can have
DIFFERENT balances on 0L vs L1 (e.g. accumulated depreciation).

💡 TIP: F110 → Parameters → Proposal (review) → Edit if needed → Payments → Print/transmit — run a report, you filter by RLDNR to get the IFRS or HGB view. F.01
financial statements = select ledger 0L for IFRS, L1 for HGB. Same G/L account can have
DIFFERENT balances on 0L vs L1 (e.g. accumulated depreciation).
📋 EXAMPLE: SE16N → ACDOCA → RLDNR = 0L → shows IFRS rows. RLDNR = L1 → shows HGB
rows. For depreciation: 0L shows IFRS accumulated depr, L1 shows HGB accumulated depr. Often
different amounts.
💡 TIP: In FAGLL03H: filter by ledger. In F.01: select ledger in selection screen. In FS10N: select
ledger for balance view.
❓ What does 'New General Ledger' mean and how is it different from classic GL?
The New General Ledger (New GL) was introduced in ECC 6.0 and is MANDATORY in S/4HANA.
Key features: (1) Document splitting for segment/profit center balance sheets, (2) Parallel
accounting via ledgers (not Special Purpose Ledger), (3) Real-time integration with CO in
ACDOCA, (4) No separate CO reconciliation. In S/4HANA, New GL = ACDOCA = everything is
integrated. The old GLT0 and FAGLFLEXA are compatibility views.
📋 EXAMPLE: Old ECC: You had to run KALC (reconciliation ledger) to reconcile FI and CO. In
S/4HANA with ACDOCA: FI and CO are the same table, zero reconciliation needed.
💡 TIP: Check if New GL is active: FAGL_ACTIVATION → should be active. In S/4HANA: always

📋 EXAMPLE: Old ECC: You had to run KALC — (reconciliation ledger) to reconcile FI and CO. In
S/4HANA with ACDOCA: FI and CO are the same table, zero reconciliation needed.
💡 TIP: Check if New GL is active: FAGL_ACTIVATION → should be active. In S/4HANA: always
active, cannot be deactivated.
❓ A vendor has a debit balance (they owe US money). What could cause this?
A debit balance on a vendor account means the vendor's open items sum to a debit (we paid more
than we owe, or a credit memo is outstanding). Common causes: (1) Overpayment or duplicate
payment, (2) Credit memo posted but not matched to invoice, (3) Advance payment (down
payment using special G/L indicator A), (4) Down payment request not cleared. Check FBL1N →
vendor → all open items. Use F-54 to clear credit memo against invoice.
📋 EXAMPLE: FBL1N → vendor 1000001 → all items → sort by amount. Credit memos (document type
KG) show as debits on vendor. If very old credit memo: request refund from vendor or apply to next
invoice.
💡 TIP: F-44 = manual clearing. F-54 = down payment clearing. FB1K = post incoming payment from
vendor (refund).
❓ What is the difference between partial payment and residual payment?
Partial payment: Customer pays less than invoice amount. Old invoice stays open. New payment
document posted.

💡 TIP: F-44 = manual clearing. F-54 = down payment clearing. FB1K = post — incoming payment from
vendor (refund).
❓ What is the difference between partial payment and residual payment?
Partial payment: Customer pays less than invoice amount. Old invoice stays open. New payment
document posted. Two open items on customer account: original invoice (full amount) + partial
payment (negative). FBL5N shows both. Residual payment: Old invoice cleared in full. New open
item created for remaining balance. FBL5N shows only one open item: the residual. Residual =
cleaner for dunning. Partial = better audit trail.
📋 EXAMPLE: Invoice €1,000. Customer pays €700. Partial: FBL5N shows Invoice 1000 + Payment
-700 = both open. Residual: FBL5N shows Residual 300 = one item.
💡 TIP: F-28 → Payment → select invoice → partial: enter partial amount. Residual: click 'Residual
items' and enter partial amount. Dunning prefers residual (cleaner aging).
❓ Explain the bank account master data structure in SAP.
Three levels: (1) House Bank (T012): the physical bank institution. HBKID = internal ID, bank
country, bank key (BLZ). (2) Bank Account (T012K): specific account at that bank. HKTID =
account ID, linked to G/L account 100000, separate clearing G/L 100010. (3) G/L Account (FS00):
the actual balance in FI. The connection: House Bank → Account ID → G/L account. FBZP uses

💡 TIP: Check if New GL is active: FAGL_ACTIVATION → should be active. In S/4HANA: always — ic account at that bank. HKTID =
account ID, linked to G/L account 100000, separate clearing G/L 100010. (3) G/L Account (FS00):
the actual balance in FI. The connection: House Bank → Account ID → G/L account. FBZP uses
this hierarchy to determine which bank to pay from.
📋 EXAMPLE: DEBA = Deutsche Bank (HBKID). MAIN = main EUR account (HKTID). G/L 100000 =
main bank account balance. G/L 100010 = bank clearing (nets to zero daily).
💡 TIP: SE16N → T012 → see house banks. T012K → see account IDs and linked G/L accounts. FI12
= transaction to maintain house bank. FBZP → Bank Determination uses this hierarchy.
❓ What happens in ACDOCA when you run AFAB (depreciation)?
AFAB posts depreciation to ACDOCA with document type AF. For each active asset with a
depreciation key and useful life, SAP calculates the period depreciation amount per depreciation
area. Each area posts to its assigned ledger: Area 01 → RLDNR=0L (IFRS), Area 15 →
RLDNR=L1 (HGB). ACDOCA gets two rows per asset per period: one for IFRS depreciation, one
for HGB depreciation. These can be different amounts if useful lives differ.
📋 EXAMPLE: Asset 1000001 (machine): AFAB period 1/2026 → ACDOCA row 1: RLDNR=0L,
RACCT=600000, HSL=-1000 (IFRS depr) → ACDOCA row 2: RLDNR=L1, RACCT=600000,
HSL=-833 (HGB depr).

📋 EXAMPLE: DEBA = Deutsche Bank (HBKID). MAIN = main EUR account (HKTID). G/L 100000 = — different amounts if useful lives differ.
📋 EXAMPLE: Asset 1000001 (machine): AFAB period 1/2026 → ACDOCA row 1: RLDNR=0L,
RACCT=600000, HSL=-1000 (IFRS depr) → ACDOCA row 2: RLDNR=L1, RACCT=600000,
HSL=-833 (HGB depr). AW01N shows both areas simultaneously.
💡 TIP: After AFAB: SE16N → ACDOCA → BLART=AF → check both RLDNR rows. AW01N → asset
→ shows planned vs posted per area. If AFAB fails: check ANLB for missing depreciation key.
❓ What is document splitting and when do you need it?
Document splitting is a New GL feature that automatically assigns profit center / segment to ALL
lines of an accounting document, including clearing lines. Without splitting: only revenue/expense
lines carry profit center. With splitting: the vendor liability line also gets profit center (enabling a
balance sheet by segment). Required for: IFRS 8 segment reporting, profit center balance sheets,
legal entity consolidation at segment level.
📋 EXAMPLE: Invoice €1,000 allocated 60% to profit center A, 40% to B. Without splitting: Vendor
160000 line has no PC. With splitting: Vendor 160000 splits automatically: 600 to PC-A, 400 to PC-B.
Balance sheet by profit center = balanced.
💡 TIP: Activate via FAGL_SGEN. Create zero-balance clearing account (e.g. 999999). Define splitting

160000 line has no PC. Wi — th splitting: Vendor 160000 splits automatically: 600 to PC-A, 400 to PC-B.
Balance sheet by profit center = balanced.
💡 TIP: Activate via FAGL_SGEN. Create zero-balance clearing account (e.g. 999999). Define splitting
method and rules per business transaction. Check: FB60 → posting → FBL1N → vendor lines should
show profit center if splitting active.
❓ What is OKB9 and why does it cause posting errors?
OKB9 = Default Account Assignment for Automatic Cost Assignment. For P&L G/L accounts (cost
elements in S/4), SAP requires a CO object (cost center, internal order, WBS element, profit
center) to be assigned. OKB9 provides a DEFAULT cost center for a G/L account when no cost
center is provided in the posting. Without OKB9 (or a cost center on the transaction), posting to a
P&L account fails with error: 'Account XXXXXX requires an assignment to a CO object'.
📋 EXAMPLE: G/L 500000 (Salaries). Manual FB50 posting → no cost center entered → error. OKB9:
500000 → Cost Center HR_CC (default) → posting succeeds automatically.
💡 TIP: KP06 = cost center planning. OKB9 = default account assignment. COSS/COEP = CO line
items (compatibility views in S/4). Check: SE16N → ACDOCA → KOSTL should be populated for all
P&L postings.

500000 → Cost Center HR_CC (default) → posting succ — eeds automatically.
💡 TIP: KP06 = cost center planning. OKB9 = default account assignment. COSS/COEP = CO line
items (compatibility views in S/4). Check: SE16N → ACDOCA → KOSTL should be populated for all
P&L postings.
❓ Why does the FX valuation (FAGL_FCV) run differently for 0L and L1?
IFRS (0L) and HGB (L1) have different FX rules. IFRS IAS 21: ALL monetary items (AR, AP, bank)
must be revalued at closing rate — both gains AND losses recognized. HGB § 256a: Losses
always recognized, but gains only if REALIZED (Imparitätsprinzip = asymmetry principle).
FAGL_FCV has a setting per ledger/accounting principle to apply the correct rule. Result: 0L may
show FX gain, L1 shows no FX gain (or zero). Both stored in ACDOCA separately.
📋 EXAMPLE: USD vendor invoice €10,000 at rate 1.10. Year-end rate 1.05. USD weakened. EUR
equivalent fell. BOTH 0L and L1 recognize the loss. But if USD strengthened: 0L shows FX gain, L1
shows zero (HGB asymmetry).
💡 TIP: FAGL_FCV → selection: company code, open items, GL accounts, rate type. Run for each
valuation area (0L, L1) separately. Check ACDOCA for document type FW after valuation.
❓ What is the Business Partner (BP) and how does it relate to vendors and customers?
In S/4HANA, Business Partner is MANDATORY for vendor and customer master data.

📋 EXAMPLE: USD vendor invoice €10,000 at rate 1.10. Year-end rate 1.05. USD weakened. EUR — tely. Check ACDOCA for document type FW after valuation.
❓ What is the Business Partner (BP) and how does it relate to vendors and customers?
In S/4HANA, Business Partner is MANDATORY for vendor and customer master data. The BP is
the central master data object. Vendor = Business Partner with role FLVN01. Customer = Business
Partner with role FLCU01. LFB1 and KNB1 tables still exist (populated automatically from BP).
FK01/XD01 transactions still work but internally create/update the BP. BUT000 table = BP master.
Consequence: cannot create a vendor without a valid BP.
📋 EXAMPLE: Your LFB1 extract (843 vendors DE02): each vendor MUST have a corresponding BP in
BUT000. PREC_BP_CHECK report validates consistency. If migration from ECC, BP migration must
run before go-live.
💡 TIP: Transaction BP (central Business Partner): create with all required roles. Check: SE16N →
BUT000 → BUT100 (roles) → LFB1 (vendor company code data).
❓ What is ELKO / FEBAN / FEBP and how do they relate?
Electronic bank processing in SAP uses three steps. ELKO (TCODE FEBC) = Electronic Bank
Communication: imports raw bank files (CAMT, MT940). FEBAN (TCODE FEBAN) = Electronic
Bank Statement: the SAP screen to view imported statements and manually clear open items.

📋 EXAMPLE: USD vendor invoice €10,000 at rate 1.10. Year-end rate 1.05. USD weakened. EUR — steps. ELKO (TCODE FEBC) = Electronic Bank
Communication: imports raw bank files (CAMT, MT940). FEBAN (TCODE FEBAN) = Electronic
Bank Statement: the SAP screen to view imported statements and manually clear open items.
FEBP (TCODE FEBP) = Post Electronic Bank Statement: the batch program that automatically
matches and posts bank items. FEBKO = header table, FEBEP = line items table.
📋 EXAMPLE: FEBAN shows your bank statement with green (auto-posted) and red (manual
intervention needed) items. Green = algorithm found matching open item. Red = no match found,
manual posting required.
💡 TIP: Process: Bank file arrives → FEBC import → FEBKO/FEBEP populated → FEBP auto-posts
matched items → FEBAN for manual items → all items green = bank reconciliation complete.
❓ Explain asset retirement / disposal in SAP. What happens to accumulated
depreciation?
Asset retirement removes an asset from the books and recognizes a gain or loss. In SAP:
Transaction ABAON (disposal without revenue) or ABAVN (disposal with revenue). The posting: Dr
Accumulated Depreciation (750000), Dr Loss on Disposal (640020) or Cr Gain on Disposal
(640010), Cr APC (700000). The NBV = APC − Accum Depr = the difference that becomes gain or
loss. After retirement, asset status = retired. ANLA shows retirement date.

💡 TIP: Process: Bank file arrives → FEBC import → FEBKO/FEBEP populated → FEBP auto-posts — Dr Loss on Disposal (640020) or Cr Gain on Disposal
(640010), Cr APC (700000). The NBV = APC − Accum Depr = the difference that becomes gain or
loss. After retirement, asset status = retired. ANLA shows retirement date. Both 0L and L1 receive
retirement posting (possibly with different gain/loss amounts).
📋 EXAMPLE: Machine: APC 60,000, Accum Depr 48,000 (0L IFRS, 4 years), sold for 15,000 scrap.
NBV = 12,000. Gain = 15,000 − 12,000 = 3,000. Posting: Dr AccDepr 48,000 + Dr Cash 15,000 + Cr
APC 60,000 + Cr Gain 3,000.
💡 TIP: ABAON/ABAVN runs the accounting. AW01N shows the asset lifecycle including retirement.
ANEP shows all line items. Check ACDOCA for retirement document: Dr Accum Depr, Cr APC, Dr/Cr
Gain/Loss.
❓ What tables do you check to troubleshoot a missing FI document?
Start with BKPF (document header) — search by CoCode, document type, date range, reference.
Then ACDOCA for the actual accounting lines. For vendor invoices: RBKP (header) + RSEG
(lines). For billing: VBRK (header) + VBRP (items). For asset posting: ANEP. For payment: PAYR
(payment run) + T042E. Key fields to check: BUKRS (company code), BLART (document type),
BUDAT (posting date), GJAHR (fiscal year).
📋 EXAMPLE: Missing vendor invoice: SE16N → RBKP → company code NI01 → date range →

💡 TIP: Process: Bank file arrives → FEBC import → FEBKO/FEBEP populated → FEBP auto-posts — AYR
(payment run) + T042E. Key fields to check: BUKRS (company code), BLART (document type),
BUDAT (posting date), GJAHR (fiscal year).
📋 EXAMPLE: Missing vendor invoice: SE16N → RBKP → company code NI01 → date range →
LIFNR (vendor) → check RBSTAT (status: A=posted, F=error). Also check BKPF → XBLNR
(reference) for the document.
💡 TIP: Posting date vs document date: BKPF.BUDAT = fiscal period date. If BUDAT is in closed
period: error. BLDAT = original document date. Use FAGLL03H for G/L line items — most reliable in
S/4.
❓ What is the difference between a document date, posting date, and value date?
Document date (BLDAT) = the date on the original paper document (e.g. vendor invoice date).
Posting date (BUDAT) = the date the entry is made in SAP — determines the fiscal period. Value
date (VALUT) = the effective date for bank statements and cash management, used for bank
interest and liquidity planning. For month-end: BUDAT must be within the open period. Common
error: document date in December but posting date in November → document goes to wrong
period.
📋 EXAMPLE: Vendor invoice dated 28-Nov but received 05-Dec. Document date = 28-Nov. Posting
date = 05-Dec (when you post in SAP). VAT/fiscal period = December. Payment terms calculated from
document date.

📋 EXAMPLE: Missing vendor invoice: SE16N → RBKP → company code NI01 → date range → — wrong
period.
📋 EXAMPLE: Vendor invoice dated 28-Nov but received 05-Dec. Document date = 28-Nov. Posting
date = 05-Dec (when you post in SAP). VAT/fiscal period = December. Payment terms calculated from
document date.
💡 TIP: Always check BKPF: BLDAT (doc date), BUDAT (posting date), VALUT (value date). For cutoff
issues: use posting date to determine period assignment.
❓ How does profit center accounting work in S/4HANA?
In S/4HANA, profit center (PRCTR) is a dimension directly in ACDOCA — no separate profit center
accounting (EC-PCA) table needed. Every posting that has a cost center also flows to the profit
center assigned to that cost center (CSKS.PRCTR). For SD billing, the profit center comes from
material master or sales order. For asset accounting, from asset master. With document splitting
active: ALL lines carry profit center including balance sheet items.
📋 EXAMPLE: CEPC extract: your profit centers. CSKS: cost center to profit center mapping. F.01 with
profit center filter = profit center P&L. FAGLL03H with PRCTR selection = P&L by profit center.
💡 TIP: 1KE5 = Profit Center Group. KE5T = PC assignment monitor. GR55 = profit center reports. In
S/4: KEF2 → ACDOCA based profit center reporting replaces old EC-PCA.

📋 EXAMPLE: Missing vendor invoice: SE16N → RBKP → company code NI01 → date range → — LL03H with PRCTR selection = P&L by profit center.
💡 TIP: 1KE5 = Profit Center Group. KE5T = PC assignment monitor. GR55 = profit center reports. In
S/4: KEF2 → ACDOCA based profit center reporting replaces old EC-PCA.
❓ What is the Controlling Area and how does it relate to Company Codes?
The Controlling Area (KOKRS) is the umbrella for all CO management: cost centers, profit centers,
internal orders, profitability analysis. One controlling area can cover multiple company codes. Your
system: GBGR = controlling area covering all 27 company codes. This means all company codes
share the same cost center hierarchy, profit center structure, and CO configuration. The controlling
area currency (EUR) is used for CO management reporting.
📋 EXAMPLE: TKA01 extract: GBGR controlling area. CSKS: cost centers assigned to GBGR. CEPC:
profit centers in GBGR. All 27 CoCodes (DE02, GB01, US01, AE09…) post CO objects to GBGR. This
enables global management reporting across all entities.
💡 TIP: OX06 = assign company code to controlling area. OKKP = controlling area settings. Check:
SE16N → TKA01 → KOKRS=GBGR → see all assigned company codes.
❓ A SEPA payment file was generated but the bank rejected it. What do you do?

💡 TIP: OX06 = a — ssign company code to controlling area. OKKP = controlling area settings. Check:
SE16N → TKA01 → KOKRS=GBGR → see all assigned company codes.
❓ A SEPA payment file was generated but the bank rejected it. What do you do?
Bank rejection of SEPA pain.001 file usually means: (1) Wrong IBAN/BIC format on vendor master,
(2) Mandate missing for direct debit, (3) File structure error (wrong pain.001 version), (4)
Insufficient funds. Steps: (1) Obtain bank rejection reason from bank communication log, (2) Check
vendor LFB1/LFA1 bank details (BANKL, IBAN, SWIFT), (3) Reset payment run (FBZP → F110 →
reset), (4) Correct vendor bank data, (5) Re-run F110.
📋 EXAMPLE: Vendor 1000001: IBAN DE89370400440532013000 but last digit wrong → bank rejects.
Go to FK02 → bank data → correct IBAN → re-run F110.
💡 TIP: F110 → payment log → FPAYM. Check: REGUH (payment header) + REGUP (line items) for
payment run details. Reset: F110 → Edit → Reset Proposal. Then re-run with corrected data.
❓ What is the difference between FAGLL03 and FAGLL03H?
FAGLL03 is the ECC-era G/L line item report that read from BSEG. FAGLL03H is the S/4HANA
version that reads directly from ACDOCA. In S/4HANA, FAGLL03H is the correct transaction to
use.

💡 TIP: F110 → payment log → FPAYM. Check: REGUH (payment header) + REGUP (line items) for — ence between FAGLL03 and FAGLL03H?
FAGLL03 is the ECC-era G/L line item report that read from BSEG. FAGLL03H is the S/4HANA
version that reads directly from ACDOCA. In S/4HANA, FAGLL03H is the correct transaction to
use. It includes the ledger selector (0L or L1), is much faster due to HANA in-memory database,
and shows CO fields (cost center, profit center) alongside FI fields on the same line. Old FAGLL03
still works but is slower.
📋 EXAMPLE: FAGLL03H → company code NI01 → G/L 300000 → Ledger 0L → shows all IFRS
revenue postings. Switch to L1 → shows HGB revenue (may differ if any L1-only adjustments).
💡 TIP: Use FAGLL03H in S/4HANA. Select ledger in the selection screen. Export to Excel for analysis.
Add fields: KOSTL, PRCTR, SEGMENT via layout settings.
❓ What is E-Bilanz and which companies must submit it?
E-Bilanz (Electronic Balance Sheet) is the German legal requirement to submit financial
statements in XBRL format electronically to the Finanzamt (German tax office) via the Elster portal.
Required for: German GmbH, AG, KG, OHG (most business entities). Exemptions: small sole
traders below thresholds. In SAP: you prepare the HGB financial statements (L1 ledger), map G/L
accounts to the XBRL taxonomy (HGB Taxonomie), generate the XBRL file, and submit via Elster.

📋 EXAMPLE: FAGLL03H → company code NI01 → G/L 300000 → Ledger 0L → shows all IFRS — ties). Exemptions: small sole
traders below thresholds. In SAP: you prepare the HGB financial statements (L1 ledger), map G/L
accounts to the XBRL taxonomy (HGB Taxonomie), generate the XBRL file, and submit via Elster.
SAP offers DART and third-party tools for XBRL generation.
📋 EXAMPLE: NI01 / DE02: must submit E-Bilanz for each German entity annually. FAGL_011PC
structure must map G/L accounts to E-Bilanz taxonomy codes (XBRL). T-code: FINSC_EBILANZ (if
S/4 E-Bilanz component active).
💡 TIP: Steps: F.01 L1 → HGB trial balance → E-Bilanz mapping → XBRL generation → Elster
submission. Deadline: approximately 12 months after fiscal year end. Check: BRZ (German tax
authority) for current taxonomy version.
❓ What happens to BSEG in S/4HANA and can you still use it?
In S/4HANA, BSEG is a COMPATIBILITY VIEW. When you SELECT FROM BSEG in ABAP, SAP
internally redirects the query to ACDOCA. The data is correct but the performance may be
suboptimal for large datasets. Old custom ABAP reports that use BSEG still work but should be
rewritten to use ACDOCA directly for performance. Important: you cannot INSERT or UPDATE
BSEG directly in S/4 — all FI postings go through ACDOCA. FBL1N, FBL5N use BSEG
compatibility view and still work correctly.

💡 TIP: Steps: F.01 L1 → HGB trial balance → E-Bilanz mapping → XBRL generation → Elster — ld be
rewritten to use ACDOCA directly for performance. Important: you cannot INSERT or UPDATE
BSEG directly in S/4 — all FI postings go through ACDOCA. FBL1N, FBL5N use BSEG
compatibility view and still work correctly.
📋 EXAMPLE: Custom Z-report: SELECT * FROM BSEG WHERE BUKRS = 'DE02'. In S/4: works but
slow for 40k+ documents. Rewrite to: SELECT * FROM ACDOCA WHERE BUKRS = 'DE02' AND
RLDNR = '0L'. 10x faster on HANA.
💡 TIP: Check with SAP Note 2217940 for BSEG compatibility details. Use ACDOCA for all new
development. SE11 → BSEG → check definition: should show it's a CDS view or compatibility
structure.
❓ How do you read the ANLA table and what does it tell you?
ANLA = Asset Master Record. One row per asset. Key fields: ANLN1 (asset number), ANLN2 (subnumber, usually 0), BUKRS (company code), ANLKL (asset class), AKTIV (acquisition date),
DEAKT (retirement date), ZUGDT (acquisition value), TXT50 (description). Your extract: 12,819
assets in DE02. Asset class distribution shows most assets are in class 1000 (Machinery). DEAKT
populated = asset retired. AKTIV date shows when asset was capitalized.
📋 EXAMPLE: SE16N → ANLA → BUKRS=DE02 → 12,819 rows. Filter ANLKL=3000 → shows assets
under construction. Filter DEAKT ≠ initial → shows retired assets.
💡 TIP: ANLA = master.

💡 TIP: Check with SAP Note 2217940 for BSEG compatibility details. Use ACDOCA for all new — AKTIV date shows when asset was capitalized.
📋 EXAMPLE: SE16N → ANLA → BUKRS=DE02 → 12,819 rows. Filter ANLKL=3000 → shows assets
under construction. Filter DEAKT ≠ initial → shows retired assets.
💡 TIP: ANLA = master. ANLB = depreciation terms (useful life, key). ANEP = line items (acquisitions,
retirements). ANLC = planned depreciation values. AW01N transaction shows all in one screen.
❓ What causes the 'No cost assignment possible' error in posting?
This error occurs when posting to a P&L G/L account (cost element in CO) without a CO
assignment (cost center, internal order, profit center). Required fixes: (1) OKB9 = set default cost
center for this G/L, (2) Substitution rule to default cost center automatically, (3) Include cost center
in the posting manually (FB60 → cost center field). Root cause: in S/4HANA, every P&L G/L = cost
element. Every cost element posting MUST have a CO assignment.
📋 EXAMPLE: FB60 → vendor invoice → G/L line for office supplies 500000 → no cost center filled →
error KI 235 'Account 500000 requires cost assignment'. Fix: OKB9 → 500000 → NI01 → Cost Center
= ADMIN_CC.
💡 TIP: KP26 = set CO version. OKB9 = default account assignments. Check: ACDOCA → KOSTL
column → should be populated for all P&L G/L rows. Blank KOSTL on P&L G/L = posting error.

📋 EXAMPLE: SE16N → ANLA → BUKRS=DE02 → 12,819 rows. Filter ANLKL=3000 → shows assets — 500000 → NI01 → Cost Center
= ADMIN_CC.
💡 TIP: KP26 = set CO version. OKB9 = default account assignments. Check: ACDOCA → KOSTL
column → should be populated for all P&L G/L rows. Blank KOSTL on P&L G/L = posting error.
❓ What is the difference between posting to ledger group 0L vs L1 vs 0L+L1?
Ledger Group in SAP = which ledgers receive a posting. Ledger Group '0L' = post ONLY to 0L
(IFRS leading ledger). Ledger Group 'L1' = post ONLY to L1 (HGB non-leading). Ledger Group
blank or '0L+L1' = post to both simultaneously. Normal business transactions (vendor invoices,
customer billing) = both ledgers receive the same posting. HGB-only adjustments: use FB50 with
ledger group L1 to post only to HGB. IFRS-only entries (IFRS 16 ROU asset on 0L without HGB):
ledger group 0L.
📋 EXAMPLE: HGB higher provision: 0L has provision €100k (IFRS best estimate). L1 needs €150k
(HGB strict). FB50 → ledger group L1 → post €50k additional provision → L1 now has €150k, 0L
unchanged at €100k.
💡 TIP: FB50 → Header → Ledger Group field. Select L1 for HGB-only. F.01 0L vs L1 shows different
provision amounts after L1-only posting.
❓ What is the Material Ledger and why is it mandatory in S/4HANA?
Material Ledger (ML) extends inventory valuation to support actual costing and multi-currency
valuation.

💡 TIP: FB50 → Header → Ledger Group field. Select L1 for HGB-only. F.01 0L vs L1 shows d — ifferent
provision amounts after L1-only posting.
❓ What is the Material Ledger and why is it mandatory in S/4HANA?
Material Ledger (ML) extends inventory valuation to support actual costing and multi-currency
valuation. In ECC it was optional. In S/4HANA it is MANDATORY for all company codes with MM.
Why: (1) S/4HANA inventory valuation uses ML for multi-currency (LC, GC, profit center currency),
(2) Actual costing (CKMLCP) requires ML, (3) Price differences reposted to actual cost via
CKMVFM. T001k (Valuation Area) extract shows 50 valuation areas — all must have ML active in
OMEI.
📋 EXAMPLE: T001k extract: 50 valuation areas linked to 50 plants. Each must have Material Ledger
active. If not: MIGO goods receipt fails or prices are wrong. CKMVFM = ML balance table.
💡 TIP: OMEI = activate ML per valuation area. CKMSTART = start ML for period. CKM3N = material
ledger cockpit (shows actual prices). Check: SE16N → CKMVFM → BWKEY (valuation area) →
MATNR (material) → prices per period.
❓ What is the difference between MIRO and FB60?
MIRO = MM invoice verification. Used for PO-based invoices. References a Purchase Order
(EKKO) → validates quantity, price, GR. Creates RE document. Automatically does 3-way match
(PO quantity × price vs GR vs invoice). FB60 = FI direct vendor invoice.

💡 TIP: KP26 = set CO version. OKB9 = default account assignments. Check: ACDOCA → KOSTL — Used for PO-based invoices. References a Purchase Order
(EKKO) → validates quantity, price, GR. Creates RE document. Automatically does 3-way match
(PO quantity × price vs GR vs invoice). FB60 = FI direct vendor invoice. No PO reference. No 3way match. Creates KR document. Used for: service invoices, overhead invoices, non-PO
purchases. Both post to vendor reconciliation account (LFB1.AKONT).
📋 EXAMPLE: Machine purchase: MIRO (references PO from ME21N). Office cleaning service invoice:
FB60 (no PO, direct FI posting). MIRO tolerance key can block if price difference > tolerance. FB60
has no tolerance check.
💡 TIP: MIRO: Logistics Invoice Verification → RBKP + RSEG tables + EKKO + EKKN. FB60: BKPF +
ACDOCA only. Check: SE16N → RBKP → BLART=RE for MIRO invoices.
❓ What does the FAGL_011PC table represent and why does it matter?
FAGL_011PC is the Financial Statement Item table. It defines how G/L accounts map to financial
statement nodes (Balance Sheet line items and P&L line items). Think of it as the structure of your
Balance Sheet and P&L. Your extract has 12,431 items = 12,431 account assignments to FS
structure nodes. F.01 uses this table to build financial statements. E-Bilanz also uses this structure
with XBRL taxonomy mapping.

💡 TIP: KP26 = set CO version. OKB9 = default account assignments. Check: ACDOCA → KOSTL — Balance Sheet and P&L. Your extract has 12,431 items = 12,431 account assignments to FS
structure nodes. F.01 uses this table to build financial statements. E-Bilanz also uses this structure
with XBRL taxonomy mapping.
📋 EXAMPLE: G/L 700000 (APC Machinery) maps to FAGL_011PC node 'Tangible Fixed Assets —
Machinery'. G/L 300000 (Revenue) maps to 'Net Revenue — Product Sales'. Without this mapping,
F.01 cannot build the Balance Sheet.
💡 TIP: OB58 = define financial statement versions. SE16N → FAGL_011PC → VERSN (version) +
ERGSL (FS item) + KONTS/KONTE (G/L account range). Check: if F.01 shows balance on 'not
assigned' → some G/L missing from FAGL_011PC.
PH22 — Number Ranges & Document Types
FBN1 — FI Document Number Ranges
NR From To Used By Type
01 0000000001 0099999999 SA, AB Internal
15 1500000000 1599999999 KZ (pmt) Internal
19 1900000000 1999999999 KR (inv) Internal
51 5100000000 5199999999 RE (MIRO) Internal
LD 0100000000 0199999999 RV (billing) External ← SD assigns
📚 Number ranges never transport. Set in DEV, then manually in QAS and PRD before first posting.
Common Number Range Mistakes
🟥 Forgetting to set NR in PRD → first posting fails
🟥 NR exhausted (all 99M numbers used) → posting fails
🟥 Gap in number range → audit question (must explain)

📚 Number ranges never transport. Set in DEV, then manually in QAS an — d PRD before first posting.
Common Number Range Mistakes
🟥 Forgetting to set NR in PRD → first posting fails
🟥 NR exhausted (all 99M numbers used) → posting fails
🟥 Gap in number range → audit question (must explain)
🟥 Same NR for two document types in same company code → duplicates
✅ Check remaining capacity: FBN1 → see current number
NUMBER RANGES — How SAP assigns document numbers
COMPANY CODE + DOCUMENT TYPE + FISCAL YEAR = NUMBER RANGE
Example:
KR (Vendor Invoice) → NR 19 → 1900000000–1999999999
KZ (Vendor Payment) → NR 15 → 1500000000–1599999999
RE (GR Invoice) → NR 51 → 5100000000–5199999999
SA (GL Posting) → NR 01 → 0000000001–0099999999
AB (Asset) → NR 01 → 0000000001–0099999999
WL (Goods Issue) → Plant/MM assigned range
Two types of number ranges:
INTERNAL: SAP assigns next number automatically ← most common
EXTERNAL: User enters the number manually (e.g. check numbers)
IMPORTANT: Number ranges are NOT transported!
Must be set manually in each system (DEV, QAS, PRD)
T-code: FBN1 (FI number ranges)
✅ Year-dependent NR: reset each year (e.g. 2026: 20260001–20269999)
PH23 — Field Status Groups
🟪 CONFIG FS01 — Field Status Group G001 — Cost Accounts
① WHAT?
Controls mandatory fields when posting to P&L/expense G/L accounts.
② WHY?

✅ Year-dependen — t NR: reset each year (e.g. 2026: 20260001–20269999)
PH23 — Field Status Groups
🟪 CONFIG FS01 — Field Status Group G001 — Cost Accounts
① WHAT?
Controls mandatory fields when posting to P&L/expense G/L accounts.
② WHY?
Without Required cost center: expense posts without CO assignment → OKB9 fails.
③ WHERE?
SPRO → FI → GL → Business Transactions → G/L Account Posting
→ Make/Check Posting Rules (T-code: OBC4)
④ ENTER:
Field Value
Field Status Group G001
FIELD STATUS = Controls fields:
Required / Optional / Hidden
when posting to a specific G/L account
G/L Account (FS00) → Field Status Group → OBC4 Definition
Example:
FS00: 500000 Salaries → Field Status Group = G001
OBC4: G001 → Cost Center = REQUIRED
Posting FB50 to 500000 → must enter cost center
FIELD STATUS GROUP EXAMPLES:
G001 = Cost accounts (cost center REQUIRED)
G004 = Bank accounts (value date REQUIRED)
G005 = Material accounts (quantity OPTIONAL)
G019 = Tax accounts (tax code SUPPRESSED)
G020 = Reconciliation accounts (most fields optional)
G067 = General accounts
POSTING KEY also controls field status
Both must be satisfied — most restrictive wins:
PK 40 says: Cost Center = Optional
FSG G001 says: Cost Center = Required
→ Result: REQUIRED (strict wins)
Description Cost accounts — CC required
Cost Center Required

🟪 CONFIG FS01 — Field Status Group G001 — Cost Accounts — atus
Both must be satisfied — most restrictive wins:
PK 40 says: Cost Center = Optional
FSG G001 says: Cost Center = Required
→ Result: REQUIRED (strict wins)
Description Cost accounts — CC required
Cost Center Required
Profit Center Optional
Business Area Optional
Value Date Suppressed
⑤ CREATES:
G001 definition active. FS00 on expense G/L references G001.
⑥ TEST:
FB50 → G/L 500000 → leave cost center blank → should get error
⑦ EXPECT:
Error: 'Field Cost Center is a required field for G/L 500000'
⑧ LANDS IN:
FS00 FSG → OBC4 definition → posting validation
🟥 MISTAKE:
❌ Setting cost center = Optional when it should be Required → CO data missing in ACDOCA.
🟢 PASS:
Posting to G/L 500000 without CC gives error · With CC: ACDOCA.KOSTL populated
PH24 — Foreign Currency (FX) & Valuation
FAGL_FCV — Key Settings
Parameter 0L (IFRS) L1 (HGB)
Valuation Method IFRS (lowest/highest) HGB (lowest only)
Exchange Rate Type M (average closing) M (same)
Always valuate ✓ YES (gains + losses) ✗ Only losses
Reversal Posting Next period day 1 Next period day 1
FX Gain G/L 640010 640010 (if any)
FX Loss G/L 640020 640020
OBA1 — FX Account Determination
FX IN SAP — THREE EVENTS
1. TRANSACTION POSTING (spot rate on posting date)
USD invoice posted at rate 1.10
Dr Expense 910.00 EUR

🟢 PASS: — Gain G/L 640010 640010 (if any)
FX Loss G/L 640020 640020
OBA1 — FX Account Determination
FX IN SAP — THREE EVENTS
1. TRANSACTION POSTING (spot rate on posting date)
USD invoice posted at rate 1.10
Dr Expense 910.00 EUR
Cr Vendor 910.00 EUR (= USD 1,000 ÷ 1.10)
2. PERIOD-END VALUATION (FAGL_FCV — closing rate)
Closing rate: 1.05 (USD weakened)
EUR equivalent now: USD 1,000 ÷ 1.05 = 952.38
Dr Vendor 952.38 − 910.00 = 42.38 (vendor HIGHER)
Cr FX Loss 640000 42.38
→ 0L posts loss (IAS 21 — ALL monetary items)
→ L1 posts loss (HGB §256a — losses ALWAYS)
3. IF USD STRENGTHENED (rate 1.15):
EUR equivalent: USD 1,000 ÷ 1.15 = 869.57
→ 0L: posts FX GAIN 40.43 (IAS 21 — always recognize)
→ L1: NO entry
(HGB Imparitätsp. — unrealized gain ignored)
REVERSAL: FAGL_FCV creates valuation doc
Next period start: valuation REVERSES automatically
Net effect over time = realized FX gain/loss
🔍 TROUBLESHOOT: FX Valuation FAGL_FCV not posting
Check open items exist
FBL1N/FBL5N → open items in foreign currency
↓
Check exchange rate
OB08 → rate type M → closing date rate maintained?
↓
Check valuation method
FAGL_FCV → valuation method correct for 0L vs L1
↓
Check G/L FX accounts
OBA1 → KDB/KDF assigned → G/L 640010/640020 exist in FS00
↓
Check ledger selection

🔍 TROUBLESHOOT: FX Valuation FAGL_FCV not posting — type M → closing date rate maintained?
↓
Check valuation method
FAGL_FCV → valuation method correct for 0L vs L1
↓
Check G/L FX accounts
OBA1 → KDB/KDF assigned → G/L 640010/640020 exist in FS00
↓
Check ledger selection
FAGL_FCV must run separately for 0L (IFRS) and L1 (HGB)
↓
ACDOCA after run
SE16N → ACDOCA → BLART = BW (valuation) → check amount and RLDNR
OBA1: Assigns G/L accounts for FX differences
Per chart of accounts (GBGR/NIOP)
Per currency
Account Key: KDB (realized) / KDF (unrealized)
Example:
KDB realized loss → 640020
KDB realized gain → 640010
KDF unrealized (valuation) → 640020 / 640010
Also: OB08 → maintain exchange rates
Rate type M = standard
Used by FAGL_FCV and all FI postings
TCURR table = exchange rate storage
PH25 — Intercompany Postings
OBY6 — Intercompany Setup
Field Value
Company Code 1 NI01
Company Code 2 DE02
IC Receivable (NI01) 180000
IC Payable (DE02) 190000
Doc Type both SA (G/L posting)
📚 IC G/Ls must exist in BOTH company codes. NI01.180000 = "Due from DE02". DE02.190000 =
"Due to NI01". Must net to zero at group consolidation.
Intercompany STO Flow (WL Documents)
INTERCOMPANY IN SAP — NI01 → DE02 Posting
SCENARIO: NI01 pays DE02's vendor on behalf
WITHOUT IC CONFIG:
Only one company code can post → no cross-company balance

📚 IC G/Ls must exist in BOTH company codes. NI01.180000 = "Due from DE02". DE02.190000 = — roup consolidation.
Intercompany STO Flow (WL Documents)
INTERCOMPANY IN SAP — NI01 → DE02 Posting
SCENARIO: NI01 pays DE02's vendor on behalf
WITHOUT IC CONFIG:
Only one company code can post → no cross-company balance
WITH IC CONFIG (OBY6):
SAP automatically creates BOTH sides:
NI01 SIDE:
Dr IC Receivable from DE02 180000 €5,000
Cr Bank 100000 €5,000
DE02 SIDE (auto-created):
Dr Expense 500000 €5,000
Cr IC Payable to NI01 190000 €5,000
EACH COMPANY CODE BALANCES INDIVIDUALLY
Cross-company document: two BKPF entries linked by BVORG
PH26 — Financial Closing Cockpit (FCC)
STO (Stock Transfer Order) — DE02 to NI01
DE02 (Sending):
ME21N UB STO → MIGO goods issue → WL doc
Dr IC COGS (410000)
Cr Inventory (300100)
Billing (SD billing DE02→NI01):
VF01 IV billing type
Dr IC Receivable (180000)
Cr IC Revenue (380000)
NI01 (Receiving):
MIGO goods receipt (WE)
Dr Inventory (300100)
Cr GR/IR IC (150010)
MIRO IC vendor invoice
Dr GR/IR IC (150010)
Cr IC Payable (190000)
BKPF: WL = 16,125 docs (your extract)
Most are STO goods issues DE02→others
Month-End Task Assignment
Task T-code Owner Day
Close AP OB52 type K AP Team WD+1
Close AR OB52 type D AR Team WD+1
Depreciation AFAB AA Team WD+2
FX Valuation FAGL_FCV GL Team WD+2
GR/IR review MB5S/MR11 MM Team WD+2
Accruals FB50 GL Team WD+3

EACH COMPANY CODE BALANCES INDIVIDUALLY — Task T-code Owner Day
Close AP OB52 type K AP Team WD+1
Close AR OB52 type D AR Team WD+1
Depreciation AFAB AA Team WD+2
FX Valuation FAGL_FCV GL Team WD+2
GR/IR review MB5S/MR11 MM Team WD+2
Accruals FB50 GL Team WD+3
Trial Balance F.01 Controller WD+3
Close GL OB52 type S Controller WD+4
FINANCIAL CLOSING COCKPIT = Task Manager for Period-End
In S/4HANA: Transaction FCCR (or Fiori: Closing Cockpit)
WHAT IT DOES:
Organises all closing tasks in dependency order
Assigns tasks to responsible users
Tracks completion status
Sends notifications
Provides audit trail
CLOSING TASK TYPES:
① Manual tasks (FB50 accrual posting)
② Program runs (AFAB, FAGL_FCV, FAGLGVTR)
③ Report runs (F.01, FAGLL03H)
④ External tasks (send file to auditor)
DEPENDENCY EXAMPLE:
AFAB depreciation
↓ (must complete first)
FAGL_FCV FX valuation
↓
Manual provisions
↓
Trial balance review
↓
FAGLGVTR carry-forward
↓
CLOSE PERIOD OB52
Year-End Additional Tasks
Task T-code Day
Stock count / inventory MI01/MI04/MI07 Dec 31
Impairment review ABAA (manual) Jan WD+5
Deferred tax calc FB50 manual Jan WD+6
HGB-only provisions FB50 LG=L1 Jan WD+6
Balance carry-forward FAGLGVTR Jan WD+7
E-Bilanz submission FINSC_EBILANZ Dec+12m
PH27 — Validations & Substitutions
VALIDATIONS = SAP checks your posting rules

CLOSE PERIOD OB52 — 50 manual Jan WD+6
HGB-only provisions FB50 LG=L1 Jan WD+6
Balance carry-forward FAGLGVTR Jan WD+7
E-Bilanz submission FINSC_EBILANZ Dec+12m
PH27 — Validations & Substitutions
VALIDATIONS = SAP checks your posting rules
SUBSTITUTIONS = SAP fills in fields automatically
WHEN THEY RUN:
Before posting saves → Validation → Accept or Reject
During posting → Substitution → Fill field
VALIDATION EXAMPLE:
IF CoCode = NI01
AND G/L = 500000 (Salary)
AND Cost Center is BLANK
THEN: Error message "Cost center mandatory for salaries"
SUBSTITUTION EXAMPLE:
IF CoCode = NI01
AND G/L IN (300000 – 399999) Revenue
THEN: Profit Center = REVENUE_PC (fill automatically)
T-CODES:
GGB0 = Create Validation
GGB1 = Create Substitution
OBBH = Assign Validation to CoCode
OBBZ = Assign Substitution to CoCode
THREE CALL POINTS:
1 = Document Header (before any lines)
2 = Line item level (each line individually)
3 = Complete document (all lines saved)
Common NI01 Validations to Consider
Rule Condition Action Purpose
V001 P&L G/L + no CC ERROR Force CO assignment
V002 Posting to period 13–16 WARNING Alert to audit postings
V003 Manual post to tax G/L ERROR Tax G/L = auto only
V004 Vendor invoice no reference ERROR Duplicate invoice check
S001 Revenue G/L FILL Profit Center Auto PC on revenue

3 = Complete document (all lines saved) — to period 13–16 WARNING Alert to audit postings
V003 Manual post to tax G/L ERROR Tax G/L = auto only
V004 Vendor invoice no reference ERROR Duplicate invoice check
S001 Revenue G/L FILL Profit Center Auto PC on revenue
S002 IC document FILL Trading Partner Group consolidation
PH28 — Accruals & Provisions
FBS1 — Recurring Entries
Recurring entries automate regular postings (rent, insurance, subscriptions).
ACCRUAL = Expense incurred but invoice not yet received
PROVISION = Liability for probable obligation (§249 HGB / IAS37)
ACCRUAL EXAMPLE (December electricity bill not received):
Dec 31 posting:
Dr Electricity Expense 500000 €3,000
Cr Accrued Liabilities 165000 €3,000 ← clearing account
Jan invoice arrives (MIRO):
Dr GR/IR or Expense 500000 €3,000 (actual)
Cr Vendor 160000 €3,200 (slightly different)
→ Reverse accrual: Dr Accrued 165000 | Cr Expense 500000 €3,000
→ Difference goes to next period naturally
PROVISION EXAMPLE (litigation, IAS37 / §249 HGB):
IFRS 0L: Best estimate of obligation
Dr Legal Provision Expense 550000 €50,000
Cr Legal Provision 166000 €50,000
HGB L1: May be higher (Vorsichtsprinzip)
FB50 Ledger Group L1 only:
Dr Legal Provision Expense 550000 €10,000 (additional)
Cr Legal Provision 166000 €10,000
→ 0L total: €50,000 | L1 total: €60,000

3 = Complete document (all lines saved) — ovision 166000 €50,000
HGB L1: May be higher (Vorsichtsprinzip)
FB50 Ledger Group L1 only:
Dr Legal Provision Expense 550000 €10,000 (additional)
Cr Legal Provision 166000 €10,000
→ 0L total: €50,000 | L1 total: €60,000
Accruals Engine (S/4HANA)
S/4HANA offers an Accruals Engine (ACAC) for automated accrual management.
Feature Manual (FB50) Accruals Engine
Automation Manual entry Rules-based auto
Reversal FB08 manual Automatic
Reporting ACDOCA query ACAC cockpit
Complexity Simple High-volume accruals
📚 For NI01 standard implementation: use FB50 + F.14 recurring entries. Accruals Engine for highvolume or complex requirements.
⚡ ECC → S/4HANA: Additional Differences
⚡ Profit Center Accounting (EC-PCA)
ECC (OLD)
EC-PCA = Separate profit center module Separate table: GLPCA Separate postings: 1KEK
transfer Period-end batch reconciliation needed 8A ledger for profit centers
S/4HANA (NEW)
FBS1 = Create recurring entry document
Set: First run date, interval, last run
E.g. Monthly rent €5,000
F.14 = Execute recurring entries
Selects all entries due this month
Creates actual posting documents
BKPF: doc type SA or KR
Advantage: avoids manual entry every month
Audit: recurring entry = evidence of control
→
NO separate EC-PCA in S/4HANA Profit center IN ACDOCA (PRCTR column) Real-time, same

al posting documents
BKPF: doc type SA or KR
Advantage: avoids manual entry every month
Audit: recurring entry = evidence of control
→
NO separate EC-PCA in S/4HANA Profit center IN ACDOCA (PRCTR column) Real-time, same
document No reconciliation needed 8A ledger = compatibility view
📋 CEPC (profit center master) still exists and still used. But GLPCA is now a compatibility view reading
from ACDOCA. Reports that selected FROM GLPCA must be rewritten.
🟪 Config: 1KEK (transfer posting) no longer needed. GLpca compatibility view active by default. New profit
center reports: S_E38_98000030 or FAGLL03H with PRCTR filter.
⚡ Sales Order Costing / CO-PA
ECC (OLD)
CO-PA = Profitability Analysis Costing-based CO-PA (COPA) primary Separate COPA tables:
CE1xxxx Period-end value flows Heavy customization often needed
S/4HANA (NEW)
Account-based CO-PA preferred in S/4 CO-PA data in ACDOCA (same table) Real-time SD → FI
→ CO-PA flow Costing-based COPA still possible Simplified reconciliation
📋 VBRK billing docs in your extract (10k rows): in S/4, when VF01 billing posts, ACDOCA gets both FI
fields (RACCT) AND CO-PA fields (SPART, MATKL, PRCTR) on the same row. No separate CE1
population needed for account-based COPA.

📋 VBRK bil — ling docs in your extract (10k rows): in S/4, when VF01 billing posts, ACDOCA gets both FI
fields (RACCT) AND CO-PA fields (SPART, MATKL, PRCTR) on the same row. No separate CE1
population needed for account-based COPA.
🟪 Config: SPRO → Controlling → Profitability Analysis → Flow of Actual Values → Activate Direct Posting
from FI/MM. SE16N → ACDOCA → PRCTR, SPART, MATKL fields show CO-PA dimensions.
⚡ Payment Program (F110) — SEPA
ECC (OLD)
ECC F110: generated payment file (DMEE tree) SEPA pain.001 via DMEE format tree Bank
communication via IDocs or files Payment medium workbench (PMW) common
S/4HANA (NEW)
S/4HANA F110: same core logic Enhanced SEPA direct debit (pain.008) Central Payment option
(hub) Advanced Bank Communication (ABCM) SAP Multi-Bank Connectivity (MBC)
📋 T042Z extract (payment methods T/Z) and T042z 1409 full extract show your payment method config. In
S/4 with Central Payment: all company codes can pay via one central CoCode — reduces bank accounts
needed.
→
→
🟪 Config: FBZP configuration unchanged for basic S/4. Advanced: SPRO → Financial Supply Chain
Management → Advanced Payment Management for Central Payment / MBC.
🎓 Business Process Q&A — Additional Questions
❓ What is a field status group and how does it affect posting?

🟪 Config: FBZP configuration unchanged for basic S/4 — . Advanced: SPRO → Financial Supply Chain
Management → Advanced Payment Management for Central Payment / MBC.
🎓 Business Process Q&A — Additional Questions
❓ What is a field status group and how does it affect posting?
A Field Status Group (FSG) is assigned to each G/L account in FS00 (CoCode view). It controls
whether each posting field is Required, Optional, or Suppressed when that G/L receives a posting.
Example: FSG G001 (cost accounts) makes Cost Center = Required. If you try to post to G/L
500000 (salaries with FSG G001) without entering a cost center, SAP gives an error. Posting keys
ALSO have field status — the stricter of the two always wins (Required beats Optional beats
Suppressed).
📋 G/L 500000 (Salaries), FSG = G001. FB50 posting → leave Cost Center blank → error 'Field Cost
Center required for G/L acct 500000'. OBC4 is where FSGs are defined.
💡 OBC4 = define FSG settings. FS00 CoCode view → Field Status Group field. Check: if posting
gives 'field X not ready for input' → FSG is suppressing it. Change FSG or posting key.
❓ What is FBZP and what are its 5 configuration screens?
FBZP is the central transaction for configuring the Automatic Payment Program (F110). It has
exactly 5 screens: (1) All Company Codes — which CoCodes participate as sending/paying. (2)

🎓 Business Process Q&A — Additional Questions — t are its 5 configuration screens?
FBZP is the central transaction for configuring the Automatic Payment Program (F110). It has
exactly 5 screens: (1) All Company Codes — which CoCodes participate as sending/paying. (2)
Paying Company Codes — outgoing payment allowed, minimum/maximum amounts. (3) Payment
Methods Country — method T (wire) for Germany, format pain.001. (4) Payment Methods
Company Code — per-CoCode method limits and house bank assignment. (5) Bank Determination
— ranking of house banks and accounts for payment. ALL 5 must be configured before F110 will
run.
📋 Your FBZP extracts (5 xlsx files) cover all 5 screens. FBZP Bank determination.XLSX shows the
ranking: NI01 → method T → house bank DEBA → account MAIN → G/L 100000.
💡 F110 error 'No paying company code found' = Screen 2 missing. 'No payment method possible' =
Screen 3 or 4 missing. 'No bank found' = Screen 5 missing. Work through all 5 screens in order.
❓ What happens if you forget to run FAGLGVTR at year-end?
If FAGLGVTR is not run: the P&L accounts carry over their full balance into the new year as
opening balances. This means Revenue and Expense G/Ls show prior year figures in the new
year instead of starting at zero. Balance sheet reports will be wrong because retained earnings

🎓 Business Process Q&A — Additional Questions — full balance into the new year as
opening balances. This means Revenue and Expense G/Ls show prior year figures in the new
year instead of starting at zero. Balance sheet reports will be wrong because retained earnings
(210000) won't include the prior year result. Additionally, each individual P&L account shows a
prior year opening balance which makes P&L reporting meaningless. Fix: run FAGLGVTR as soon
as discovered — it can be run multiple times (it's cumulative, not destructive). Must run separately
for 0L and L1.
📋 NI01 forgot FAGLGVTR for FY2025. In Jan 2026: FAGLL03H shows Revenue 300000 opening
balance = 500,000 (prior year). New revenue adds on top. F.01 P&L shows wrong cumulative figures.
Fix: FAGLGVTR → fiscal year 2025 → run for 0L → run for L1.
💡 FAGLGVTR is safe to run multiple times. Second run adjusts for any postings made to prior year
after first run. Check result: FS10N → 210000 → period 000 (opening balance) = prior year P&L net.
❓ What is the difference between a vendor invoice and a credit memo?
A vendor invoice (document type KR or RE) records the purchase — it creates a credit on the
vendor account (we owe money). A vendor credit memo (document type KG) records a return or

📋 NI01 forgot FAGLGVTR for FY2025. In Jan 2026: FAGLL03H shows Revenue 300000 opening — a vendor invoice and a credit memo?
A vendor invoice (document type KR or RE) records the purchase — it creates a credit on the
vendor account (we owe money). A vendor credit memo (document type KG) records a return or
correction — it creates a debit on the vendor account (vendor owes us money or reduces our
liability). In FBL1N: invoices show as positive (credit) open items, credit memos show as negative
(debit) open items. F110 payment run selects invoices for payment and nets against credit memos
automatically.
📋 You return goods worth €500 to vendor. Vendor sends credit note. Post: FB65 (credit memo entry) →
Dr Vendor 160000 €500 | Cr Expense/GR-IR 150000 €500. FBL1N: shows credit memo as negative
item against the original invoice.
💡 FB60 = vendor invoice (creates liability). FB65 = vendor credit memo (reduces liability). MIRO = PObased invoice. MR8M = reverse/cancel MIRO invoice. In F110: credit memo automatically offsets
against invoice from same vendor.
❓ What is a down payment and how is it handled differently from a normal payment?
A down payment (advance payment) is paid to a vendor BEFORE receiving goods or invoice. In
SAP it uses a Special G/L Indicator (usually 'A') to distinguish it from regular AP. This keeps it off

📋 NI01 forgot FAGLGVTR for FY2025. In Jan 2026: FAGLL03H shows Revenue 300000 opening — ly from a normal payment?
A down payment (advance payment) is paid to a vendor BEFORE receiving goods or invoice. In
SAP it uses a Special G/L Indicator (usually 'A') to distinguish it from regular AP. This keeps it off
the normal reconciliation account and prevents it from being included in payment runs accidentally.
Process: F-47 (down payment request) → F-48 (post down payment, uses special G/L) → MIRO
(invoice arrives) → F-54 (clear down payment against invoice). The down payment sits on G/L
159000 (advance payments G/L) not 160000 (regular AP recon).
📋 NI01 pays €10,000 advance to vendor for custom machinery. F-48 → Special GL A → Dr Advance
Payments 159000 €10,000 | Cr Bank 100000 €10,000. Invoice arrives: MIRO €50,000. F-54: clears
advance → net payment = €40,000.
💡 Special GL indicators in FS00 configuration: FBKP → Special GL → define accounts. 'A' = down
payment to vendor (159000). 'E' = down payment to customer (129000). Check FBL1N: filter by special
GL indicator A to see all advances.
❓ How do you handle a cross-company posting in SAP and what are the prerequisites?
A cross-company (intercompany) posting occurs when a document involves two different company
codes. Prerequisites: (1) OBY6: intercompany clearing G/L accounts defined for each pair of

159000 (advance payments G/L) not 160000 (regular AP recon). — AP and what are the prerequisites?
A cross-company (intercompany) posting occurs when a document involves two different company
codes. Prerequisites: (1) OBY6: intercompany clearing G/L accounts defined for each pair of
company codes, (2) Both G/Ls must exist in both company codes (FS00), (3) Document types
must allow cross-company (OBY6 assigns doc types). When posted, SAP automatically creates a
separate document in each company code with the IC clearing accounts balancing each side. Both
documents are linked by BVORG (cross-company reference). Each company code's Balance
Sheet stays balanced.
📋 NI01 pays DE02's office rent €2,000. FB50 → CoCode NI01 → enter lines for NI01 bank AND DE02
expense. SAP creates: NI01 doc (Dr IC-Recv 180000 | Cr Bank 100000) and DE02 doc (Dr Rent Exp |
Cr IC-Pay 190000) automatically.
💡 Error 'No intercompany G/L accounts defined' = OBY6 missing for this CoCode pair. Check: SE16N
→ T001R → company code pairs. IC G/Ls (180000/190000) must be defined in FS00 for BOTH
company codes.
📁 GitHub Table Extract Map — 61 Files
Source: https://github.com/Sk1n11/sap-fico-table-extract-for-green-field-implementation
Table Description Type Key Data Phase
T001 Company Codes Config 27 CoCodes GBGR K4 PH00
T001B Posting Period
Variants

📁 GitHub Table Extract M — ap — 61 Files
Source: https://github.com/Sk1n11/sap-fico-table-extract-for-green-field-implementation
Table Description Type Key Data Phase
T001 Company Codes Config 27 CoCodes GBGR K4 PH00
T001B Posting Period
Variants
Config Period controls per acct type PH04
T001W + T001W
Plant
Plants Config 50 plants PH17
T001k Valuation Areas Config 50 val areas (=plants in S/4) PH17
T004 Chart of
Accounts
Config GBGR COA PH01
T009 Fiscal Year
Variant
Config K4 = Jan–Dec all CoCodes PH04
SKA1 GL MASTER
LIST
G/L COA Level Master
Data
18,947 G/Ls in GBGR PH01
SKB1 GL ACCOUNT
MASTER
G/L CoCode
Level
Master
Data
53,089 records PH01
T007a Tax Keys Config German tax key definitions PH07
T007S Tax Codes Config V1/V7/A1/A7/V0 etc PH08
T030 Acct Det OBYC Config BSX/WRX/PRD etc PH09
T030k Tax Acct Det Config VST→154310/MWS→175000 PH09
TBSL Posting Keys Config 01/25/31/40/50/70/75 PH05
document types t003 Document Types Config 51 types WL/KR/AB/DZ/RV PH05
BKPF Accounting Doc
Header
Transaction 40k: WL16125 KR12286
AB9109
PH05
BSET Tax Document
Lines
Transaction Tax lines per document PH08
Acdoca 10k de02 Universal
Journal
Transaction WL5310 DZ1782 RV1444 PH00
LFB1 / LFB1
DUPCHECK
Vendor Master
CoCode
Master
Data
843 vendors DE02 PH10
active VENDOR
LFC1
Vendor
Balances

AB9109 — nsaction Tax lines per document PH08
Acdoca 10k de02 Universal
Journal
Transaction WL5310 DZ1782 RV1444 PH00
LFB1 / LFB1
DUPCHECK
Vendor Master
CoCode
Master
Data
843 vendors DE02 PH10
active VENDOR
LFC1
Vendor
Balances
Transaction Active vendor summary PH10
RBKP Invoice Receipt
Header
Transaction MIRO headers PH17
INCOMING INVOICE
RSEG
Invoice Receipt
Lines
Transaction MIRO lines with G/L PH17
EKKO PO Header Transaction PO headers PH17
T161 PO TYPES PO Types Config NB/UB etc PH17
T163 PO Item Cat Config Item category config PH17
T024E/W Purch
Org/Group
Config Purchasing org PH17
KNVV Customer Sales
Area
Master
Data
1479 customers PH11
VBRK Billing Doc
Header
Transaction 10k: F2=7393 DE02=6590 PH16
VBFA Document Flow Transaction 40k rows SD→FI PH16
TVAK Sales Order
Types
Config 156 types Z010=2368 PH16
TVAP Sales Doc Item
Cat
Config PH16
TVEP Schedule Line
Cat
Config PH16
TVFK Billing Types Config F2=std G2=credit PH16
TVKO Sales Orgs Config PH16
TVLK Delivery Types Config LF NL PH16
ANLA Asset Master Master
Data
12,819 assets DE02 PH12
ANKA Asset Classes Config 1000/1100/1200/3000/4000 PH12
ANLB Depreciation
Terms
Config Area 01 IFRS, Area 15 HGB PH12
ANEP Asset Line Items Transaction APC postings per asset PH12
T012 / House Bank
T012
House Banks Config HBKID master PH13

1479 customers PH11 — onfig 1000/1100/1200/3000/4000 PH12
ANLB Depreciation
Terms
Config Area 01 IFRS, Area 15 HGB PH12
ANEP Asset Line Items Transaction APC postings per asset PH12
T012 / House Bank
T012
House Banks Config HBKID master PH13
T012K House Bank
Accounts
Config HKTID → G/L PH13
FEBKO EBS Header Transaction Bank stmt headers PH13
EBS LINE ITEMS
FEBEP
EBS Line Items Transaction Bank stmt lines PH13
BANKING FULL
FLOW.png
Banking Flow Reference Visual diagram PH13
FBZP All company
codes
Payment
Program
Config Paying CoCodes PH14
FBZP Bank
determination
Payment
Program
Config Bank ranking PH14
FBZP Paying
company codes
Payment
Program
Config AP pay config PH14
FBZP Payment
method country
Payment
Program
Config Method T for DE PH14
Payment method
T042Z
Payment
Methods
Config T/Z/U methods PH14
Payment method in
company code
Payment
Methods
Config Per-CoCode limits PH14
T042z 1409 full
extract
Payment
Methods
Config Full method config PH14
T042a bank selection Payment
Program
Config Bank selection ranking PH14
T042e CoCode pay
method
Payment
Program
Config CoCode method PH14
Account
determination T042I
Payment
Program
Config G/L for payment PH14
FAGL_011PC FS Structure Config 12431 items IFRS+HGB PH21
GLT0 - New GL GL Totals
Legacy
Reference ECC primary, S/4 compat view PH21 /
ECC-S4

d PH14
Account
determination T042I
Payment
Program
Config G/L for payment PH14
FAGL_011PC FS Structure Config 12431 items IFRS+HGB PH21
GLT0 - New GL GL Totals
Legacy
Reference ECC primary, S/4 compat view PH21 /
ECC-S4
TKA01 Controlling
Areas
Config GBGR controlling area PH15
CSKS Cost Center
Master
Master
Data
Cost centers PH15
CEPC Profit Center
Master
Master
Data
Profit center hierarchy PH15
ZFI COGS Custom COGS
Report
Custom ZFI_COGS_ACCOUNT
program
PH16
🟢 Go-Live Readiness Checklist
✅ NI01 GO-LIVE READINESS
FOUNDATION:
☐ T001: NI01 created · COA NIOP · K4 variant assigned
☐ SKA1 + SKB1: all key G/Ls created and typed correctly
☐ Ledgers 0L + L1 active and tested in ACDOCA
☐ OB53: P&L type X → 210000 Retained Earnings
☐ OB52: go-live period open
TAX:
☐ TAXD procedure assigned to country DE (OBBG)
☐ Tax codes V1/V7/A1/A7/V0 created in FTXP
☐ T030k: VST→154310, MWS→175000
☐ BSET tested: tax document lines exist after posting
ACCOUNTS PAYABLE:
☐ LFB1: vendors created with AKONT=160000 + REPRF set
☐ FBZP: all 5 screens configured
☐ F110 test payment run executed and cleared
☐ SEPA pain.001 format validated with bank
ACCOUNTS RECEIVABLE:
☐ KNVV: customers with AKONT=120000
☐ VKOA: revenue account determination tested
☐ FBL5N: customer open item visible after billing

✅ NI01 GO-LIVE READINESS — run executed and cleared
☐ SEPA pain.001 format validated with bank
ACCOUNTS RECEIVABLE:
☐ KNVV: customers with AKONT=120000
☐ VKOA: revenue account determination tested
☐ FBL5N: customer open item visible after billing
☐ F-28 / FEBAN: clearing tested
ASSET ACCOUNTING:
☐ ANKA: asset classes created
☐ AO90: account determination per class
☐ ANLB: dep areas 01 (IFRS) + 15 (HGB) configured
☐ AFAB: test run clean · ACDOCA 0L+L1 rows exist
☐ AW01N: both areas visible per asset
BANK:
☐ T012 house bank + T012K account → G/L 100000
☐ EBS: account symbols + posting rules + algorithms
☐ FEBAN: test bank statement imported and cleared
☐ Bank clearing 100010 = zero at end of test
CO / SD / MM:
☐ GBGR controlling area verified
☐ OKB9: default account assignments for P&L G/Ls
☐ OBYC: GR/IR chain tested end-to-end
☐ VKOA: SD billing → revenue → ACDOCA
PARALLEL ACCOUNTING:
☐ L1-only adjustment posting tested (FB50 ledger L1)
☐ AFAB: different depreciation 0L vs L1 confirmed
☐ F.01: IFRS Balance Sheet (0L) + HGB Balance Sheet (L1)
NI01 S/4HANA FICO Greenfield Book v2 · 61 Real Table Extracts · Mobile-Responsive · ECC→S/4HANA · New
GL · 40 BPQs
S/4HANA On-Premise / Private Cloud · Company Code NI01 · Germany · EUR · NIOP · K4
Teaching values «…» — replace with customer values at go-live

1 Real Table Extracts · Mobile-Responsive · ECC→S/4HANA · New
GL · 40 BPQs
S/4HANA On-Premise / Private Cloud · Company Code NI01 · Germany · EUR · NIOP · K4
Teaching values «…» — replace with customer values at go-live
☐ FAGL_011PC: all G/Ls mapped to FS structure nodes
ACDOCA FINAL VERIFICATION:
☐ RLDNR = 0L rows exist for all transaction types
☐ RLDNR = L1 rows exist for parallel postings
☐ KOSTL populated on all P&L G/L postings
☐ ACDOCA reconciles to F.01 trial balance
🟢 GO LIVE ✓