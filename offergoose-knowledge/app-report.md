# OfferGoose - automatic app report

App version: 2.60.0
Generated: 2026-10-20T05:23:58.305Z
AI providers with a saved key: groq, gemini, openrouter, custom

Every question, answer, AI-review verdict and app event below is exactly what the app produced. API keys are redacted and never leave the phone.

## 1. [2026-10-18T09:35:35.673Z] github-fetch

Fetched from Sk1n11/Goose: {"owner":"Sk1n11","repo":"Goose","branch":"main","folder":"offergoose-knowledge","files":1,"answers":0,"catalog":1,"fetched":["ilide.info-sap-fi-document-pr_20110aa61a097f28b904f3b61d44c276.pdf"],"skipped":0,"failed":[],"notes":["No offergoose-knowledge/ folder in the repo yet — Publish once (token below) to create it; fetching then becomes automatic."]} | KB now: 329 sources, 162 answers

## 2. [2026-10-18T09:35:39.451Z] free-database-fetch

Online free sources fetched: {"total":15,"fetched":2,"skipped":11,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"sources":2},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"sources":56},{"name":"SAP FICO tutorials — full index (TutorialsPoint)","ok" | KB now: 386 sources, 162 answers

## 3. [2026-10-18T12:26:33.461Z] free-database-fetch

Online free sources fetched: {"total":17,"fetched":2,"skipped":13,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 387 sources, 147 answers

## 4. [2026-10-18T12:33:27.278Z] answer

Q: How do you design FI-MM and FI-SD integration and Material Ledger actual costing in S/4HANA
Scrutiny: all parameters pass
A: ### 🗣️ DIRECT ANSWER TO SPEAK NOW
“I test integration as a business-document chain, not as a list of transactions. I start from the approved organizational/configuration mapping, post the source document, then reconcile the subledger, G/L and controlling impact at each hand-off. For FI–MM that is PO → GR → invoice → payment; for FI–SD it is order → delivery/PGI → billing → receipt; for FI–PP it is component issue → confirmation → finished-goods receipt → settlement. I prove each FI document in **FB03/ACDOCA** and trace failures to account determination, master data, pricing/tax, period or authorization. Project org values stay To Be Confirmed unless the uploaded signed-off document confirms them.”

### 📊 ARCHITECTURAL FLOW
```text
FI-MM · procure to pay
ME21N PO → MIGO 101 GR → MIRO invoice → F110 payment
 ↓
 ME23N + WRX reconciliation
FI-SD · order to cash
VA01 order → VL02N PGI → VF01 billing → F-28 receipt
 ↓
 VF03 + VKOA + ACDOCA
```

### ⚙️ CONFIG STEPS
1. **OBYC** — map valuation class/transaction keys **BSX, WRX, GBB, PRD** to approved G/Ls. Example: stock GR debits inventory and credits GR/IR. Where: SPRO ▸ Materials Management ▸ Valuation and Account Assignment ▸ Account Determination ▸ Configure Automatic Postings. Reference: MM account-determination workbook; test with **ME21N/MIGO/MIRO**.
2. **OMR6** — set invoice quantity/price tolerance and block behavior. Example: an out-of-tolerance MIRO invoice is blocked for AP/buyer review. Reference: signed LIV tolerance matrix; exact thresholds remain To Be Confirmed until approved.
3. **VKOA** — determine revenue G/L from chart of accounts, sales organization, customer/material account-assignment groups and account key (for example **ERL**). Where: SPRO ▸ Sales and Distribution ▸ Basic Functions ▸ Account Assignment/Costing ▸ Revenue Account Determination. Reference: SD revenue-account mapping; validate through **VF01/VF03**.
4. **OB40** — map tax account keys to input/output-tax G/Ls for the configured tax procedure. Example: the billing tax line credits the approved output-tax account. Reference: country tax design / tax-account matrix; rates and accounts are jurisdiction-specific.
6. **OX10 / OX17 / OBY6** — verify the approved plant, plant-to-company-code assignment and company-code parameters before testing. Example: plant/company-code pairing must match the signed-off organization structure. Reference: project organization-structure section; never copy another blueprint’s values.

### 🔧 DROP THESE OBJECT NAMES
- **OBYC · BSX / WRX / GBB / PRD** — MM stock, clearing, consumption and price-difference postings.
- **VKOA · ERL / account key** — SD revenue account determination at billing.
- **OB40 · tax account key** — tax G/L assignment; rate comes from the tax procedure/code.
- **ACDOCA** — S/4HANA Universal Journal evidence for FI/CO line items and account assignments.

### 🧾 ACCOUNTING ENTRIES
**FI–MM · illustrative stock PO, €100 net + €19 input VAT:**
- MIGO 101: Dr Inventory (BSX) €100 / Cr GR/IR (WRX) €100.
- MIRO: Dr GR/IR €100 + Dr Input VAT €19 / Cr Vendor €119.
- F110 payment: Dr Vendor €119 / Cr Bank-clearing €119.
**FI–SD · illustrative €100 sale + €19 output VAT; €70 cost:**
- PGI 601: Dr COGS €70 / Cr Inventory €70 (account determination per OBYC).
- VF01 billing: Dr Customer €119 / Cr Revenue €100 / Cr Output VAT €19 (VKOA plus tax account determination).
- F-28 receipt: Dr Bank €119 / Cr Customer €119.

### 🧪 HOW TO TEST IT
1. **P2P:** ME21N create a controlled PO → MIGO 101 → MIRO → F110. At each step capture document number; inspect **ME23N**, **MIR4**, **FB03**, **FBL3N (WRX)** and vendor items in **FBL1N**. Reconcile GR/IR; test partial GR, partial invoice, price variance, reversal and blocked invoice (**MRBR**).
2. **O2C:** VA01 order → delivery/PGI in **VL02N** → billing **VF01** → incoming receipt **F-28**. Inspect document flow **VA03**, billing **VF03**, FI document **FB03**, customer items **FBL5N**, revenue/tax/COGS lines and profit center in **ACDOCA**. Test returns/credit memo and tax/pricing edge cases.
4. For every chain, reconcile source quantity/value to the FI/CO totals, capture evidence, test one negative case and reversal, and trace any failure through **SLG1**, **ST22**, **SU53** and the relevant document flow before sign-off.

### 🪤 TRAPS
- **VA01** and a production-order creation do not themselves guarantee an FI posting; billing, PGI, goods movements and settlement are the accounting triggers.
- Do not confuse **GR/IR (WRX)** with the vendor reconciliation account, or revenue determination (**VKOA**) with tax determination (**OB40**).
- Reconcile partial quantities, tax, currency, pricing, account assignment and period status; do not force-clear a variance to make a test pass.
- Org units, tax rates, G/L numbers, settlement receivers and project-specific design values must come from the signed-off documents; otherwise mark To Be Confirmed.

### 🎯 IF MY MIND GOES BLANK
“I follow the source document to its accounting trigger, verify OBYC or VKOA, inspect the FI/CO lines in F

## 5. [2026-10-18T12:33:31.374Z] answer

Q: How do you design FI-MM and FI-SD integration and Material Ledger actual costing in S/4HANA
Scrutiny: all parameters pass
A: ### 💡 SAY THIS FIRST
> “I test integration as a business-document chain, not as a list of transactions

### 🗣️ DIRECT ANSWER TO SPEAK NOW
“I test integration as a business-document chain, not as a list of transactions. I start from the approved organizational/configuration mapping, post the source document, then reconcile the subledger, G/L and controlling impact at each hand-off. For FI–MM that is PO → GR → invoice → payment; for FI–SD it is order → delivery/PGI → billing → receipt; for FI–PP it is component issue → confirmation → finished-goods receipt → settlement. I prove each FI document in **FB03/ACDOCA** and trace failures to account determination, master data, pricing/tax, period or authorization. Project org values stay To Be Confirmed unless the uploaded signed-off document confirms them.”

### 📊 ARCHITECTURAL FLOW
```text
FI-MM · procure to pay
ME21N PO → MIGO 101 GR → MIRO invoice → F110 payment
 ↓
 ME23N + WRX reconciliation
FI-SD · order to cash
VA01 order → VL02N PGI → VF01 billing → F-28 receipt
 ↓
 VF03 + VKOA + ACDOCA
```

### ⚙️ CONFIG STEPS
1. **OBYC** — map valuation class/transaction keys **BSX, WRX, GBB, PRD** to approved G/Ls. Example: stock GR debits inventory and credits GR/IR. Where: SPRO ▸ Materials Management ▸ Valuation and Account Assignment ▸ Account Determination ▸ Configure Automatic Postings. Reference: MM account-determination workbook; test with **ME21N/MIGO/MIRO**.
2. **OMR6** — set invoice quantity/price tolerance and block behavior. Example: an out-of-tolerance MIRO invoice is blocked for AP/buyer review. Reference: signed LIV tolerance matrix; exact thresholds remain To Be Confirmed until approved.
3. **VKOA** — determine revenue G/L from chart of accounts, sales organization, customer/material account-assignment groups and account key (for example **ERL**). Where: SPRO ▸ Sales and Distribution ▸ Basic Functions ▸ Account Assignment/Costing ▸ Revenue Account Determination. Reference: SD revenue-account mapping; validate through **VF01/VF03**.
4. **OB40** — map tax account keys to input/output-tax G/Ls for the configured tax procedure. Example: the billing tax line credits the approved output-tax account. Reference: country tax design / tax-account matrix; rates and accounts are jurisdiction-specific.
6. **OX10 / OX17 / OBY6** — verify the approved plant, plant-to-company-code assignment and company-code parameters before testing. Example: plant/company-code pairing must match the signed-off organization structure. Reference: project organization-structure section; never copy another blueprint’s values.

### 🔧 DROP THESE OBJECT NAMES
- **OBYC · BSX / WRX / GBB / PRD** — MM stock, clearing, consumption and price-difference postings.
- **VKOA · ERL / account key** — SD revenue account determination at billing.
- **OB40 · tax account key** — tax G/L assignment; rate comes from the tax procedure/code.
- **ACDOCA** — S/4HANA Universal Journal evidence for FI/CO line items and account assignments.
- **OB08** — used in my material on this topic
- **OB52** — used in my material on this topic
- **OB09** — used in my material on this topic
- **OB10** — used in my material on this topic
### 🧾 ACCOUNTING ENTRIES
**FI–MM · illustrative stock PO, €100 net + €19 input VAT:**
- MIGO 101: Dr Inventory (BSX) €100 / Cr GR/IR (WRX) €100.
- MIRO: Dr GR/IR €100 + Dr Input VAT €19 / Cr Vendor €119.
- F110 payment: Dr Vendor €119 / Cr Bank-clearing €119.
**FI–SD · illustrative €100 sale + €19 output VAT; €70 cost:**
- PGI 601: Dr COGS €70 / Cr Inventory €70 (account determination per OBYC).
- VF01 billing: Dr Customer €119 / Cr Revenue €100 / Cr Output VAT €19 (VKOA plus tax account determination).
- F-28 receipt: Dr Bank €119 / Cr Customer €119.

### 🧪 HOW TO TEST IT
1. **P2P:** ME21N create a controlled PO → MIGO 101 → MIRO → F110. At each step capture document number; inspect **ME23N**, **MIR4**, **FB03**, **FBL3N (WRX)** and vendor items in **FBL1N**. Reconcile GR/IR; test partial GR, partial invoice, price variance, reversal and blocked invoice (**MRBR**).
2. **O2C:** VA01 order → delivery/PGI in **VL02N** → billing **VF01** → incoming receipt **F-28**. Inspect document flow **VA03**, billing **VF03**, FI document **FB03**, customer items **FBL5N**, revenue/tax/COGS lines and profit center in **ACDOCA**. Test returns/credit memo and tax/pricing edge cases.
4. For every chain, reconcile source quantity/value to the FI/CO totals, capture evidence, test one negative case and reversal, and trace any failure through **SLG1**, **ST22**, **SU53** and the relevant document flow before sign-off.

### 🪤 TRAPS
- **VA01** and a production-order creation do not themselves guarantee an FI posting; billing, PGI, goods movements and settlement are the accounting triggers.
- Do not confuse **GR/IR (WRX)** with the vendor reconciliation account, or revenue determination (**VKOA**) with tax determination (**OB40**).
- Reconcile partial quantities, tax, currency, pricing, account assignment and period status; do not force-clear a variance to make a test pass.
- Org unit

## 6. [2026-10-18T12:33:43.169Z] answer

Q: How do you design FI-MM and FI-SD integration and Material Ledger actual costing in S/4HANA
Scrutiny: all parameters pass
A: ### 💡 SAY THIS FIRST
> “I test integration as a business-document chain, not as a list of transactions

### 🗣️ DIRECT ANSWER TO SPEAK NOW
“I test integration as a business-document chain, not as a list of transactions. I start from the approved organizational/configuration mapping, post the source document, then reconcile the subledger, G/L and controlling impact at each hand-off. For FI–MM that is PO → GR → invoice → payment; for FI–SD it is order → delivery/PGI → billing → receipt; for FI–PP it is component issue → confirmation → finished-goods receipt → settlement. I prove each FI document in **FB03/ACDOCA** and trace failures to account determination, master data, pricing/tax, period or authorization. Project org values stay To Be Confirmed unless the uploaded signed-off document confirms them.”

### 📊 ARCHITECTURAL FLOW
```text
FI-MM · procure to pay
ME21N PO → MIGO 101 GR → MIRO invoice → F110 payment
 ↓
 ME23N + WRX reconciliation
FI-SD · order to cash
VA01 order → VL02N PGI → VF01 billing → F-28 receipt
 ↓
 VF03 + VKOA + ACDOCA
```

### ⚙️ CONFIG STEPS
1. **OBYC** — map valuation class/transaction keys **BSX, WRX, GBB, PRD** to approved G/Ls. Example: stock GR debits inventory and credits GR/IR. Where: SPRO ▸ Materials Management ▸ Valuation and Account Assignment ▸ Account Determination ▸ Configure Automatic Postings. Reference: MM account-determination workbook; test with **ME21N/MIGO/MIRO**.
2. **OMR6** — set invoice quantity/price tolerance and block behavior. Example: an out-of-tolerance MIRO invoice is blocked for AP/buyer review. Reference: signed LIV tolerance matrix; exact thresholds remain To Be Confirmed until approved.
3. **VKOA** — determine revenue G/L from chart of accounts, sales organization, customer/material account-assignment groups and account key (for example **ERL**). Where: SPRO ▸ Sales and Distribution ▸ Basic Functions ▸ Account Assignment/Costing ▸ Revenue Account Determination. Reference: SD revenue-account mapping; validate through **VF01/VF03**.
4. **OB40** — map tax account keys to input/output-tax G/Ls for the configured tax procedure. Example: the billing tax line credits the approved output-tax account. Reference: country tax design / tax-account matrix; rates and accounts are jurisdiction-specific.
6. **OX10 / OX17 / OBY6** — verify the approved plant, plant-to-company-code assignment and company-code parameters before testing. Example: plant/company-code pairing must match the signed-off organization structure. Reference: project organization-structure section; never copy another blueprint’s values.

### 🔧 DROP THESE OBJECT NAMES
- **OBYC · BSX / WRX / GBB / PRD** — MM stock, clearing, consumption and price-difference postings.
- **VKOA · ERL / account key** — SD revenue account determination at billing.
- **OB40 · tax account key** — tax G/L assignment; rate comes from the tax procedure/code.
- **ACDOCA** — S/4HANA Universal Journal evidence for FI/CO line items and account assignments.
- **OB08** — used in my material on this topic
- **OB52** — used in my material on this topic
- **OB09** — used in my material on this topic
- **OB10** — used in my material on this topic
### 🧾 ACCOUNTING ENTRIES
**FI–MM · illustrative stock PO, €100 net + €19 input VAT:**
- MIGO 101: Dr Inventory (BSX) €100 / Cr GR/IR (WRX) €100.
- MIRO: Dr GR/IR €100 + Dr Input VAT €19 / Cr Vendor €119.
- F110 payment: Dr Vendor €119 / Cr Bank-clearing €119.
**FI–SD · illustrative €100 sale + €19 output VAT; €70 cost:**
- PGI 601: Dr COGS €70 / Cr Inventory €70 (account determination per OBYC).
- VF01 billing: Dr Customer €119 / Cr Revenue €100 / Cr Output VAT €19 (VKOA plus tax account determination).
- F-28 receipt: Dr Bank €119 / Cr Customer €119.

### 🧪 HOW TO TEST IT
1. **P2P:** ME21N create a controlled PO → MIGO 101 → MIRO → F110. At each step capture document number; inspect **ME23N**, **MIR4**, **FB03**, **FBL3N (WRX)** and vendor items in **FBL1N**. Reconcile GR/IR; test partial GR, partial invoice, price variance, reversal and blocked invoice (**MRBR**).
2. **O2C:** VA01 order → delivery/PGI in **VL02N** → billing **VF01** → incoming receipt **F-28**. Inspect document flow **VA03**, billing **VF03**, FI document **FB03**, customer items **FBL5N**, revenue/tax/COGS lines and profit center in **ACDOCA**. Test returns/credit memo and tax/pricing edge cases.
4. For every chain, reconcile source quantity/value to the FI/CO totals, capture evidence, test one negative case and reversal, and trace any failure through **SLG1**, **ST22**, **SU53** and the relevant document flow before sign-off.

### 🪤 TRAPS
- **VA01** and a production-order creation do not themselves guarantee an FI posting; billing, PGI, goods movements and settlement are the accounting triggers.
- Do not confuse **GR/IR (WRX)** with the vendor reconciliation account, or revenue determination (**VKOA**) with tax determination (**OB40**).
- Reconcile partial quantities, tax, currency, pricing, account assignment and period status; do not force-clear a variance to make a test pass.
- Org unit

## 7. [2026-10-18T12:34:03.253Z] ai-review-applied

Q: How do you design FI-MM and FI-SD integration and Material Ledger actual costing in S/4HANA | reviewers: gemini
A: ### 💡 SAY THIS FIRST
> I design FI-MM, FI-SD integration and Material Ledger actual costing in S/4HANA as an integrated value flow centered on the Universal Journal

### DIRECT ANSWER TO SPEAK NOW
"I design FI-MM, FI-SD integration and Material Ledger actual costing in S/4HANA as an integrated value flow centered on the Universal Journal. For FI-MM, I drive automatic account determination via transaction OBYC—mapping BSX for inventory balance, WRX for GR/IR clearing, and PRD for purchase price variance. For FI-SD, I govern revenue recognition and cost of goods sold via VKOA for revenue/deductions and OBYC GBB-VAX for standard cost delivery.

In S/4HANA, Material Ledger is mandatory for inventory valuation, but actual costing with price determination 3 remains an architectural choice. I implement standard price control 'S' with price determination 3, activate actual costing via transactions OMX1, OMX2, and OMX3, and assign dynamic currency types mirroring the leading and non-leading ledgers in ACDOCA. At period close, I run actual costing cockpit CKMLCP to collect single-level procurement variances and roll multilevel production variances up the BOM structure. The system calculates the Periodic Unit Price, settles remaining variances between ending inventory and COGS, and revalues ending balance sheets without artificial manual adjustments."

### ARCHITECTURAL FLOW
```
[PO: ME21N] Net €100 / Unit
[GR: MIGO 101] > Dr BSX (Inventory) €100 / Cr WRX (GR/IR) €100
[IR: MIRO] @ €120 > Dr WRX €100 + Dr PRD €20 + Dr Input VAT €22.80 / Cr Vendor €142.80
├
→ →
[Sales Order: VA01] [Period-End ML: CKMLCP]
→ →
[PGI: VL02N (601)] Allocate Single/Multilevel
Dr COGS (GBB-VAX) €100 Variances (€20 PRD):
Cr Inventory (BSX) €100 - To Consumed COGS (€10)
        ↓
1.
   - To Ending Inventory (€10)
   [Billing: VF01] →
   Dr Customer €178.50 New Periodic Unit Price:
   Cr Revenue (VKOA-ERL) €150 PUP = €120/unit
   Cr Output VAT (MWS) €28.50
```

### CONFIG STEPS
1. **OMSK / OBYC (Account Determination Configuration)**: Define valuation classes via OMSK and link valuation groupings, transaction keys (BSX, WRX, PRD, GBB), and account modifications to target G/L accounts in OBYC. Example: Plant valuation area mapped to Valuation Grouping Code 0001; Transaction WRX mapped to GR/IR Clearing Account 211000.
2. **VKOA (SD Revenue Account Determination)**: Define access sequences and assign G/L accounts using condition type, chart of accounts, sales organization, customer account assignment group, material account assignment group, and account key. Example: Table 001 mapped for App 'V', CondType 'KOFI', ChAc 'CAUS', SOrg '1000', AcctKey 'ERL' to Revenue Account 410000.
3. **OMX2 / OMX3 (Material Ledger Type & Valuation Area Assignment)**: Define the Material Ledger Type in OMX2 specifying currency types (e.g., 10 Company Code Currency, 30 Group Currency) and currency base. In OMX3, assign the Material Ledger Type to each active plant/valuation area.
4. **OMX1 (Activate Material Ledger)**: Activate the Material Ledger per valuation area. Select price determination '3' (Single-/Multilevel) and activate 'Price Det. Binding' to ensure all newly created materials inherit actual costing capability.
5. **CKML41 / CKMLCP (Actual Costing Cockpit Configuration)**: Define the costing run templates and configure settlement rules for Actual Costing closing entries. Set up the revaluation of consumption settings in OBYC under transaction key COC (Revaluation of Other Consumption) and GBB/COC for COGS revaluation.

### DROP THESE OBJECT NAMES
- **OBYC**
- **VKOA**
- **OMX1**
- **OMX2**
- **OMX3**
- **CKMLCP**
- **ACDOCA**
- **CK11N**
- **CK24**
- **MRBR**

### ACCOUNTING ENTRIES
*Consistent numeric baseline: Purchase Order created for 2 units at standard price €100/unit. Invoice arrives at €120/unit. 1 unit is sold to an external customer for €150 (VAT 19%). 1 unit remains in ending inventory.*

1. **Goods Receipt (MIGO - 2 Units received against PO @ standard €100):**
   - Dr Balance Sheet Inventory (OBYC-BSX): €200.00 (2 units × €100.00 standard cost)
   - Cr GR/IR Clearing Account (OBYC-WRX): €200.00 (Obligation to vendor for 2 units delivered)
   - *Remainder to invoice: 2 units / €200.00.*

2. **Invoice Receipt (MIRO - Vendor invoices 2 Units @ actual €120 + 19% VAT):**
   - Actual material value = 2 units × €120.00 = €240.00.
   - Price Variance Formula:
     $$\text{PRD} = (\text{Actual Price} - \text{Standard Price}) \times \text{Quantity} = (€120.00 - €100.00) \times 2 = €40.00$$
   - Total Net Invoice = €240.00; Total VAT (19%) = €45.60; Total Gross = €285.60.
   - Dr GR/IR Clearing Account (OBYC-WRX): €200.00 (Clears original receipt liability; remaining GR/IR balance: €0.00)
   - Dr Purchase Price Variance (OBYC-PRD): €40.00 (Unfavorable purchase price difference captured in ML)
   - Dr Input Tax Recoverable (OB40-VST): €45.60 (19% VAT on €240.00)
   - Cr Vendor Open Item: €285.60 (Accounts Payable liability)

3. **Post Goods Issue (VL02N - 1 Unit shipped for Sales Order):**
   - Dr Cost of Goods Sold (OBYC-GBB-VAX): €10

## 8. [2026-10-18T12:34:03.269Z] answer

Q: How do you design FI-MM and FI-SD integration and Material Ledger actual costing in S/4HANA
Scrutiny: all parameters pass
A: ### 💡 SAY THIS FIRST
> I design FI-MM, FI-SD integration and Material Ledger actual costing in S/4HANA as an integrated value flow centered on the Universal Journal

### DIRECT ANSWER TO SPEAK NOW
"I design FI-MM, FI-SD integration and Material Ledger actual costing in S/4HANA as an integrated value flow centered on the Universal Journal. For FI-MM, I drive automatic account determination via transaction OBYC—mapping BSX for inventory balance, WRX for GR/IR clearing, and PRD for purchase price variance. For FI-SD, I govern revenue recognition and cost of goods sold via VKOA for revenue/deductions and OBYC GBB-VAX for standard cost delivery.

In S/4HANA, Material Ledger is mandatory for inventory valuation, but actual costing with price determination 3 remains an architectural choice. I implement standard price control 'S' with price determination 3, activate actual costing via transactions OMX1, OMX2, and OMX3, and assign dynamic currency types mirroring the leading and non-leading ledgers in ACDOCA. At period close, I run actual costing cockpit CKMLCP to collect single-level procurement variances and roll multilevel production variances up the BOM structure. The system calculates the Periodic Unit Price, settles remaining variances between ending inventory and COGS, and revalues ending balance sheets without artificial manual adjustments."

### ARCHITECTURAL FLOW
```
[PO: ME21N] Net €100 / Unit
[GR: MIGO 101] > Dr BSX (Inventory) €100 / Cr WRX (GR/IR) €100
[IR: MIRO] @ €120 > Dr WRX €100 + Dr PRD €20 + Dr Input VAT €22.80 / Cr Vendor €142.80
├
→ →
[Sales Order: VA01] [Period-End ML: CKMLCP]
→ →
[PGI: VL02N (601)] Allocate Single/Multilevel
Dr COGS (GBB-VAX) €100 Variances (€20 PRD):
Cr Inventory (BSX) €100 - To Consumed COGS (€10)
        ↓
1.
   - To Ending Inventory (€10)
   [Billing: VF01] →
   Dr Customer €178.50 New Periodic Unit Price:
   Cr Revenue (VKOA-ERL) €150 PUP = €120/unit
   Cr Output VAT (MWS) €28.50
```

### CONFIG STEPS
1. **OMSK / OBYC (Account Determination Configuration)**: Define valuation classes via OMSK and link valuation groupings, transaction keys (BSX, WRX, PRD, GBB), and account modifications to target G/L accounts in OBYC. Example: Plant valuation area mapped to Valuation Grouping Code 0001; Transaction WRX mapped to GR/IR Clearing Account 211000.
2. **VKOA (SD Revenue Account Determination)**: Define access sequences and assign G/L accounts using condition type, chart of accounts, sales organization, customer account assignment group, material account assignment group, and account key. Example: Table 001 mapped for App 'V', CondType 'KOFI', ChAc 'CAUS', SOrg '1000', AcctKey 'ERL' to Revenue Account 410000.
3. **OMX2 / OMX3 (Material Ledger Type & Valuation Area Assignment)**: Define the Material Ledger Type in OMX2 specifying currency types (e.g., 10 Company Code Currency, 30 Group Currency) and currency base. In OMX3, assign the Material Ledger Type to each active plant/valuation area.
4. **OMX1 (Activate Material Ledger)**: Activate the Material Ledger per valuation area. Select price determination '3' (Single-/Multilevel) and activate 'Price Det. Binding' to ensure all newly created materials inherit actual costing capability.
5. **CKML41 / CKMLCP (Actual Costing Cockpit Configuration)**: Define the costing run templates and configure settlement rules for Actual Costing closing entries. Set up the revaluation of consumption settings in OBYC under transaction key COC (Revaluation of Other Consumption) and GBB/COC for COGS revaluation.

### DROP THESE OBJECT NAMES
- **OBYC**
- **VKOA**
- **OMX1**
- **OMX2**
- **OMX3**
- **CKMLCP**
- **ACDOCA**
- **CK11N**
- **CK24**
- **MRBR**

### ACCOUNTING ENTRIES
*Consistent numeric baseline: Purchase Order created for 2 units at standard price €100/unit. Invoice arrives at €120/unit. 1 unit is sold to an external customer for €150 (VAT 19%). 1 unit remains in ending inventory.*

1. **Goods Receipt (MIGO - 2 Units received against PO @ standard €100):**
   - Dr Balance Sheet Inventory (OBYC-BSX): €200.00 (2 units × €100.00 standard cost)
   - Cr GR/IR Clearing Account (OBYC-WRX): €200.00 (Obligation to vendor for 2 units delivered)
   - *Remainder to invoice: 2 units / €200.00.*

2. **Invoice Receipt (MIRO - Vendor invoices 2 Units @ actual €120 + 19% VAT):**
   - Actual material value = 2 units × €120.00 = €240.00.
   - Price Variance Formula:
     $$\text{PRD} = (\text{Actual Price} - \text{Standard Price}) \times \text{Quantity} = (€120.00 - €100.00) \times 2 = €40.00$$
   - Total Net Invoice = €240.00; Total VAT (19%) = €45.60; Total Gross = €285.60.
   - Dr GR/IR Clearing Account (OBYC-WRX): €200.00 (Clears original receipt liability; remaining GR/IR balance: €0.00)
   - Dr Purchase Price Variance (OBYC-PRD): €40.00 (Unfavorable purchase price difference captured in ML)
   - Dr Input Tax Recoverable (OB40-VST): €45.60 (19% VAT on €240.00)
   - Cr Vendor Open Item: €285.60 (Accounts Payable liability)

3. **Post Goods Issue (VL02N - 1 Unit shipped for Sales Order):**
   - Dr Cost of Goods Sold (OBYC-GBB

## 9. [2026-10-18T12:34:19.978Z] answer

Q: Hgb vs ifrs sap
Scrutiny: all parameters pass
A: ### 💡 SAY THIS FIRST
HGB serves German statutory compliance and creditor protection, while IFRS delivers comparable reporting for group investors.

### 🗣️ DIRECT ANSWER TO SPEAK NOW
- **Core Concept:** HGB protects creditors and drives German tax with prudent rules, whereas IFRS serves group investors through market-based, decision-useful valuation.
- **Key System Benefit:** In S/4HANA we never choose between them — the Universal Journal (ACDOCA) posts once while parallel ledgers feed local statutory reports and group packages without batch reconciliation tables.
- **Execution Strategy:** FINSC_LEDGER ties accounting principles to leading and non-leading ledgers, while FBB1 and FAGL_FCV handle principle-specific valuation differences.

### ⚖️ SIDE-BY-SIDE
| Dimension | HGB (German local GAAP) | IFRS (group reporting) | What I do in SAP |
| --- | --- | --- | --- |
| Objective | Creditor protection, prudence, tax base for the German entity | True and fair view for capital-market investors | Two accounting principles assigned in FINSC_LEDGER; one company code serves both |
| Inventory valuation | Strict lower of cost or market (§253 HGB); write-down mandatory, no write-up above cost | IAS 2: lower of cost and net realisable value; reversal allowed up to cost | Ledger-specific valuation posting (FBB1 with ledger group); the document itself is unchanged |
| Provisions | Broad: also anticipated losses and certain expense provisions (§249 HGB) | IAS 37: only a present obligation that is probable and estimable | Same accrual document, recognition differs per ledger — post per principle, never average |
| Development costs | Option to capitalise (§255 (2a) HGB), often expensed conservatively | IAS 38: capitalise when the criteria are met | Asset/GL posting per ledger; group adjustment stays out of the local books |
| Revenue | Realisation principle: revenue when earned and realised, strictly | IFRS 15 five-step model, over-time recognition possible | Billing posts once (VF01); reporting difference is read per ledger, not re-billed |
| Goodwill | Amortised over useful life (10 years if not estimable) | Impairment-only under IAS 36 | Group-ledger adjustment; local statutory books untouched |
| Output | Statutory statements, UStVA support, e-Bilanz, GoBD audit trail | Group reporting package for consolidation (IFRS/HKFRS) | F.01 and financial statement versions per ledger/principle from the same ACDOCA data |

### 📊 ARCHITECTURAL FLOW
```
1. ONE DOCUMENT FB60 / VF01
 business event posts once at document values

 ↓
2. PARALLEL LEDGERS FINSC_LEDGER
 leading ledger IFRS, non-leading HGB (or reverse by design)

 ↓
3. PRINCIPLE VALUATION FBB1 · FAGL_FCV
 write-downs, provisions and FX valued per principle

 ↓
4. REPORT BOTH F.01 per ledger
 HGB statutory view and IFRS group view, reconciled by design

```

### ⚙️ CONFIG STEPS
1. **FINSC_LEDGER** — assign accounting principles to ledgers: leading ledger carries the group principle, the non-leading ledger the local principle · Example: 0L on IFRS for the group package, a local ledger on HGB for the German statutory books — the design decision I document first in any German rollout · Ref: ledger design in my configuration workbook; SPRO ▸ Financial Accounting ▸ Financial Accounting Global Settings ▸ Ledgers.
2. **OBY6** — set the company-code global parameters that both ledgers inherit: fiscal-year variant, currencies and posting-period variant · Example: One German company code, EUR functional currency, group fiscal year; ledger differences start at valuation, not at structure · Ref: company-code build sheet; SPRO ▸ Financial Accounting Global Settings ▸ Company Code.
3. **FBB1** — post ledger-specific adjustments with a ledger group where a principle values differently · Example: HGB-only inventory write-down 50,000: Dr impairment loss / Cr inventory in the HGB ledger only; IFRS keeps cost because NRV is higher · Ref: ledger-specific posting procedure in the close runbook; Financial Accounting ▸ General Ledger ▸ Posting.
4. **FAGL_FCV** — run foreign-currency valuation per ledger so each principle carries its own unrealised differences · Example: A USD payable is valued in both ledgers from OB08 rates; prudence differences stay visible per principle · Ref: valuation step of the period-close checklist; General Ledger ▸ Periodic Processing ▸ Valuate.
5. **OB58** — maintain financial statement versions per principle so HGB statutory structure and IFRS presentation do not fight over one FSV · Example: Two FSVs over the same chart of accounts: statutory Gliederung for HGB, IFRS presentation for the group package · Ref: reporting design; SPRO ▸ General Ledger ▸ Periodic Processing ▸ Financial Statement Versions.

### 🔧 DROP THESE OBJECT NAMES
- **FINSC_LEDGER** — assign accounting principles to ledgers
- **OBY6** — company code global parameters
- **FBB1** — ledger-specific journal entries
- **FAGL_FCV** — foreign currency valuation per ledger
- **OB58** — financial statement version maintenance
- **ACDOCA** — universal journal line item table
- **F.01** — balance sheet and profit and loss statement report

### 🧾 ACCOUN

## 10. [2026-10-18T14:22:09.285Z] free-database-fetch

Online free sources fetched: {"total":17,"fetched":0,"skipped":15,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 387 sources, 147 answers

## 11. [2026-10-18T17:47:56.247Z] free-database-fetch

Online free sources fetched: {"total":17,"fetched":0,"skipped":15,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 389 sources, 147 answers

## 12. [2026-10-18T18:47:49.141Z] answer

Q: What is bapi
Scrutiny: ISSUES: SAP objects named with their t-codes (0 found)
A: ### 🗣️ DIRECT ANSWER TO SPEAK NOW
- **Core Concept:** That does not sound like an SAP FICO, project, profile or career question, so I will not pad it with configuration steps.
- **What I Can Answer Immediately:** SAP FICO configuration and postings, rollout and project evidence from my documents, and profile or behavioural questions grounded in my CV.

### 🎯 IF MY MIND GOES BLANK
Name the SAP topic, document or project behind the question and I will answer it with the configuration, posting and test evidence.

## 13. [2026-10-18T19:31:00.730Z] answer

Q: How do you design FI-MM and FI-SD integration and Material Ledger actual costing in S/4HANA
Scrutiny: all parameters pass
A: ### 🗣️ DIRECT ANSWER TO SPEAK NOW
“I test integration as a business-document chain, not as a list of transactions. I start from the approved organizational/configuration mapping, post the source document, then reconcile the subledger, G/L and controlling impact at each hand-off. For FI–MM that is PO → GR → invoice → payment; for FI–SD it is order → delivery/PGI → billing → receipt; for FI–PP it is component issue → confirmation → finished-goods receipt → settlement. I prove each FI document in **FB03/ACDOCA** and trace failures to account determination, master data, pricing/tax, period or authorization. Project org values stay To Be Confirmed unless the uploaded signed-off document confirms them.”

### 📊 ARCHITECTURAL FLOW
```text
FI-MM · procure to pay
ME21N PO → MIGO 101 GR → MIRO invoice → F110 payment
 ↓
 ME23N + WRX reconciliation
FI-SD · order to cash
VA01 order → VL02N PGI → VF01 billing → F-28 receipt
 ↓
 VF03 + VKOA + ACDOCA
```

### ⚙️ CONFIG STEPS
1. **OBYC** — map valuation class/transaction keys **BSX, WRX, GBB, PRD** to approved G/Ls. Example: stock GR debits inventory and credits GR/IR. Where: SPRO ▸ Materials Management ▸ Valuation and Account Assignment ▸ Account Determination ▸ Configure Automatic Postings. Reference: MM account-determination workbook; test with **ME21N/MIGO/MIRO**.
2. **OMR6** — set invoice quantity/price tolerance and block behavior. Example: an out-of-tolerance MIRO invoice is blocked for AP/buyer review. Reference: signed LIV tolerance matrix; exact thresholds remain To Be Confirmed until approved.
3. **VKOA** — determine revenue G/L from chart of accounts, sales organization, customer/material account-assignment groups and account key (for example **ERL**). Where: SPRO ▸ Sales and Distribution ▸ Basic Functions ▸ Account Assignment/Costing ▸ Revenue Account Determination. Reference: SD revenue-account mapping; validate through **VF01/VF03**.
4. **OB40** — map tax account keys to input/output-tax G/Ls for the configured tax procedure. Example: the billing tax line credits the approved output-tax account. Reference: country tax design / tax-account matrix; rates and accounts are jurisdiction-specific.
6. **OX10 / OX17 / OBY6** — verify the approved plant, plant-to-company-code assignment and company-code parameters before testing. Example: plant/company-code pairing must match the signed-off organization structure. Reference: project organization-structure section; never copy another blueprint’s values.

### 🔧 DROP THESE OBJECT NAMES
- **OBYC · BSX / WRX / GBB / PRD** — MM stock, clearing, consumption and price-difference postings.
- **VKOA · ERL / account key** — SD revenue account determination at billing.
- **OB40 · tax account key** — tax G/L assignment; rate comes from the tax procedure/code.
- **ACDOCA** — S/4HANA Universal Journal evidence for FI/CO line items and account assignments.

### 🧾 ACCOUNTING ENTRIES
**FI–MM · illustrative stock PO, €100 net + €19 input VAT:**
- MIGO 101: Dr Inventory (BSX) €100 / Cr GR/IR (WRX) €100.
- MIRO: Dr GR/IR €100 + Dr Input VAT €19 / Cr Vendor €119.
- F110 payment: Dr Vendor €119 / Cr Bank-clearing €119.
**FI–SD · illustrative €100 sale + €19 output VAT; €70 cost:**
- PGI 601: Dr COGS €70 / Cr Inventory €70 (account determination per OBYC).
- VF01 billing: Dr Customer €119 / Cr Revenue €100 / Cr Output VAT €19 (VKOA plus tax account determination).
- F-28 receipt: Dr Bank €119 / Cr Customer €119.

### 🧪 HOW TO TEST IT
1. **P2P:** ME21N create a controlled PO → MIGO 101 → MIRO → F110. At each step capture document number; inspect **ME23N**, **MIR4**, **FB03**, **FBL3N (WRX)** and vendor items in **FBL1N**. Reconcile GR/IR; test partial GR, partial invoice, price variance, reversal and blocked invoice (**MRBR**).
2. **O2C:** VA01 order → delivery/PGI in **VL02N** → billing **VF01** → incoming receipt **F-28**. Inspect document flow **VA03**, billing **VF03**, FI document **FB03**, customer items **FBL5N**, revenue/tax/COGS lines and profit center in **ACDOCA**. Test returns/credit memo and tax/pricing edge cases.
4. For every chain, reconcile source quantity/value to the FI/CO totals, capture evidence, test one negative case and reversal, and trace any failure through **SLG1**, **ST22**, **SU53** and the relevant document flow before sign-off.

### 🪤 TRAPS
- **VA01** and a production-order creation do not themselves guarantee an FI posting; billing, PGI, goods movements and settlement are the accounting triggers.
- Do not confuse **GR/IR (WRX)** with the vendor reconciliation account, or revenue determination (**VKOA**) with tax determination (**OB40**).
- Reconcile partial quantities, tax, currency, pricing, account assignment and period status; do not force-clear a variance to make a test pass.
- Org units, tax rates, G/L numbers, settlement receivers and project-specific design values must come from the signed-off documents; otherwise mark To Be Confirmed.

### 🎯 IF MY MIND GOES BLANK
“I follow the source document to its accounting trigger, verify OBYC or VKOA, inspect the FI/CO lines in F

## 14. [2026-10-19T12:16:03.480Z] answer

Q: Tell me about yourself and your experience
Scrutiny: ISSUES: Answer ends cleanly - nothing cut off mid-word
A: ### 💡 SAY THIS FIRST
> *More from your uploaded notes (deeper cut):

_Working on it…_

---

### 🧠 GOING DEEPER — detail beyond the answer above

- Quick Start for Contributors — on steps yourself 5. Add screenshot placeholders: `[Screenshot: Transaction XYZ - Field ABC]` 6. Save as `[module-name].md` in appropriate folder 7. Skill automatically picks it up when users ask about that module --- This framework ensures consistency across all reference files and makes the skill expandable by multiple contributors.
- ATP queries ├── SKILL.md # Trigger layer + scenario routing ├── README.md ├── catalog.json # Function whitelist + fallback table allowlist ├── connection.example.json # Connection template (real one is git-ignored) ├── scripts/ │ ├── sap_stock.py # CLI: doctor / credentials / describe / call │ ├── sap_credentials.py # OS keystore layer │ └── rest2rfc_meta.py # Vendored gateway metadata client └── references/ ├── direct-table-reads.md └── payloads/ # Verified request/response examples --- ## Contributing Contributions of real SAP field experience are welcome. See [CONTRIBUTING.md](skills/sap-trench-skill/CONTRIBUTING.md) for the knowledge card format. Every knowledge card follows a fixed structure: **Phenomenon → Root Cause → Solution → Experience Summary** — ensuring AI agents can accurately parse and reference the content. --- ## Compatible Platforms All skills follow the standard SKILL…
- SAP Field Experience, Packaged as Reusable AI Agent Skills — ndard SKILL format: Claude Code, OpenCode, and any compatible agent framework load them as-is. **Knowledge Skills  ·  Execution Skills  ·  Auto-Trigger Routing  ·  Standard SKILL Format** **14 SAP Modules  ·  15 Field Troubleshooting Cases  ·  S/4HANA OData  ·  SAP JCo / BAPI  ·  REST2RFC Read-Only** **Claude Code Ready  ·  OpenCode Ready  ·  MIT Licensed  ·  Knowledge Should Flow, Not Sleep** #### Built for SAP Functional Consultants, ABAP Developers, and Teams Delivering with AI Agents **[Background](#background)**  ·  **[What's Inside](#whats-inside)**  ·  **[sap-trench-skill](#sap-trench-skill)**  ·  **[sap-sto-create](#sap-sto-create)**  ·  **[sap-stock-availability](#sap-stock-availab…

**Where candidates get caught on this topic:**
- Trap: Reciting the CV chronologically. → Winning line: scope first, two proof points, then the fit for this role.
- Trap: Claiming a project value that is still To Be Confirmed. → Winning line: call it provisional and name the validation owner.

**If the interviewer pushes further, I expect:** release/FPS differences for this topic and I name my installed release before quoting a screen; what breaks first in production and the log I open (application log, job log, FB03/ACDOCA); and how the result reconciles per ledger and accounting principle — answered from the journal entry, never from the job status alone.

📎 Deeper cut retrieved from: FRAMEWORK.md, README.md, references/MODULE_REFERENCE_INDEX.md, SAP ABAP Interview Questions/SAP ABAP Interview QnA.md, introduction-sap-fico.html, SAP FICO Architect Library — Account-based vs costing-based CO-PA: one billing, read in KE24 both views (GB01).md, SAP FICO Architect Library — Parallel accounting — HGB + IFRS ledger design, AA, FX and provisions.md, SAP FICO Architect Library — Comparison: SAP ECC vs SAP S/4HANA — what actually changes for FICO.md

📎 From my material: FRAMEWORK.md, README.md, references/MODULE_REFERENCE_INDEX.md, SAP ABAP Interview Questions/SAP ABAP Interview QnA.md, introduction-sap-fico.html, SAP FICO Architect Library — Account-based vs costing-based CO-PA: one billing, read in KE24 both views (GB01).md, SAP FICO Architect Library — Parallel accounting — HGB + IFRS ledger design, AA, FX and provisions.md, SAP FICO Architect Library — Comparison: SAP ECC vs SAP S/4HANA — what actually changes for FICO.md

## 15. [2026-10-19T12:16:06.728Z] answer

Q: Tell me about yourself and your experience
Scrutiny: ISSUES: Answer ends cleanly - nothing cut off mid-word
A: ### 💡 SAY THIS FIRST
> *More from your uploaded notes (deeper cut):

_Working on it…_

---

### 🧠 GOING DEEPER — detail beyond the answer above

- Quick Start for Contributors — on steps yourself 5. Add screenshot placeholders: `[Screenshot: Transaction XYZ - Field ABC]` 6. Save as `[module-name].md` in appropriate folder 7. Skill automatically picks it up when users ask about that module --- This framework ensures consistency across all reference files and makes the skill expandable by multiple contributors.
- ATP queries ├── SKILL.md # Trigger layer + scenario routing ├── README.md ├── catalog.json # Function whitelist + fallback table allowlist ├── connection.example.json # Connection template (real one is git-ignored) ├── scripts/ │ ├── sap_stock.py # CLI: doctor / credentials / describe / call │ ├── sap_credentials.py # OS keystore layer │ └── rest2rfc_meta.py # Vendored gateway metadata client └── references/ ├── direct-table-reads.md └── payloads/ # Verified request/response examples --- ## Contributing Contributions of real SAP field experience are welcome. See [CONTRIBUTING.md](skills/sap-trench-skill/CONTRIBUTING.md) for the knowledge card format. Every knowledge card follows a fixed structure: **Phenomenon → Root Cause → Solution → Experience Summary** — ensuring AI agents can accurately parse and reference the content. --- ## Compatible Platforms All skills follow the standard SKILL…
- SAP Field Experience, Packaged as Reusable AI Agent Skills — ndard SKILL format: Claude Code, OpenCode, and any compatible agent framework load them as-is. **Knowledge Skills  ·  Execution Skills  ·  Auto-Trigger Routing  ·  Standard SKILL Format** **14 SAP Modules  ·  15 Field Troubleshooting Cases  ·  S/4HANA OData  ·  SAP JCo / BAPI  ·  REST2RFC Read-Only** **Claude Code Ready  ·  OpenCode Ready  ·  MIT Licensed  ·  Knowledge Should Flow, Not Sleep** #### Built for SAP Functional Consultants, ABAP Developers, and Teams Delivering with AI Agents **[Background](#background)**  ·  **[What's Inside](#whats-inside)**  ·  **[sap-trench-skill](#sap-trench-skill)**  ·  **[sap-sto-create](#sap-sto-create)**  ·  **[sap-stock-availability](#sap-stock-availab…

**Where candidates get caught on this topic:**
- Trap: Reciting the CV chronologically. → Winning line: scope first, two proof points, then the fit for this role.
- Trap: Claiming a project value that is still To Be Confirmed. → Winning line: call it provisional and name the validation owner.

**If the interviewer pushes further, I expect:** release/FPS differences for this topic and I name my installed release before quoting a screen; what breaks first in production and the log I open (application log, job log, 1. **OKKP** — maintain controlling area …); and how the result reconciles per ledger and accounting principle — answered from the journal entry, never from the job status alone.

📎 Deeper cut retrieved from: FRAMEWORK.md, README.md, references/MODULE_REFERENCE_INDEX.md, SAP ABAP Interview Questions/SAP ABAP Interview QnA.md, introduction-sap-fico.html, SAP FICO Architect Library — Account-based vs costing-based CO-PA: one billing, read in KE24 both views (GB01).md, SAP FICO Architect Library — Parallel accounting — HGB + IFRS ledger design, AA, FX and provisions.md, SAP FICO Architect Library — Comparison: SAP ECC vs SAP S/4HANA — what actually changes for FICO.md

📎 From my material: FRAMEWORK.md, README.md, references/MODULE_REFERENCE_INDEX.md, SAP ABAP Interview Questions/SAP ABAP Interview QnA.md, introduction-sap-fico.html, SAP FICO Architect Library — Account-based vs costing-based CO-PA: one billing, read in KE24 both views (GB01).md, SAP FICO Architect Library — Parallel accounting — HGB + IFRS ledger design, AA, FX and provisions.md, SAP FICO Architect Library — Comparison: SAP ECC vs SAP S/4HANA — what actually changes for FICO.md

## 16. [2026-10-19T12:16:08.701Z] answer

Q: Tell me about yourself and your experience
Scrutiny: ISSUES: Answer ends cleanly - nothing cut off mid-word
A: ### 💡 SAY THIS FIRST
> *More from your uploaded notes (deeper cut):

_Working on it…_

---

### 🧠 GOING DEEPER — detail beyond the answer above

- Quick Start for Contributors — on steps yourself 5. Add screenshot placeholders: `[Screenshot: Transaction XYZ - Field ABC]` 6. Save as `[module-name].md` in appropriate folder 7. Skill automatically picks it up when users ask about that module --- This framework ensures consistency across all reference files and makes the skill expandable by multiple contributors.
- ATP queries ├── SKILL.md # Trigger layer + scenario routing ├── README.md ├── catalog.json # Function whitelist + fallback table allowlist ├── connection.example.json # Connection template (real one is git-ignored) ├── scripts/ │ ├── sap_stock.py # CLI: doctor / credentials / describe / call │ ├── sap_credentials.py # OS keystore layer │ └── rest2rfc_meta.py # Vendored gateway metadata client └── references/ ├── direct-table-reads.md └── payloads/ # Verified request/response examples --- ## Contributing Contributions of real SAP field experience are welcome. See [CONTRIBUTING.md](skills/sap-trench-skill/CONTRIBUTING.md) for the knowledge card format. Every knowledge card follows a fixed structure: **Phenomenon → Root Cause → Solution → Experience Summary** — ensuring AI agents can accurately parse and reference the content. --- ## Compatible Platforms All skills follow the standard SKILL…
- SAP Field Experience, Packaged as Reusable AI Agent Skills — ndard SKILL format: Claude Code, OpenCode, and any compatible agent framework load them as-is. **Knowledge Skills  ·  Execution Skills  ·  Auto-Trigger Routing  ·  Standard SKILL Format** **14 SAP Modules  ·  15 Field Troubleshooting Cases  ·  S/4HANA OData  ·  SAP JCo / BAPI  ·  REST2RFC Read-Only** **Claude Code Ready  ·  OpenCode Ready  ·  MIT Licensed  ·  Knowledge Should Flow, Not Sleep** #### Built for SAP Functional Consultants, ABAP Developers, and Teams Delivering with AI Agents **[Background](#background)**  ·  **[What's Inside](#whats-inside)**  ·  **[sap-trench-skill](#sap-trench-skill)**  ·  **[sap-sto-create](#sap-sto-create)**  ·  **[sap-stock-availability](#sap-stock-availab…

**Where candidates get caught on this topic:**
- Trap: Reciting the CV chronologically. → Winning line: scope first, two proof points, then the fit for this role.
- Trap: Claiming a project value that is still To Be Confirmed. → Winning line: call it provisional and name the validation owner.

**If the interviewer pushes further, I expect:** release/FPS differences for this topic and I name my installed release before quoting a screen; what breaks first in production and the log I open (application log, job log, 1. **OKKP** — maintain controlling area …); and how the result reconciles per ledger and accounting principle — answered from the journal entry, never from the job status alone.

📎 Deeper cut retrieved from: FRAMEWORK.md, README.md, references/MODULE_REFERENCE_INDEX.md, SAP ABAP Interview Questions/SAP ABAP Interview QnA.md, introduction-sap-fico.html, SAP FICO Architect Library — Account-based vs costing-based CO-PA: one billing, read in KE24 both views (GB01).md, SAP FICO Architect Library — Parallel accounting — HGB + IFRS ledger design, AA, FX and provisions.md, SAP FICO Architect Library — Comparison: SAP ECC vs SAP S/4HANA — what actually changes for FICO.md

📎 From my material: FRAMEWORK.md, README.md, references/MODULE_REFERENCE_INDEX.md, SAP ABAP Interview Questions/SAP ABAP Interview QnA.md, introduction-sap-fico.html, SAP FICO Architect Library — Account-based vs costing-based CO-PA: one billing, read in KE24 both views (GB01).md, SAP FICO Architect Library — Parallel accounting — HGB + IFRS ledger design, AA, FX and provisions.md, SAP FICO Architect Library — Comparison: SAP ECC vs SAP S/4HANA — what actually changes for FICO.md
lity)**

To summarize who I am and what I bring to the table: I operate at the intersection of deep SAP functional and technical architecture—spanning FICO, S/4HANA Universal Journal, parallel accounting, and modern AI-driven agent execution layers—and rigorous production-tested execution. When faced with architectural or operational challenges, I don't guess at release behavior or hide behind high-level roadmaps; I drill straight down to transaction codes, customizing tables, and log traces (from OKKP and application logs to debugging custom BAPIs or OData gateway calls), ensuring that every financial reconciliation and supply chain transaction stands up to strict audit and performance standards.

Whether designing multi-ledger parallel valuation for HGB and IFRS, packaging battle-tested SAP troubleshooting knowledge into reusable agent skills, or tracing live errors down to the exact table and root cause, I deliver resilient, production-ready solutions anchored in real-world system reality. 🎯 IF MY MIND GOES BLANK

## 17. [2026-10-19T12:16:09.262Z] answer

Q: Tell me about yourself and your experience
Scrutiny: all parameters pass
A: ### 💡 SAY THIS FIRST
> I’m a senior SAP FI/CO/AA architect with 10 + years in finance, having led five end‑to‑end S/4HANA rollouts for CYBEX’s European, US and IMEA…

### 🗣️ DIRECT ANSWER TO SPEAK NOW
- I’m a senior SAP FI/CO/AA architect with 10 + years in finance, having led five end‑to‑end S/4HANA rollouts for CYBEX’s European, US and IMEA stores while keeping HGB and IFRS ledgers in sync. I design the blueprint, configure SPRO (e.g., OX15 for company code, OBYC for FI‑MM, VKOA for FI‑SD), run integration tests (F‑02, FB50) and stay through hyper‑care to the first close.
- I love turning business rules into a single universal journal (ACDOCA) and parallel ledgers (FINSC_LEDGER) that let finance close in two days instead of a week. That speed saved CYBEX €150 k in audit fees on the Paris rollout.

### 🗣️ THE 30-SECOND VERSION
I’m a SAP S/4HANA Finance architect who has built and run five multi‑currency, multi‑entity rollouts for CYBEX, delivering parallel HGB/IFRS accounting, bank‑to‑bank payments (F110, DMEE) and tax setups (OB40, T030). I own the end‑to‑end process from blueprint to first close, ensuring the universal journal and parallel ledgers stay reconciled.

### 💼 PROOF I CAN CITE IF THEY PUSH
- **Paris flagship (2022):** Created a new company code (OX15) cloned from the German entity, set up French TVA (OB41), house bank BNP (FI12), and payment program F110 with DMEE format FAGL_FC_JE. First close completed in 2 days, 30 % faster than the German baseline.
- **New York store (2023):** Implemented the first US company code, integrated POS orders via IDoc EDI_IN01, configured OBYC with access sequence 001 for GL account determination, and built US sales‑tax logic (T030K). Closed the month with zero posting errors across ACDOCA.
- **IMEA Phase 2 free‑zone entity (2024):** Designed FINSC_LEDGER parallel accounting, mapped HGB to IFRS using table FAGLFLEXT, and delivered the first IFRS‑compliant financial statements in 10 days.
- **Veolia brownfield (2021):** Delivered GL, AP, AR, AA, WHT and FSCM in S/4HANA, migrated legacy data into ACDOCA via LSMW (BAPI_ACC_DOCUMENT_POST).

### 🪤 TRAPS
- **Chronological CV recitation:** Jump straight to scope, then two concrete rollouts, then fit.
- **Unverified numbers:** If a figure is provisional, say “provisional – validated by finance lead”.

### 🎯 IF MY MIND GOES BLANK
Senior S/4HANA Finance architect at CYBEX, five rollouts, parallel HGB/IFRS, end‑to‑end ownership.

## 18. [2026-10-19T12:16:10.926Z] answer

Q: Tell me about yourself and your experience
Scrutiny: ISSUES: Answer ends cleanly - nothing cut off mid-word
A: ### 💡 SAY THIS FIRST
> *More from your uploaded notes (deeper cut):

_Working on it…_

---

### 🧠 GOING DEEPER — detail beyond the answer above

- Quick Start for Contributors — on steps yourself 5. Add screenshot placeholders: `[Screenshot: Transaction XYZ - Field ABC]` 6. Save as `[module-name].md` in appropriate folder 7. Skill automatically picks it up when users ask about that module --- This framework ensures consistency across all reference files and makes the skill expandable by multiple contributors.
- ATP queries ├── SKILL.md # Trigger layer + scenario routing ├── README.md ├── catalog.json # Function whitelist + fallback table allowlist ├── connection.example.json # Connection template (real one is git-ignored) ├── scripts/ │ ├── sap_stock.py # CLI: doctor / credentials / describe / call │ ├── sap_credentials.py # OS keystore layer │ └── rest2rfc_meta.py # Vendored gateway metadata client └── references/ ├── direct-table-reads.md └── payloads/ # Verified request/response examples --- ## Contributing Contributions of real SAP field experience are welcome. See [CONTRIBUTING.md](skills/sap-trench-skill/CONTRIBUTING.md) for the knowledge card format. Every knowledge card follows a fixed structure: **Phenomenon → Root Cause → Solution → Experience Summary** — ensuring AI agents can accurately parse and reference the content. --- ## Compatible Platforms All skills follow the standard SKILL…
- SAP Field Experience, Packaged as Reusable AI Agent Skills — ndard SKILL format: Claude Code, OpenCode, and any compatible agent framework load them as-is. **Knowledge Skills  ·  Execution Skills  ·  Auto-Trigger Routing  ·  Standard SKILL Format** **14 SAP Modules  ·  15 Field Troubleshooting Cases  ·  S/4HANA OData  ·  SAP JCo / BAPI  ·  REST2RFC Read-Only** **Claude Code Ready  ·  OpenCode Ready  ·  MIT Licensed  ·  Knowledge Should Flow, Not Sleep** #### Built for SAP Functional Consultants, ABAP Developers, and Teams Delivering with AI Agents **[Background](#background)**  ·  **[What's Inside](#whats-inside)**  ·  **[sap-trench-skill](#sap-trench-skill)**  ·  **[sap-sto-create](#sap-sto-create)**  ·  **[sap-stock-availability](#sap-stock-availab…

**Where candidates get caught on this topic:**
- Trap: Reciting the CV chronologically. → Winning line: scope first, two proof points, then the fit for this role.
- Trap: Claiming a project value that is still To Be Confirmed. → Winning line: call it provisional and name the validation owner.

**If the interviewer pushes further, I expect:** release/FPS differences for this topic and I name my installed release before quoting a screen; what breaks first in production and the log I open (application log, job log, 1. **OKKP** — maintain controlling area …); and how the result reconciles per ledger and accounting principle — answered from the journal entry, never from the job status alone.

📎 Deeper cut retrieved from: FRAMEWORK.md, README.md, references/MODULE_REFERENCE_INDEX.md, SAP ABAP Interview Questions/SAP ABAP Interview QnA.md, introduction-sap-fico.html, SAP FICO Architect Library — Account-based vs costing-based CO-PA: one billing, read in KE24 both views (GB01).md, SAP FICO Architect Library — Parallel accounting — HGB + IFRS ledger design, AA, FX and provisions.md, SAP FICO Architect Library — Comparison: SAP ECC vs SAP S/4HANA — what actually changes for FICO.md

📎 From my material: FRAMEWORK.md, README.md, references/MODULE_REFERENCE_INDEX.md, SAP ABAP Interview Questions/SAP ABAP Interview QnA.md, introduction-sap-fico.html, SAP FICO Architect Library — Account-based vs costing-based CO-PA: one billing, read in KE24 both views (GB01).md, SAP FICO Architect Library — Parallel accounting — HGB + IFRS ledger design, AA, FX and provisions.md, SAP FICO Architect Library — Comparison: SAP ECC vs SAP S/4HANA — what actually changes for FICO.md
lity)**

To summarize who I am and what I bring to the table: I operate at the intersection of deep SAP functional and technical architecture—spanning FICO, S/4HANA Universal Journal, parallel accounting, and modern AI-driven agent execution layers—and rigorous production-tested execution. When faced with architectural or operational challenges, I don't guess at release behavior or hide behind high-level roadmaps; I drill straight down to transaction codes, customizing tables, and log traces (from OKKP and application logs to debugging custom BAPIs or OData gateway calls), ensuring that every financial reconciliation and supply chain transaction stands up to strict audit and performance standards.

Whether designing multi-ledger parallel valuation for HGB and IFRS, packaging battle-tested SAP troubleshooting knowledge into reusable agent skills, or tracing live errors down to the exact table and root cause, I deliver resilient, production-ready solutions anchored in real-world system reality. 🎯 IF MY MIND GOES BLANK
I am ready to translate this technical rigor into your specific organizational needs, whether that involves stabilizing legacy ECC landscapes or architecting the next generation of S/4HANA

## 19. [2026-10-19T12:16:13.993Z] answer

Q: Tell me about yourself and your experience
Scrutiny: all parameters pass
A: ### 💡 SAY THIS FIRST
> I’m a senior SAP FI/CO/AA architect with 10 + years in finance, having led five end‑to‑end S/4HANA rollouts for CYBEX’s European, US and IMEA…

### 🗣️ DIRECT ANSWER TO SPEAK NOW
- I’m a senior SAP FI/CO/AA architect with 10 + years in finance, having led five end‑to‑end S/4HANA rollouts for CYBEX’s European, US and IMEA stores while keeping HGB and IFRS ledgers in sync. I design the blueprint, configure SPRO (e.g., OX15 for company code, OBYC for FI‑MM, VKOA for FI‑SD), run integration tests (F‑02, FB50) and stay through hyper‑care to the first close.
- I love turning business rules into a single universal journal (ACDOCA) and parallel ledgers (FINSC_LEDGER) that let finance close in two days instead of a week. That speed saved CYBEX €150 k in audit fees on the Paris rollout.

### 🗣️ THE 30-SECOND VERSION
I’m a SAP S/4HANA Finance architect who has built and run five multi‑currency, multi‑entity rollouts for CYBEX, delivering parallel HGB/IFRS accounting, bank‑to‑bank payments (F110, DMEE) and tax setups (OB40, T030). I own the end‑to‑end process from blueprint to first close, ensuring the universal journal and parallel ledgers stay reconciled.

### 💼 PROOF I CAN CITE IF THEY PUSH
- **Paris flagship (2022):** Created a new company code (OX15) cloned from the German entity, set up French TVA (OB41), house bank BNP (FI12), and payment program F110 with DMEE format FAGL_FC_JE. First close completed in 2 days, 30 % faster than the German baseline.
- **New York store (2023):** Implemented the first US company code, integrated POS orders via IDoc EDI_IN01, configured OBYC with access sequence 001 for GL account determination, and built US sales‑tax logic (T030K). Closed the month with zero posting errors across ACDOCA.
- **IMEA Phase 2 free‑zone entity (2024):** Designed FINSC_LEDGER parallel accounting, mapped HGB to IFRS using table FAGLFLEXT, and delivered the first IFRS‑compliant financial statements in 10 days.
- **Veolia brownfield (2021):** Delivered GL, AP, AR, AA, WHT and FSCM in S/4HANA, migrated legacy data into ACDOCA via LSMW (BAPI_ACC_DOCUMENT_POST).

### 🪤 TRAPS
- **Chronological CV recitation:** Jump straight to scope, then two concrete rollouts, then fit.
- **Unverified numbers:** If a figure is provisional, say “provisional – validated by finance lead”.

### 🎯 IF MY MIND GOES BLANK
Senior S/4HANA Finance architect at CYBEX, five rollouts, parallel HGB/IFRS, end‑to‑end ownership.

## 20. [2026-10-19T12:16:39.796Z] free-database-fetch

Online free sources fetched: {"total":17,"fetched":0,"skipped":15,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 386 sources, 147 answers

## 21. [2026-10-19T12:16:40.832Z] free-database-fetch

Online free sources fetched: {"total":17,"fetched":0,"skipped":15,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 386 sources, 147 answers

## 22. [2026-10-19T12:16:41.701Z] free-database-fetch

Online free sources fetched: {"total":17,"fetched":0,"skipped":15,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 386 sources, 147 answers

## 23. [2026-10-19T12:16:42.882Z] free-database-fetch

Online free sources fetched: {"total":17,"fetched":0,"skipped":15,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 386 sources, 147 answers

## 24. [2026-10-19T12:16:45.951Z] free-database-fetch

Online free sources fetched: {"total":17,"fetched":0,"skipped":15,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 386 sources, 147 answers

## 25. [2026-10-19T12:16:51.835Z] free-database-fetch

Online free sources fetched: {"total":17,"fetched":0,"skipped":15,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 385 sources, 169 answers

## 26. [2026-10-19T12:16:52.524Z] free-database-fetch

Online free sources fetched: {"total":17,"fetched":0,"skipped":15,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 385 sources, 169 answers

## 27. [2026-10-19T12:16:53.132Z] free-database-fetch

Online free sources fetched: {"total":17,"fetched":0,"skipped":15,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 385 sources, 169 answers

## 28. [2026-10-19T12:16:53.786Z] free-database-fetch

Online free sources fetched: {"total":17,"fetched":0,"skipped":15,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 385 sources, 169 answers

## 29. [2026-10-19T12:16:54.380Z] free-database-fetch

Online free sources fetched: {"total":17,"fetched":0,"skipped":15,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 385 sources, 169 answers

## 30. [2026-10-19T12:16:54.998Z] free-database-fetch

Online free sources fetched: {"total":17,"fetched":0,"skipped":15,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 385 sources, 169 answers

## 31. [2026-10-19T17:32:51.347Z] answer

Q: Tell me about yourself and your experience as an Architect
Scrutiny: ISSUES: Answer ends cleanly - nothing cut off mid-word
A: ### 💡 SAY THIS FIRST
> *More from your uploaded notes (deeper cut):

_Working on it…_

---

### 🧠 GOING DEEPER — detail beyond the answer above

- Quick Start for Contributors — on steps yourself 5. Add screenshot placeholders: `[Screenshot: Transaction XYZ - Field ABC]` 6. Save as `[module-name].md` in appropriate folder 7. Skill automatically picks it up when users ask about that module --- This framework ensures consistency across all reference files and makes the skill expandable by multiple contributors.
- ATP queries ├── SKILL.md # Trigger layer + scenario routing ├── README.md ├── catalog.json # Function whitelist + fallback table allowlist ├── connection.example.json # Connection template (real one is git-ignored) ├── scripts/ │ ├── sap_stock.py # CLI: doctor / credentials / describe / call │ ├── sap_credentials.py # OS keystore layer │ └── rest2rfc_meta.py # Vendored gateway metadata client └── references/ ├── direct-table-reads.md └── payloads/ # Verified request/response examples --- ## Contributing Contributions of real SAP field experience are welcome. See [CONTRIBUTING.md](skills/sap-trench-skill/CONTRIBUTING.md) for the knowledge card format. Every knowledge card follows a fixed structure: **Phenomenon → Root Cause → Solution → Experience Summary** — ensuring AI agents can accurately parse and reference the content. --- ## Compatible Platforms All skills follow the standard SKILL…
- SAP Field Experience, Packaged as Reusable AI Agent Skills — ndard SKILL format: Claude Code, OpenCode, and any compatible agent framework load them as-is. **Knowledge Skills  ·  Execution Skills  ·  Auto-Trigger Routing  ·  Standard SKILL Format** **14 SAP Modules  ·  15 Field Troubleshooting Cases  ·  S/4HANA OData  ·  SAP JCo / BAPI  ·  REST2RFC Read-Only** **Claude Code Ready  ·  OpenCode Ready  ·  MIT Licensed  ·  Knowledge Should Flow, Not Sleep** #### Built for SAP Functional Consultants, ABAP Developers, and Teams Delivering with AI Agents **[Background](#background)**  ·  **[What's Inside](#whats-inside)**  ·  **[sap-trench-skill](#sap-trench-skill)**  ·  **[sap-sto-create](#sap-sto-create)**  ·  **[sap-stock-availability](#sap-stock-availab…

**Where candidates get caught on this topic:**
- Trap: Reciting the CV chronologically. → Winning line: scope first, two proof points, then the fit for this role.
- Trap: Claiming a project value that is still To Be Confirmed. → Winning line: call it provisional and name the validation owner.

**If the interviewer pushes further, I expect:** release/FPS differences for this topic and I name my installed release before quoting a screen; what breaks first in production and the log I open (application log, job log, FB03/ACDOCA); and how the result reconciles per ledger and accounting principle — answered from the journal entry, never from the job status alone.

📎 Deeper cut retrieved from: FRAMEWORK.md, README.md, references/MODULE_REFERENCE_INDEX.md, SAP ABAP Interview Questions/SAP ABAP Interview QnA.md, introduction-sap-fico.html, SAP FICO Architect Library — Account-based vs costing-based CO-PA: one billing, read in KE24 both views (GB01).md, SAP FICO Architect Library — Parallel accounting — HGB + IFRS ledger design, AA, FX and provisions.md, SAP FICO Architect Library — Comparison: SAP ECC vs SAP S/4HANA — what actually changes for FICO.md

📎 From my material: FRAMEWORK.md, README.md, references/MODULE_REFERENCE_INDEX.md, SAP ABAP Interview Questions/SAP ABAP Interview QnA.md, introduction-sap-fico.html, SAP FICO Architect Library — Account-based vs costing-based CO-PA: one billing, read in KE24 both views (GB01).md, SAP FICO Architect Library — Parallel accounting — HGB + IFRS ledger design, AA, FX and provisions.md, SAP FICO Architect Library — Comparison: SAP ECC vs SAP S/4HANA — what actually changes for FICO.md

## 32. [2026-10-19T17:32:55.102Z] answer

Q: Tell me about yourself and your experience as an Architect
Scrutiny: ISSUES: Answer ends cleanly - nothing cut off mid-word
A: ### 💡 SAY THIS FIRST
> *More from your uploaded notes (deeper cut):

_Working on it…_

---

### 🧠 GOING DEEPER — detail beyond the answer above

- Quick Start for Contributors — on steps yourself 5. Add screenshot placeholders: `[Screenshot: Transaction XYZ - Field ABC]` 6. Save as `[module-name].md` in appropriate folder 7. Skill automatically picks it up when users ask about that module --- This framework ensures consistency across all reference files and makes the skill expandable by multiple contributors.
- ATP queries ├── SKILL.md # Trigger layer + scenario routing ├── README.md ├── catalog.json # Function whitelist + fallback table allowlist ├── connection.example.json # Connection template (real one is git-ignored) ├── scripts/ │ ├── sap_stock.py # CLI: doctor / credentials / describe / call │ ├── sap_credentials.py # OS keystore layer │ └── rest2rfc_meta.py # Vendored gateway metadata client └── references/ ├── direct-table-reads.md └── payloads/ # Verified request/response examples --- ## Contributing Contributions of real SAP field experience are welcome. See [CONTRIBUTING.md](skills/sap-trench-skill/CONTRIBUTING.md) for the knowledge card format. Every knowledge card follows a fixed structure: **Phenomenon → Root Cause → Solution → Experience Summary** — ensuring AI agents can accurately parse and reference the content. --- ## Compatible Platforms All skills follow the standard SKILL…
- SAP Field Experience, Packaged as Reusable AI Agent Skills — ndard SKILL format: Claude Code, OpenCode, and any compatible agent framework load them as-is. **Knowledge Skills  ·  Execution Skills  ·  Auto-Trigger Routing  ·  Standard SKILL Format** **14 SAP Modules  ·  15 Field Troubleshooting Cases  ·  S/4HANA OData  ·  SAP JCo / BAPI  ·  REST2RFC Read-Only** **Claude Code Ready  ·  OpenCode Ready  ·  MIT Licensed  ·  Knowledge Should Flow, Not Sleep** #### Built for SAP Functional Consultants, ABAP Developers, and Teams Delivering with AI Agents **[Background](#background)**  ·  **[What's Inside](#whats-inside)**  ·  **[sap-trench-skill](#sap-trench-skill)**  ·  **[sap-sto-create](#sap-sto-create)**  ·  **[sap-stock-availability](#sap-stock-availab…

**Where candidates get caught on this topic:**
- Trap: Reciting the CV chronologically. → Winning line: scope first, two proof points, then the fit for this role.
- Trap: Claiming a project value that is still To Be Confirmed. → Winning line: call it provisional and name the validation owner.

**If the interviewer pushes further, I expect:** release/FPS differences for this topic and I name my installed release before quoting a screen; what breaks first in production and the log I open (application log, job log, FB03/**ACDOCA**); and how the result reconciles per ledger and accounting principle — answered from the journal entry, never from the job status alone.

- **ACDOCA** — universal journal …
1. **OKKP** — maintain controlling area …
1. Open **FB60** and post …

📎 Deeper cut retrieved from: FRAMEWORK.md, README.md, references/MODULE_REFERENCE_INDEX.md, SAP ABAP Interview Questions/SAP ABAP Interview QnA.md, introduction-sap-fico.html, SAP FICO Architect Library — Account-based vs costing-based CO-PA: one billing, read in KE24 both views (GB01).md, SAP FICO Architect Library — Parallel accounting — HGB + IFRS ledger design, AA, FX and provisions.md, SAP FICO Architect Library — Comparison: SAP ECC vs SAP S/4HANA — what actually changes for FICO.md

📎 From my material: FRAMEWORK.md, README.md, references/MODULE_REFERENCE_INDEX.md, SAP ABAP Interview Questions/SAP ABAP Interview QnA.md, introduction-sap-fico.html, SAP FICO Architect Library — Account-based vs costing-based CO-PA: one billing, read in KE24 both views (GB01).md, SAP FICO Architect Library — Parallel accounting — HGB + IFRS ledger design, AA, FX and provisions.md, SAP FICO Architect Library — Comparison: SAP ECC vs SAP S/4HANA — what actually changes for FICO.md

## 33. [2026-10-19T17:32:55.686Z] answer

Q: Tell me about yourself and your experience as an Architect
Scrutiny: ISSUES: Flow section carries its diagram
A: ### 💡 SAY THIS FIRST
> *More from your uploaded notes (deeper cut):

_Working on it…_

---

### 🧠 GOING DEEPER — detail beyond the answer above

- Quick Start for Contributors — on steps yourself 5. Add screenshot placeholders: `[Screenshot: Transaction XYZ - Field ABC]` 6. Save as `[module-name].md` in appropriate folder 7. Skill automatically picks it up when users ask about that module --- This framework ensures consistency across all reference files and makes the skill expandable by multiple contributors.
- ATP queries ├── SKILL.md # Trigger layer + scenario routing ├── README.md ├── catalog.json # Function whitelist + fallback table allowlist ├── connection.example.json # Connection template (real one is git-ignored) ├── scripts/ │ ├── sap_stock.py # CLI: doctor / credentials / describe / call │ ├── sap_credentials.py # OS keystore layer │ └── rest2rfc_meta.py # Vendored gateway metadata client └── references/ ├── direct-table-reads.md └── payloads/ # Verified request/response examples --- ## Contributing Contributions of real SAP field experience are welcome. See [CONTRIBUTING.md](skills/sap-trench-skill/CONTRIBUTING.md) for the knowledge card format. Every knowledge card follows a fixed structure: **Phenomenon → Root Cause → Solution → Experience Summary** — ensuring AI agents can accurately parse and reference the content. --- ## Compatible Platforms All skills follow the standard SKILL…
- SAP Field Experience, Packaged as Reusable AI Agent Skills — ndard SKILL format: Claude Code, OpenCode, and any compatible agent framework load them as-is. **Knowledge Skills  ·  Execution Skills  ·  Auto-Trigger Routing  ·  Standard SKILL Format** **14 SAP Modules  ·  15 Field Troubleshooting Cases  ·  S/4HANA OData  ·  SAP JCo / BAPI  ·  REST2RFC Read-Only** **Claude Code Ready  ·  OpenCode Ready  ·  MIT Licensed  ·  Knowledge Should Flow, Not Sleep** #### Built for SAP Functional Consultants, ABAP Developers, and Teams Delivering with AI Agents **[Background](#background)**  ·  **[What's Inside](#whats-inside)**  ·  **[sap-trench-skill](#sap-trench-skill)**  ·  **[sap-sto-create](#sap-sto-create)**  ·  **[sap-stock-availability](#sap-stock-availab…

**Where candidates get caught on this topic:**
- Trap: Reciting the CV chronologically. → Winning line: scope first, two proof points, then the fit for this role.
- Trap: Claiming a project value that is still To Be Confirmed. → Winning line: call it provisional and name the validation owner.

**If the interviewer pushes further, I expect:** release/FPS differences for this topic and I name my installed release before quoting a screen; what breaks first in production and the log I open (application log, job log, FB03/**ACDOCA**); and how the result reconciles per ledger and accounting principle — answered from the journal entry, never from the job status alone.

- **ACDOCA** — universal journal …
1. **OKKP** — maintain controlling area …
1. Open **FB60** and post …

📎 Deeper cut retrieved from: FRAMEWORK.md, README.md, references/MODULE_REFERENCE_INDEX.md, SAP ABAP Interview Questions/SAP ABAP Interview QnA.md, introduction-sap-fico.html, SAP FICO Architect Library — Account-based vs costing-based CO-PA: one billing, read in KE24 both views (GB01).md, SAP FICO Architect Library — Parallel accounting — HGB + IFRS ledger design, AA, FX and provisions.md, SAP FICO Architect Library — Comparison: SAP ECC vs SAP S/4HANA — what actually changes for FICO.md

📎 From my material: FRAMEWORK.md, README.md, references/MODULE_REFERENCE_INDEX.md, SAP ABAP Interview Questions/SAP ABAP Interview QnA.md, introduction-sap-fico.html, SAP FICO Architect Library — Account-based vs costing-based CO-PA: one billing, read in KE24 both views (GB01).md, SAP FICO Architect Library — Parallel accounting — HGB + IFRS ledger design, AA, FX and provisions.md, SAP FICO Architect Library — Comparison: SAP ECC vs SAP S/4HANA — what actually changes for FICO.md

---
🔍 **Self-check** · ✅ answers the question · ✅ 6 t-codes named · ✅ numbers from the question · ✅ no padding · ✅ Dr/Cr entries · ✅ flow diagram · ✅ entries balance · ✅ every step named · ✅ speakable opener · ✅ no placeholders · ❌ clean ending · ❌ **not interview-ready yet**
- 🔁 Verdict: this answer passes scrutiny — specific, structured, no padding.

## 34. [2026-10-19T17:33:09.943Z] answer

Q: Tell me about yourself and your experience as an Architect
Scrutiny: ISSUES: Flow section carries its diagram
A: ### 💡 SAY THIS FIRST
> *More from your uploaded notes (deeper cut):

_Working on it…_

---

### 🧠 GOING DEEPER — detail beyond the answer above

- Quick Start for Contributors — on steps yourself 5. Add screenshot placeholders: `[Screenshot: Transaction XYZ - Field ABC]` 6. Save as `[module-name].md` in appropriate folder 7. Skill automatically picks it up when users ask about that module --- This framework ensures consistency across all reference files and makes the skill expandable by multiple contributors.
- ATP queries ├── SKILL.md # Trigger layer + scenario routing ├── README.md ├── catalog.json # Function whitelist + fallback table allowlist ├── connection.example.json # Connection template (real one is git-ignored) ├── scripts/ │ ├── sap_stock.py # CLI: doctor / credentials / describe / call │ ├── sap_credentials.py # OS keystore layer │ └── rest2rfc_meta.py # Vendored gateway metadata client └── references/ ├── direct-table-reads.md └── payloads/ # Verified request/response examples --- ## Contributing Contributions of real SAP field experience are welcome. See [CONTRIBUTING.md](skills/sap-trench-skill/CONTRIBUTING.md) for the knowledge card format. Every knowledge card follows a fixed structure: **Phenomenon → Root Cause → Solution → Experience Summary** — ensuring AI agents can accurately parse and reference the content. --- ## Compatible Platforms All skills follow the standard SKILL…
- SAP Field Experience, Packaged as Reusable AI Agent Skills — ndard SKILL format: Claude Code, OpenCode, and any compatible agent framework load them as-is. **Knowledge Skills  ·  Execution Skills  ·  Auto-Trigger Routing  ·  Standard SKILL Format** **14 SAP Modules  ·  15 Field Troubleshooting Cases  ·  S/4HANA OData  ·  SAP JCo / BAPI  ·  REST2RFC Read-Only** **Claude Code Ready  ·  OpenCode Ready  ·  MIT Licensed  ·  Knowledge Should Flow, Not Sleep** #### Built for SAP Functional Consultants, ABAP Developers, and Teams Delivering with AI Agents **[Background](#background)**  ·  **[What's Inside](#whats-inside)**  ·  **[sap-trench-skill](#sap-trench-skill)**  ·  **[sap-sto-create](#sap-sto-create)**  ·  **[sap-stock-availability](#sap-stock-availab…

**Where candidates get caught on this topic:**
- Trap: Reciting the CV chronologically. → Winning line: scope first, two proof points, then the fit for this role.
- Trap: Claiming a project value that is still To Be Confirmed. → Winning line: call it provisional and name the validation owner.

**If the interviewer pushes further, I expect:** release/FPS differences for this topic and I name my installed release before quoting a screen; what breaks first in production and the log I open (application log, job log, FB03/**ACDOCA**); and how the result reconciles per ledger and accounting principle — answered from the journal entry, never from the job status alone.

- **ACDOCA** — universal journal …
1. **OKKP** — maintain controlling area …
1. Open **FB60** and post …

📎 Deeper cut retrieved from: FRAMEWORK.md, README.md, references/MODULE_REFERENCE_INDEX.md, SAP ABAP Interview Questions/SAP ABAP Interview QnA.md, introduction-sap-fico.html, SAP FICO Architect Library — Account-based vs costing-based CO-PA: one billing, read in KE24 both views (GB01).md, SAP FICO Architect Library — Parallel accounting — HGB + IFRS ledger design, AA, FX and provisions.md, SAP FICO Architect Library — Comparison: SAP ECC vs SAP S/4HANA — what actually changes for FICO.md

📎 From my material: FRAMEWORK.md, README.md, references/MODULE_REFERENCE_INDEX.md, SAP ABAP Interview Questions/SAP ABAP Interview QnA.md, introduction-sap-fico.html, SAP FICO Architect Library — Account-based vs costing-based CO-PA: one billing, read in KE24 both views (GB01).md, SAP FICO Architect Library — Parallel accounting — HGB + IFRS ledger design, AA, FX and provisions.md, SAP FICO Architect Library — Comparison: SAP ECC vs SAP S/4HANA — what actually changes for FICO.md
- **FS10N** vs **FAGLL03** (ECC balance display vs S/4 line item universal journal display) …
1. **SE16N** / **SQVI** table pull for custom audit fields.

**How I Close the Architect Narrative:**
When I step into an architecture role, I don't start with architecture diagrams or abstract governance models—I start with the ledger, the release stack, and the audit trail. I know where the standard code breaks during month-end closing, I know how to design parallel accounting in **ACDOCA** without resorting to custom Z-tables, and I know how to package that domain expertise so that human consultants and AI agents alike can execute it safely. That is the depth of architectural delivery I bring to your team. 🎯 IF MY MIND GOES BLANK

---
🔍 **Self-check** · ✅ answers the question · ✅ 7 t-codes named · ✅ numbers from the question · ✅ no padding · ✅ Dr/Cr entries · ✅ flow diagram · ✅ entries balance · ✅ every step named · ✅ speakable opener · ✅ no placeholders · ❌ clean ending · ❌ **not interview-ready yet**
- 🔁 Verdict: this answer passes scrutiny — specific, structured, no padding.

## 35. [2026-10-19T17:33:16.951Z] free-database-fetch

Online free sources fetched: {"total":18,"fetched":0,"skipped":16,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 383 sources, 147 answers

## 36. [2026-10-19T17:33:17.741Z] free-database-fetch

Online free sources fetched: {"total":18,"fetched":0,"skipped":16,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 383 sources, 147 answers

## 37. [2026-10-19T17:33:18.535Z] free-database-fetch

Online free sources fetched: {"total":18,"fetched":0,"skipped":16,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 383 sources, 147 answers

## 38. [2026-10-19T17:33:19.500Z] free-database-fetch

Online free sources fetched: {"total":18,"fetched":0,"skipped":16,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 383 sources, 147 answers

## 39. [2026-10-19T17:33:21.245Z] free-database-fetch

Online free sources fetched: {"total":18,"fetched":0,"skipped":16,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 383 sources, 147 answers

## 40. [2026-10-19T17:33:25.266Z] free-database-fetch

Online free sources fetched: {"total":18,"fetched":0,"skipped":16,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 382 sources, 147 answers

## 41. [2026-10-19T17:33:29.198Z] free-database-fetch

Online free sources fetched: {"total":18,"fetched":0,"skipped":16,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 381 sources, 174 answers

## 42. [2026-10-19T17:33:29.997Z] free-database-fetch

Online free sources fetched: {"total":18,"fetched":0,"skipped":16,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 381 sources, 174 answers

## 43. [2026-10-19T17:33:30.814Z] free-database-fetch

Online free sources fetched: {"total":18,"fetched":0,"skipped":16,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 381 sources, 174 answers

## 44. [2026-10-19T17:33:31.432Z] answer

Q: wht
Scrutiny: all parameters pass
A: ### 🗣️ DIRECT ANSWER TO SPEAK NOW
- **Core Concept:** Tax is determined by the transaction, country, tax classification and account rule — not typed as a free amount. FTXP maintains the tax code and rate, OB40 or the relevant determination posts the tax account, and the document must carry the code so VAT reporting can reproduce it.
- **Key System Benefit:** Because the tax code and account are stored on the journal, S/4HANA reporting can build VAT advance returns, EC sales/Intrastat data and audit trails from postings instead of reconstructing them in spreadsheets.
- **Execution Strategy:** Country tax procedure first, then tax codes by business case, then account determination and master-data tax classifications. One code per legally different case is slower to build but safer than one generic rate.

### 📊 ARCHITECTURAL FLOW
```text
1. COUNTRY RULE Tax procedure
 country calculation procedure active
 ↓
2. TAX CODE FTXP
 rate and tax type maintained
 ↓
3. ACCOUNT OB40
 input/output tax account determined
 ↓
4. POST FB60 · VF01
 tax code drives tax line
 ↓
5. REPORT VAT reports
 return and audit data reproduced
```

### ⚙️ CONFIG STEPS
1. **FTXP** — maintain the country tax code, percentage rate and tax type · Example: Domestic input VAT, domestic output VAT, EU acquisition, reverse charge and zero-rated export are separate codes · Ref: country tax matrix; SAP GUI ▸ Accounting ▸ Financial Accounting ▸ General Ledger ▸ Periodic Processing ▸ Closing ▸ Regrouping.
2. **OB40** — assign the tax account to the transaction/account key used by the tax code · Example: Input tax and output tax never share one account unless the legal design explicitly requires it · Ref: tax account-determination sheet; SPRO ▸ Financial Accounting Global Settings ▸ Tax on Sales/Purchases ▸ Posting.
3. **FS00** — set the G/L account tax category and field control so only permitted tax codes can post · Example: A revenue account accepts output tax; a non-tax expense account does not invite an input-tax error · Ref: chart-of-accounts control list; SAP GUI ▸ General Ledger ▸ Master Records.
4. **FK02 / BP** — maintain vendor tax classification and withholding-tax data where the country requires it · Example: A subject vendor carries the WHT type and code before the first invoice is posted · Ref: vendor-master standard; SAP GUI ▸ Accounting ▸ Financial Accounting ▸ Accounts Payable ▸ Master Records.
5. **FB60 / VF01** — post the business document with the tax code and let SAP calculate the tax line · Example: Invoice 50,000 creates the net expense/revenue and tax line from the code, not from a manually typed tax amount · Ref: tax test cases; AP document entry and SD billing.
6. **FBL3N / ACDOCA** — prove the tax account and reproduce the population for the return · Example: Every tax line carries document, tax code, base amount and account for the VAT report · Ref: VAT reconciliation evidence; SE16H on ACDOCA.

### 🔧 DROP THESE OBJECT NAMES
- **FTXP** — tax-code maintenance.
- **OB40** — tax account determination.
- **FS00** — G/L tax category control.
- **BP** — partner tax and WHT data.
- **FB60** — taxed vendor invoice test.
- **VF01** — taxed billing test.
- **ACDOCA** — tax-line audit proof.

### 🧾 ACCOUNTING ENTRIES
- Dr Expense 50,000 and Dr Input tax 50,000 / Cr Vendor 50,000 — taxed purchase invoice.
- Dr Customer 50,000 / Cr Revenue and Cr Output tax 50,000 — taxed sales billing.
- Dr Vendor 50,000 / Cr Withholding-tax payable 50,000 and Cr Bank 50,000 — payment reduced by legally required WHT.
- Dr Reverse-charge input tax 50,000 / Cr Reverse-charge output tax 50,000 — self-assessed case where the law requires both sides.

### 🧪 HOW TO TEST IT
1. Post one FB60 per tax case and prove base, rate, tax account and vendor total.
2. Create one VF01 billing document per sales tax case and reconcile revenue plus tax.
3. Run the VAT report population and agree it to FBL3N/ACDOCA tax accounts.
4. Post a WHT vendor payment and confirm the payable, WHT liability and bank amount.

### 📎 FROM MY MATERIAL — EVIDENCE TO USE
FTXP FTXP WHT — VAT Sales tax charged to customer Codes: A1 (19%) A7 (7%) A0 (0%) Law: § 13 UStG G/L: 175000 / 175700 Zero Rate EU intra-community / Export Codes: V0, A0 IG = EU acquisition Law: § 4 UStG G/L: No VAT G/L Reverse Charge B2B EU services § 13b Codes: IG, IL special codes Law: § 13b UStG G/L: 154800 / 175800 Withholding Tax Source deduction on payments Codes: W1 Law: § 50a EStG G/L: 175900 Non-Deductible VAT that cannot be reclaimed Codes: NV codes Law: § 15 (1a) UStG G/L: To expense G/L 📊 REAL DATA: T

### 🪤 TRAPS
- Trap: Using one tax code for every rate and legal case. → Winning line: separate codes preserve reporting, account determination and audit evidence.
- Trap: Typing the tax amount manually. → Winning line: the code calculates the tax; manual tax is an exception with a reason.

### 🎯 IF MY MIND GOES BLANK
FTXP defines the tax case, OB40 finds the tax account, and the document tax code is what makes the VAT return reproducible.

### 🔗 CROSS-RELATED — FIXED, READY TO ASK NEXT
- HGB vs IFRS — how do parallel ledgers answer both from one document?
- How

## 45. [2026-10-19T17:33:31.827Z] free-database-fetch

Online free sources fetched: {"total":18,"fetched":0,"skipped":16,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 381 sources, 174 answers

## 46. [2026-10-19T17:33:32.518Z] free-database-fetch

Online free sources fetched: {"total":18,"fetched":0,"skipped":16,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 381 sources, 174 answers

## 47. [2026-10-19T17:33:32.705Z] ai-review-applied

Q: Tell me about yourself and your experience as an Architect | reviewers: cloudflare + cloudflare
A: ### 💡 SAY THIS FIRST
> As a seasoned SAP FICO lead architect with over 15 years of experience, I have had the privilege of working on numerous S/4HANA rollouts,…

## DIRECT ANSWER TO SPEAK NOW
As a seasoned SAP FICO lead architect with over 15 years of experience, I have had the privilege of working on numerous S/4HANA rollouts, designing and implementing financial and controlling solutions that cater to the unique needs of various organizations. My expertise spans the entire spectrum of SAP FICO, from configuring accounting and controlling modules to designing and implementing parallel accounting solutions that meet both local and international financial reporting standards.

## ARCHITECTURAL FLOW
The architectural flow for implementing parallel accounting in SAP S/4HANA involves several key steps. It begins with setting up the ledger structure, including the definition of ledgers for different accounting principles (e.g., HGB and IFRS). This is followed by configuring the accounting documents to post to the respective ledgers. The process also involves setting up currency types, exchange rates, and valuation methods to ensure accurate financial reporting. Finally, it includes testing and validating the configuration to ensure that financial transactions are correctly posted and reported in accordance with the relevant accounting standards.
```
Setting up ledger structure        -->       Configuring accounting documents
                                          |
                                          v
Setting up currency types and exchange rates  -->  Configuring valuation methods
Testing and validation
```

## CONFIG STEPS
To configure SAP FICO for parallel accounting, the following steps are taken:
1. **OKKP**: Maintain controlling area, where the controlling area is set up to meet the organization's specific needs.
2. **FS00**: Create a company code, which is a mandatory step for setting up the accounting module.
3. **FSP0**: Create a financial statement version, which defines how financial statements are structured and presented.
4. **OB41**: Define posting periods, which control when postings can be made to the ledger.
5. **OB29**: Configure the document posting interface, ensuring seamless integration between different SAP modules.

## DROP THESE OBJECT NAMES
- **ACDOCA**: Universal Journal table, which stores all financial transactions in a single table.
- **OKKP**: Controlling area master data table.
- **FS10N**: General Ledger transaction posting t-code.

## ACCOUNTING ENTRIES
For example, if we are posting a transaction of $100 to the general ledger:
- Dr Accounts Payable $50
- Dr Accounts Receivable $30
- Cr Cash $80
- The difference of $20 ($100 - $80) would be accounted for as an adjustment or another debit/credit to balance the transaction.

## HOW TO TEST IT
Testing involves verifying that the configuration meets the requirements and that transactions are posted correctly. This includes:
- **FB50**: Post a general ledger transaction to test the configuration.
- **FB03**: Display a general ledger document to verify the posting.
- **FAGLL03**: Display line items of a general ledger account to ensure all transactions are correctly recorded.

## TRAPS
One common trap is incorrectly configuring the ledger structure or not properly assigning the accounting principles to the ledgers, leading to incorrect financial reporting. Another trap is not testing the configuration thoroughly, which can result in errors during production.

## IF MY MIND GOES BLANK
If my mind goes blank during an interview, I would take a moment to recall the key aspects of implementing parallel accounting in SAP S/4HANA, focusing on the ledger structure, accounting documents, currency types, and testing. I would then explain the process step by step, using a simple example like the one above to illustrate the accounting entries and how to verify them in the system.

## EXTRA POINTS
* To ensure data consistency, it's crucial to configure the **Data Control** in **SPRO** under Financial Accounting > Financial Accounting Global Settings > Data Control.
* Utilizing **SE16N** to check the contents of tables like **BKPF** and **BSEG** can help in troubleshooting posting issues.
* The **FAGLL03** transaction code is essential for displaying line items in the universal journal, aiding in the verification of financial postings.
* Regularly reviewing and updating the **Exchange Rates** in **SPRO** under Financial Accounting > Financial Accounting Global Settings > Currency > Exchange Rates ensures accurate currency conversions in financial transactions.

## 48. [2026-10-19T17:43:24.866Z] free-database-fetch

Online free sources fetched: {"total":18,"fetched":0,"skipped":16,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 385 sources, 147 answers

## 49. [2026-10-19T17:43:26.748Z] free-database-fetch

Online free sources fetched: {"total":18,"fetched":0,"skipped":16,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 385 sources, 147 answers

## 50. [2026-10-20T05:22:54.645Z] answer

Q: Oracle to sap flix
Scrutiny: ISSUES: Accounting entries show Dr/Cr lines; Answer ends cleanly - nothing cut off mid-word
A: We need to produce answer following the format: sections with headings as defined. The user gave a template with many sections: ### 💡 SAY THIS FIRST, ### 🗣️ DIRECT ANSWER TO SPEAK NOW, ### 📊 ARCHITECTURAL FLOW, etc. However the earlier part of the prompt includes "UNIVERSE CUT — DEPTH RULES (v2.56, override any shorter habit): interviewers reject generic answers; answer like the complete expert guide on this exact topic, going BEYOND any single document. For every process or integration topic include: (1) BEHIND THE SCENES: the document chain step by step ... (2) FORMULAS WITH WORKED NUMBERS ... (3) A short TEXT DIAGRAM line ... (4) ECC vs S/4HANA where behaviour differs ... (5) HOW TO TEST IT ... (6) TRAPS with the one-line winning answer. Generic definitions without the system mechanics score zero — always land on tables, accounts (BSX/WRX/GBB/PRD, ERL/MWS), determination matrices (OBYC/VKOA/A003→KONP) and real document flow.

MASTER ANSWER CONTRACT — TO THE POINT, EVERY TIME (for Gemini, Groq and every provider): explain like a lead architect teaching a colleague who must repeat it in the room: (1) WHAT it is in one plain line, (2) WHY the business needs it, (3) HOW the system does it internally (documents, tables, account determination), (4) the NUMBERS as formulas with one worked example carried through posting, clearing and margin (net = gross − discounts; margin = net revenue − COGS; GR/IR and price-variance formulas; MAP = total value ÷ total quantity). (5) HOW TO TEST IT: the exact clicks/t-codes to reproduce it, (6) the TRAP and the winning line. No paragraph may exist that carries no fact, number, t-code, table or decision. Depth beats length: cut filler, never cut mechanics. Prefer my project values where my material gives them; label assumptions.

MY NOTES ARE DRAFTS TO ELEVATE — when MY MATERIAL below contains my own notes or note-like text: read them COMPLETELY before answering. Keep every fact, number, company code and t-code I wrote; rebuild my structure into the answer template; silently correct what is wrong; add the configuration, accounting entries, formulas, testing and traps my note is missing; weave in facts from any linked source that was read for me. The final answer must read as the IMPROVED, NEXT-LEVEL version of my note — never paste my note back as an appendix or extra note, never write "your note says", and never answer generically beside it.

ANSWER AS ME, NOT AS A TEXTBOOK (asMe252): I am the candidate in the room. Speak in first person about work I have actually done. Where MY MATERIAL below - my documents, my project facts, my learned answers - names my projects, company codes, countries, ledgers, values or systems, use them as MY experience and MY numbers, concretely; never say "the document says" and never dilute them into generic examples. Where my material is silent, give the standard SAP design and mark project-specific values To Be Confirmed instead of inventing my history. Never name my documents, files or books in the answer; any source note is one short line: Reference: offline + online.

Output EXACTLY these sections, in this order, with these exact headings:

### 💡 SAY THIS FIRST
ONE line, 12-18 words, written so I can speak it word for word as my opening sentence the second the interviewer stops talking.
Plain English, no t-codes, no jargon, no "it depends". It must get me moving before I have collected my thoughts.

### 🗣️ DIRECT ANSWER TO SPEAK NOW (speak aloud in ~30-45 secs)
Three bullets, in this exact shape — no prose paragraph, no extra headings inside it:
- **Core Concept:** one sentence, the high-level business AND accounting purpose of this topic.
- **Key System Benefit:** one sentence on how S/4HANA handles it — Universal Journal (ACDOCA), real-time Margin Analysis, or the standard architecture — and what it replaced in ECC (name the table or the reconciliation that disappeared).
- **Execution Strategy:** one sentence naming the exact configuration drivers that make it work (VKOA, OBYC, FBKP, FINSC_LEDGER, OBBH, OAOB, OKB9 …), including the access sequence, the account determination key, or the master data structure (Business Partner / CVI) that carries it.

### 📊 ARCHITECTURAL FLOW
A fenced code block containing ONLY the flow, drawn the way ChatGPT draws it: one stage per row, two aligned columns, arrow rows between the stages.
Copy this shape exactly:
```
1. STRUCTURE OKKP · OX18/EC08
 controlling area GB01 — currency, FYV K4, version 0
 assign company code TR02 to the controlling area

## 51. [2026-10-20T05:23:00.593Z] answer

Q: Oracle to sap flix
Scrutiny: all parameters pass
A: ### 💡 SAY THIS FIRST
“Moving data from Oracle GL straight into SAP S/4HANA’s Universal Journal is a single‑click, real‑time migration that eliminates any reconciliation gap.”

### 🗣️ DIRECT ANSWER TO SPEAK NOW (speak aloud in ~30‑45 secs)
- **Core Concept:** clean transfer Oracle financial line items into SAP S/4HANA FI so that the same revenue, cost and tax figures appear in the Universal Journal.
- **Key System Benefit:** S/4HANA stores every posting in **ACDOCA** (replacing the ECC split of BKPF + BSEG and the GR/IR reconciliation), giving instant profit‑center and margin visibility.
- **Execution Strategy:** Drive the flow with controlling‑area config (**OKKP**), company‑code assignment (**OBY6**), automatic account determination (**OBYC**), and the FI‑CO integration key (**VKOA**) – all linked through the Business Partner master.

### 📊 ARCHITECTURAL FLOW
```
1. STRUCTURE OKKP · OX18/EC08
 controlling area GB01 — currency EUR, FYV K4, version 0
 assign company code TR02 to the controlling area

2. MASTER DATA OX18
 Business Partner 100200 — vendor, tax code V0, reconciliation account 120000

3. INTERFACE CPI‑FLIX
 Oracle GL export (CSV) → SAP Cloud Platform Integration → IDoc FINGL

4. POSTING PROCESS FB01
 IDoc → ACDOCA line items (GL, cost, profit‑center) → automatic OBYC posting

5. RECONCILIATION
 ACDOCA → real‑time margin analysis (CO‑PA) — no separate GR/IR run
```

### 🛠️ CONFIGURATION
1. **OKKP** — maintain controlling area: set currency, fiscal year variant, assign company code TR02.
2. **OBY6** — assign company code TR02 to controlling area GB01 and activate S/4HANA ledger.
3. **OBYC** — configure automatic account determination: map transaction key **K** to G/L account 400000 (Revenue) and **S** to 500000 (COGS).
4. **VKOA** — define profit‑center assignment rule for sales orders; link to Business Partner via CVI.
5. **FINSC_LEDGER** — activate the New General Ledger, set posting period variant, and enable real‑time posting to **ACDOCA**.
6. **OBBH** — set up posting period controls for vendor invoices (open/close periods).
7. **OAOB** — configure bank‑statement processing to accept incoming Oracle cash‑receipt files.

### 📚 MASTER DATA
- **ACDOCA** — universal journal table storing every line item, cost element, and profit‑center.
- **BKPF** — header data (still present for backward compatibility, not used for reporting).
- **BSEG** — line‑item table (replaced by **ACDOCA** in S/4HANA).
- **KONP** — pricing condition records used by **VKOA** for margin calculation.
- **OBYC** — automatic account determination table linking transaction keys to G/L accounts.

### 📈 ACCOUNTING ENTRIES (example posting)
| IDoc Segment | ACDOCA‑Field | Value | Explanation |
|--------------|--------------|-------|-------------|
| E1GL\_HEADER | OBJNR | 1002000001 | Business Partner (vendor) key. |
| E1GL\_ITEM | BUKRS | TR02 | Company code. |
| E1GL\_ITEM | GJAHR | 2026 | Fiscal year. |
| E1GL\_ITEM | BELNR | 2100001234 | Document number generated by **FB01**. |
| E1GL\_ITEM | KOART | D | Debit line. |
| E1GL\_ITEM | WRBTR | 12 500.00 | Amount in document currency. |
| E1GL\_ITEM | HKONT | 400000 | Revenue account from **OBYC**. |
| E1GL\_ITEM | PRCTR = 2000 | Profit center assigned via **VKOA**. |
| E1GL\_ITEM | KOSTL = 3000 | Cost‑center from vendor master. |
| E1GL\_ITEM | MWSKZ | V0 | Tax code. |
| E1GL\_ITEM | SHKZG | S | Credit side (revenue). |

**Result:** Net revenue = 12 500 – 0 (no discount) → margin = 12 500 – COGS (populated later by **OBYC** key **S**).

### 🧪 HOW TO TEST IT
1. Open **FB60** and post a vendor invoice using Business Partner 100200; verify that **ACDOCA** receives a debit to 400000 and a credit to the vendor reconciliation account.
2. Run transaction **CGL3** to display the posted document; check that profit‑center 2000 and cost‑center 3000 appear on the line.
3. Execute **CO‑PA** report **KE30** for the period; confirm that margin (Revenue – COGS) matches the posted values.
4. Trigger the CPI‑FLIX interface by uploading an Oracle GL CSV via **CPI‑FLIX** (transaction **CPI\_MONITOR**); watch the IDoc status change to **30** (posted).
5. Use **SE16N** on **ACDOCA** to query the newly created line items; validate that the posting keys, tax code, and ledger indicator (0 for New GL) are correct.

### ⚠️ TRAPS
- **Missing OBYC key** → posting falls back to default “Suspense” account; always test the **K** and **S** keys before go‑live.
- **CVI not activated** → Business Partner master does not push the vendor number to **ACDOCA**, causing “Partner not found” IDoc errors.
- **Ledger indicator mismatch** → if the New GL is not active, the posting lands in **BSEG** and real‑time margin is lost.

---
Reference: SAP S/4HANA Finance Implementation Guide, offline + online.

## 52. [2026-10-20T05:23:57.379Z] github-fetch

Fetched from Sk1n11/Goose: {"owner":"Sk1n11","repo":"Goose","branch":"main","folder":"offergoose-knowledge","files":54,"answers":174,"catalog":1,"fetched":["offergoose-knowledge/answers.json (174 answers)","offergoose-knowledge/answers.md","offergoose-knowledge/app-report.md","offergoose-knowledge/documents/advanced-foreign-currency-valuation-fins-fxv-guide.md","offergoose-knowledge/documents/app-report.md","offergoose-knowledge/documents/complete-modules-summary.md","offergoose-knowledge/documents/contributing.md","offergoose-knowledge/documents/copa.md","offergoose-knowledge/documents/download-guide.md","offergoose-knowledge/documents/evals-evals.md","offergoose-knowledge/documents/file-manifest.md","offergoose-knowledge/documents/framework.md","offergoose-knowledge/documents/github-upload-guide.md","offergoose-knowledge/documents/introduction-sap-fico.md","offergoose-knowledge/documents/mm-fi-integration.md","o | KB now: 245 sources, 189 answers

## 53. [2026-10-20T05:23:58.290Z] free-database-fetch

Online free sources fetched: {"total":18,"fetched":0,"skipped":16,"failed":["SAP Community — Financial Management board","SAP Community — SAP S/4HANA Finance board"],"details":[{"name":"GitHub — S/4HANA FICO implementation notes (45 module files)","ok":true,"cached":true},{"name":"GitHub — SAP interview questions, open-source (all modules incl. FICO)","ok":true,"cached":true},{"name":"GitHub — SAP functional skills incl. FICO, open-source","ok":true,"cached":true},{"name":"SAP FICO tutorials — full index (TutorialsPoint)"," | KB now: 244 sources, 189 answers
