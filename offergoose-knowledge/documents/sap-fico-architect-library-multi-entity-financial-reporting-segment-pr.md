# SAP FICO Architect Library — Multi-entity financial reporting — segment, profit centre and entity reporting.md

Topic: SAP FICO Reference Library

Multi-entity financial reporting — segment, profit centre and entity reporting — # Multi-entity financial reporting — segment, profit centre and entity reporting

### 🗣️ DIRECT ANSWER TO SPEAK NOW
- **Core Concept:** For a group like Cybex with 25+ company codes in one S/4HANA, multi-entity reporting means three things: entity-level reports (trial balance, B/S, P&L per company code), management segment reports (by controlling area, profit centre or segment), and consolidated group reports (after intercompany elimination). The first two come straight out of ACDOCA by filtering on the relevant dimension; the third requires Group Reporting or a consolidation tool.
- **Key System Benefit:** One S/4HANA system means all three reporting layers read from ACDOCA without data movement, reconciliation or BW replication; month-end is the same S/4 close for every entity, and the group consolidation uses the same data.
- **Execution Strategy:** Design the reporting hierarchy before go-live: which company codes belong to which segment, which segments roll up to the group. The profit centre hierarchy is the management view; the company code hierarchy is the legal view; the consolidation group in Group Reporting is the external view. All three must be consistent — a company code must belong to exactly one profit centre and one consolidation unit.

### 📊 ARCHITECTURAL FLOW

🗣️ DIRECT ANSWER TO SPEAK NOW — legal view; the consolidation group in Group Reporting is the external view. All three must be consistent — a company code must belong to exactly one profit centre and one consolidation unit.

### 📊 ARCHITECTURAL FLOW
```text
ENTITY LEVEL F0718 / F.01 / FAGLB03
 Trial balance, B/S and P&L per company code — straight from ACDOCA filtered by company code
 ↓
PROFIT CENTRE Fiori Profit Center — Actual/Plan
 P&L and balance sheet by profit centre — reads ACDOCA filtered by profit centre; requires profit centre derivation on all documents
 ↓
SEGMENT Fiori Segment Reporting (IFRS 8)
 External segment B/S and P&L — requires document splitting to be active; reads ACDOCA segment field
 ↓
CONTROLLING AREA KE30 / Fiori Margin Analysis
 Contribution margin by operating concern characteristics — reads ACDOCA with CO attributes
 ↓
GROUP CONSOLIDATION SAP Group Reporting / SEM-BCS
 Eliminate intercompany, translate currencies, adjust for group policies — runs on ACDOCA via Group Reporting
 ↓
DISCLOSURE Fiori Group Financial Statements
 IFRS/HKFRS consolidated B/S, P&L, cash flow, segment note, EPS — published by Group Reporting
```

### ⚙️ CONFIG STEPS
1.

📊 ARCHITECTURAL FLOW — roup policies — runs on ACDOCA via Group Reporting
 ↓
DISCLOSURE Fiori Group Financial Statements
 IFRS/HKFRS consolidated B/S, P&L, cash flow, segment note, EPS — published by Group Reporting
