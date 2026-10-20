# Interview screenshot 2026-10-17.jpg

Topic: Screenshots

[Local OCR · confidence 48%]
AP O0@ - NO ®Li017%
Whatis a Reconciliation Account?
Thi oft sa translator
Howit works — in el me
Ap sub ledgr Recontiaton Account po
21000 Ss Hoot
Total: € 10,500 do €10500
Suledger total aways = GL balance
The 3 mai Reconliaion Accounts
AE Yon Ter a
ep
The golden ue
ONrcnsenunes

[Structured understanding of this image]
### 🖼️ WHAT THE IMAGE SAYS
- AP O0@ - NO ®Li017%
- Whatis a Reconciliation Account?
- Thi oft sa translator
- Howit works — in el me
- Ap sub ledgr Recontiaton Account po
- 21000 Ss Hoot
- Total: € 10,500 do €10500
- Suledger total aways = GL balance
- The 3 mai Reconliaion Accounts
- AE Yon Ter a
- The golden ue
- ONrcnsenunes
- **SAP objects detected:** LI017.
- **Amounts / rates detected:** € 10,500, €105.
### 🗣️ DIRECT ANSWER TO SPEAK NOW
- **Core Concept:** A ledger is a complete set of books for one accounting principle. In S/4HANA I post once into ACDOCA and the leading and non-leading ledgers receive their valuation in the same document, so IFRS group reporting and local HGB/statutory books stay reconciled by design.

🗣️ DIRECT ANSWER TO SPEAK NOW — unting principle. In S/4HANA I post once into ACDOCA and the leading and non-leading ledgers receive their valuation in the same document, so IFRS group reporting and local HGB/statutory books stay reconciled by design.
- **Key System Benefit:** ACDOCA removes the old FI/CO reconciliation problem: GL, CO, asset and margin characteristics sit on one line item, and extension ledgers can carry management adjustments without changing the primary posting.
- **Execution Strategy:** FINSC_LEDGER defines the ledger set, accounting principles bind each ledger to its valuation rule, ledger groups control which company codes post where, and document splitting keeps balance-sheet characteristics zero-balanced.
- **Scenario Figures I Will Use:** € 10,500, €105. I keep the same figures through the posting, clearing and test steps; if a rate or account is not given, I state it as an explicit assumption rather than inventing a project value.
- **Objects Detected In The Question/Image:** LI017.

### 📊 ARCHITECTURAL FLOW
```text
1. POSTING FB50 · FB60 · MIRO
 one business document enters Finance
 ↓
2. LEDGER ENGINE FINSC_LEDGER
 leading and non-leading ledgers selected
 ↓
3. JOURNAL ACDOCA
 one line per ledger, account and characteristic
 ↓
4. REPORTING FAGLL03 · Fiori

📊 ARCHITECTURAL FLOW — MIRO
 one business document enters Finance
 ↓
2. LEDGER ENGINE FINSC_LEDGER
 leading and non-leading ledgers selected
 ↓
3. JOURNAL ACDOCA
 one line per ledger, account and characteristic
 ↓
4. REPORTING FAGLL03 · Fiori
 local and group views read the same document
```

### ⚙️ CONFIG STEPS
1. **FINSC_LEDGER** — define ledgers, accounting principles and ledger groups · Example: 0L for IFRS leading ledger and a non-leading ledger for HGB/local GAAP · Ref: ledger-design sheet; SPRO ▸ Financial Accounting ▸ Financial Accounting Global Settings ▸ Ledgers.
2. **OBY6** — assign the company code currency, fiscal-year variant and posting-period variant · Example: German company code reports EUR locally while the group reads the same ACDOCA document under IFRS · Ref: company-code global-parameter sheet; SPRO ▸ Financial Accounting Global Settings.
3. **FAGL_ACTIVATION** — confirm New GL/document-splitting activation in an ECC conversion context · Example: Segment and profit-center splitting are active before the first productive posting · Ref: conversion readiness checklist; SPRO ▸ Financial Accounting ▸ General Ledger Accounting.
4.

⚙️ CONFIG STEPS — n an ECC conversion context · Example: Segment and profit-center splitting are active before the first productive posting · Ref: conversion readiness checklist; SPRO ▸ Financial Accounting ▸ General Ledger Accounting.
4. **OB52** — open and close posting periods by account type and company code · Example: Only the current period stays open for users; special periods are restricted to the close team · Ref: period-close calendar; SPRO ▸ Financial Accounting Global Settings ▸ Document ▸ Posting Periods.
5. **FS00** — maintain the G/L account and its field-status, tax and open-item behaviour · Example: A balance-sheet clearing account is open-item managed; a revenue account carries the correct tax category · Ref: chart-of-accounts governance list; SAP GUI ▸ Accounting ▸ Financial Accounting ▸ General Ledger ▸ Master Records.
6. **FAGLFLEXT / ACDOCA** — prove totals and line items after posting · Example: The local and leading ledger show the same document number with their own valuation lines · Ref: reconciliation evidence pack; SE16H on ACDOCA.

### 🔧 DROP THESE OBJECT NAMES
- **FINSC_LEDGER** — ledger and accounting-principle setup.
- **ACDOCA** — Universal Journal line items.
- **OB52** — posting-period control.
- **FS00** — G/L master maintenance.

⚙️ CONFIG STEPS — ACDOCA.

### 🔧 DROP THESE OBJECT NAMES
- **FINSC_LEDGER** — ledger and accounting-principle setup.
- **ACDOCA** — Universal Journal line items.
- **OB52** — posting-period control.
- **FS00** — G/L master maintenance.
- **FAGLL03** — ledger-specific line-item display.
- **OBBH** — substitution rules when a field must be derived.

### 🧾 ACCOUNTING ENTRIES
- Dr Expense € 10,500 / Cr Vendor or bank € 10,500 — same document creates the required ledger lines.
- Dr Depreciation expense € 10,500 / Cr Accumulated depreciation € 10,500 — asset depreciation posts by depreciation area and ledger.
- Dr Foreign-currency revaluation € 10,500 / Cr Balance-sheet adjustment € 10,500 — FAGL_FCV at period end, reversed or carried by design.

### 🧪 HOW TO TEST IT
1. Post FB50 with two ledgers active and inspect ACDOCA for document, ledger, account, profit center and segment.
2. Run FAGLL03 for the non-leading ledger and agree it to the local trial balance.
3. Post a document-splitting case and confirm every balance-sheet characteristic nets to zero.
4. Close and reopen a test period in OB52 and prove user postings are blocked outside the allowed window.

### 🪤 TRAPS
- Trap: Calling a ledger an accounting principle.

🧪 HOW TO TEST IT — m every balance-sheet characteristic nets to zero.
4. Close and reopen a test period in OB52 and prove user postings are blocked outside the allowed window.

### 🪤 TRAPS
- Trap: Calling a ledger an accounting principle. → Winning line: Winning line: the principle is the valuation rule; the ledger is the book where that rule posts.
- Trap: Saying S/4 still reconciles FI and CO at month-end. → Winning line: Winning line: ACDOCA carries both views in one line; close becomes review and valuation, not reconciliation.

### 🎯 IF MY MIND GOES BLANK
One posting, every book. FINSC_LEDGER defines the ledgers, ACDOCA stores the lines, and local plus group reporting read the same document.

### 🔗 CROSS-RELATED — FIXED, READY TO ASK NEXT
- HGB vs IFRS — how do parallel ledgers answer both from one document?
- How will you set up a company code for a new-country rollout?
- How does the Universal Journal (ACDOCA) change the month-end close?