```

### ⚙️ CONFIG STEPS
1. **Financial statement version (OB58)** — design one group financial statement version and one local version per chart of accounts; the group version maps to the IFRS/HKFRS taxonomy · Example: The group version is the hierarchy used by F0718 and Group Reporting for the consolidated financial statements; local versions are used for statutory reports per entity · SPRO ▸ Financial Accounting Global Settings ▸ Document ▸ Define Financial Statement Versions.
2. **Profit centre standard hierarchy (3KEH)** — build the profit centre hierarchy so management P&L can be sliced at any level from the individual store to the division to the group · Example: Every master data object (cost centre, WBS, sales order) that posts to FI must have a profit centre assigned; an unassigned profit centre is "corporate unallocated" and must be investigated · Transaction 3KEH ▸ Maintain Standard Hierarchy.
3.

⚙️ CONFIG STEPS — ct (cost centre, WBS, sales order) that posts to FI must have a profit centre assigned; an unassigned profit centre is "corporate unallocated" and must be investigated · Transaction 3KEH ▸ Maintain Standard Hierarchy.
3. **Segment derivation (Fiori Configure Segment Reporting)** — map each profit centre to a segment so the external IFRS 8 segment note can be produced without manual reclassification · Example: A profit centre not mapped to a segment produces unassigned items in the segment report; map every profit centre before activating document splitting · Fiori Configure Segment Reporting ▸ Assign Profit Centre to Segment.
4. **FBICR3 / Group Reporting IC elimination** — configure the intercompany relationships (trading partner pairs) so IC elimination matches the AR in entity A to the AP in entity B · Example: The RASSC field (trading partner) must be populated on every intercompany document; blank RASSC means the elimination cannot match the document · Transaction FBICR3 or Fiori Group Reporting ▸ Configure Intercompany Elimination.

### 🔧 DROP THESE OBJECT NAMES
- **OB58** — financial statement version — the account hierarchy for B/S and P&L reports.
- **3KEH** — profit centre standard hierarchy — management reporting structure.

⚙️ CONFIG STEPS — pany Elimination.

### 🔧 DROP THESE OBJECT NAMES
- **OB58** — financial statement version — the account hierarchy for B/S and P&L reports.
- **3KEH** — profit centre standard hierarchy — management reporting structure.
- **SEGMENT field in ACDOCA** — external IFRS 8 segment — populated via document splitting.
- **RASSC** — trading partner field in FI documents — drives IC elimination.
- **FBICR3** — intercompany reconciliation — matches IC receivables to IC payables.
- **Group Reporting** — SAP S/4HANA Group Reporting — consolidation on ACDOCA.

### 🧾 ACCOUNTING ENTRIES
- Entity P&L (ACDOCA filter company code): all revenue and expense lines for the entity — read-only, no posting
- IC elimination (Group Reporting): Dr IC revenue 1,000 / Cr IC cost 1,000 — eliminates the intercompany margin at group level; net zero at group P&L

### 🧪 HOW TO TEST IT
1. Post one intercompany invoice; run FBICR3 and confirm the AR in one entity matches the AP in the other; any difference over EUR 1 is a defect.
2. Run F0718 for the group FSV and compare the consolidated total to the sum of the entity totals minus the intercompany eliminations; they must agree.
3. Build the Fiori segment report; confirm the segment totals equal the company-code totals and the segment balance sheet balances.
4.

🧪 HOW TO TEST IT — to the sum of the entity totals minus the intercompany eliminations; they must agree.
3. Build the Fiori segment report; confirm the segment totals equal the company-code totals and the segment balance sheet balances.
4. Run Group Reporting for one period; confirm the translation difference posts to the correct equity account and the consolidated equity reconciles to the sum of entity equities minus IC eliminations.

### 🪤 TRAPS
- Trap: Profit centre not assigned on all documents → Winning line: A missing profit centre produces "unallocated" in the management P&L. Fix master data defaults (OKB9, material master, cost centre) before go-live.
- Trap: IC trading partner missing on cross-entity documents → Winning line: Without RASSC, Group Reporting cannot identify which entity is the counterpart and the IC elimination fails. Enforce RASSC via field status or substitution.

### 🎯 IF MY MIND GOES BLANK
Entity B/S from ACDOCA filtered by company code. Segment B/S from ACDOCA filtered by segment field (needs document splitting). Consolidated B/S from Group Reporting after IC elimination.

### 🔗 CROSS-RELATED — FIXED, READY TO ASK NEXT
- HGB vs IFRS — how do parallel ledgers answer both from one document?
- How will you set up a company code for a new-country rollout?

🎯 IF MY MIND GOES BLANK — oup Reporting after IC elimination.

### 🔗 CROSS-RELATED — FIXED, READY TO ASK NEXT
- HGB vs IFRS — how do parallel ledgers answer both from one document?
- How will you set up a company code for a new-country rollout?
- How does the Universal Journal (ACDOCA) change the month-end close?