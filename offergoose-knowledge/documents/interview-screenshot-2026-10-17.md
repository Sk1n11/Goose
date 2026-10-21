# Interview screenshot 2026-10-17.jpg

Topic: Screenshots

[Local OCR · confidence 55%]
NA H rocess.
Cybex - SAP IA MM-FI Integration (Procure-to-Pay) Ocyb ras
From Purchase Requisition to Vendor Payment — Complete Guide J Cy! ex An eel
Configuration « Determination Logic « Accounting Entries « Examples + Reporting etutiom fors Better Tomonron: Better BS
@ End-to-End Procure-to-Pay (P2P) Process Flow @ Process Highlights
Purchase Purchase © Receipt Invoice Outgoing ti
ON, OME @ win © Ji, © SEM Q bein | © wesw
(MESTN) (ME21N) fly (MIRO) (FT107F-53) A ©»
tomatic account determination
BE Ww © BB Of dl erm
=, = eal-time postings to ACDOCA
oe € = [1] posting
+ intemal request + Legally binding * Receive goods * MotchPO+GR+Imvoice + Automaticormanval + Balance Sheet, PBL @ supports stock, services, assets
for goods/services contract with vendor instock or seniceentty pot vendor ably payment (SEPA, wire) = Vendor open ems (FBLIN) Hoxaos ton dicot
i Fl ting Ma Fl posting Rh + DIGRAR Input Tax PRO fany) + Dr Vendor (AP) « Material ledger & costs @ Hands ax, discounts, variances
Shams «Cr Vendor (AP) « CrBank (House Bank) + Audit trail (ACDOCA) @ Works forlocal and group reporting
[2] Key Master Data Elements (MM-FI) [3] Account Assignment Categories (ME21N) [5) Material Master - 5 Level Hierarchy

ms «Cr Vendor (AP) « CrBank (House Bank) + Audit trail (ACDOCA) @ Works forlocal and group reporting
[2] Key Master Data Elements (MM-FI) [3] Account Assignment Categories (ME21N) [5) Material Master - 5 Level Hierarchy
Object / Field Example (box) Purpose Description Level ProdoctCategary
A py
Company Cote DEDI (Geary) Legale, cureny, Con 5 Inventory (Blane Sheet es
pn sella (Bk 0 | me Check) via 0BYC (BSK/VIRX) Product Family
Pant Vation Area | E01 ventory vation eel pr mi | OE,
Purchasing Org. (KORG) | P01 Response for purchasing Lh Sita (688+ VBR) Lewy Prodct Gop
5 Se Fame cess
Purchasing Group (GRP) | 601 Purchaser team Seis Asset Under Constncton
Ld Pal 4 fled Fired Asset (ANL) Leveld ht.
Vendor (1FAT/LFBY) | 300000 Vendor master recon account SIs na io os (oven) rs
Matera (HARA MARC) 100001 Mate master puchaogbacantod) | F Outer Interna order (68B + VBR) y eg, 52000 - ram est
Se— Uo Unioo Used in special scenar .
Valuation Class (MBEW) = 3000 / 7920 Determines inventory G/L via OBYC - == Smee Valuation Class
Chart of Accounts. GBR Group Chart of Accounts. L Subcontracting. EKG) e + Determines inventory accounts (OBYC)
’ Linked to mater ype and hat of accoonts
Curency eR Tansacton and company curency No Consgmen Consignment tock (85) « Maitined at plan vl (M02)

5 Se Fame cess — Accounts. L Subcontracting. EKG) e + Determines inventory accounts (OBYC)
’ Linked to mater ype and hat of accoonts
Curency eR Tansacton and company curency No Consgmen Consignment tock (85) « Maitined at plan vl (M02)
ax Code Iu VAT Geman nice Senice entyshet MLBINARO) JR ———
IE iL ER ps 6 W) G S P&L Expense + Can be split by plant, material group, etc.
@ 0BYC - Automatic Account Determination (MM —> FI) @ 08YC Determination Logic (Step-by-Step)
Tarscioney| Meaning | RCRA pct oder vege © System reads movement ye eg.101, 102,122.
Po ery poring Fp 5 ‘Stockincrease at GR @ Reads transaction key from movement string (OMJJ).
(Balance Sheet) (movement 101, 105..) © Reads valuation class from material master (MBEW).
wp Olney TT ware C008 epee stig © Reads account moifer (eg, VAX) f required.
{Consteuption) (61, consumption, cost center) | @) Reads valuation grouping code from plant (OMWD).
PRD Price differences 5130000000 PRA/PRF Price variances (PO vs. Invoice] @@) Searches OBYC (T030) with Chart of Accounts + Val, Class + Tras. Key (+ Mod.)
SE a © memento | €) naiewsll cont sna ADO
Change in stock. © MM and Fl documents are created simultaneously.
svi Rm Et 4030000000 E Subcontracting stock change

5 Se Fame cess — 0) with Chart of Accounts + Val, Class + Tras. Key (+ Mod.)
SE a © memento | €) naiewsll cont sna ADO
Change in stock. © MM and Fl documents are created simultaneously.
svi Rm Et 4030000000 E Subcontracting stock change
8S Comigmenlobilty | 2110000000 E Ven aly fcr || gp Key Table: 15 Oement yp, 156Y(arsacton io)
Fos ee re = T030 (OBYC), TOOK (Valuation aea), TO30K (Mod. act. determination),
@ Tax Determination on Procurement (TAXD / MWS) © Pricing in Purchase Order (MM)
Del as prscedies ‘Example Tox Codes (Cybex) io ears ETD reno,
{osvz) [TaxCode | Description | Rate | Country a ot tric), | CoM Description Ca Type Typical Use
Define tx codes (FTP) Vi patvar 19% | Gemmany Rabat discount), roc (eight etc. PRO Netpice B | Bisepice PO)
eg Vi=19% - co i + Ping procedure (OMUM/ONGE) defines = =
Asia acooints (0840) 0 % (Epon) vo sequence K04 Cashdscount %or amount
Tax type MWST — MWS 0 macmmnty 0% EY + Conditions are not posted to FUNGI MRO. | 70g) | prce(gosy) | C Atemathepice
Maintain tax classification B | Bempt 0% | Geman
(customer/vendor/material) ™ = a 20% Turkey i FRAY | Freight 8 i
System calculates tax Ls bial IS Hesderdscomt B %oramount
‘during MIRO and posts to FI ‘Tax account determination uses 0BYZ/0B40 (MWS) - not VKOA.

5 Se Fame cess — | Geman
(customer/vendor/material) ™ = a 20% Turkey i FRAY | Freight 8 i
System calculates tax Ls bial IS Hesderdscomt B %oramount
‘during MIRO and posts to FI ‘Tax account determination uses 0BYZ/0B40 (MWS) - not VKOA.
@ Complete Accounting Entries — P2P Example (Cybex) QD) R000 and R004 - Automatic Postings
 5 Imi Recep FO) CTT) uo-wstsa 6 1o-optens
Receive 100 pes @ 10 EUR Invoice 1,000 EUR + 19% VAT Invoice higher by 50 EUR + 19% VAT Pay vendor 1,249.50 EUR
(Material 3000, V1 19%) | ‘» Maintains G/L account © Mormaiically posts
| | con Tou Toes como Ten Id =
Inventory (5%) 1,000 GRIRMWRY) | 1000 | - GRAR(WRK) | 1000 - Vendor (AF) 124950 - Grok lend « Puchase orders GRR voce)
GOR) - 0 | uta || POD © km ms Unecmuluielea ®) + brn ess
vom | io ||| eaten so | - + Tents mst chrgs fabs canbe
No taxat GR (fo stock materi) 4
Vendor) + 120050 + Sched as backround ob
@ «ey Configuration Steps (summary) @ Reporting & Reconciliation QE) Key Takeaways
@ Moai materia master andolatincloss (Cre apc dct 01 BAL FTP) | €@ FOLIN= Vendor open ems Do —————————
@ Maintain vendor maser (recon account) DL e——— 3 rested mer) ©) GRposts inventory and GRR; MIRO posts vendor and ax.
© Define purchasing or. oup (OWEL ONES) Fi Ridin], @ Discounts, feightand price vriaces ar handed via canon types.

5 Imi Recep FO) CTT) uo-wstsa 6 1o-optens — ndor maser (recon account) DL e——— 3 rested mer) ©) GRposts inventory and GRR; MIRO posts vendor and ax.
© Define purchasing or. oup (OWEL ONES) Fi Ridin], @ Discounts, feightand price vriaces ar handed via canon types.
Po ————) © Tx tema ss TD 0BYZI080)- ok KOA
Br ——— © #01 Fanci sstement (X00) er om a? ts hy Ek
(OM. TI5651) © Tete OTN MGO- MOI) @ Mtr gr CO for costars | @) ASL sme cst ives pestng loge ack expense
© nin irinont ppm arn) |S LESAN) Enns onsras sr
fetemination O Hoye pce vronces (RD) @ Eno endimecration ensues scare compliant franc eprtng
( ita.
A Important Useful SAP T-Codes [0] Same Da Processes:
GL sccounts, ta codes nd confi may vo by court, campy code snd ies reiremerts ME2IN, MIGO, MIRO, F110, OMWD, OMLJ, Connected for Capes
Avy fr fil SP acumen cont used SAP constant. OBYC, 08YZ, 0840, FIX, ROOD, R004 FELT OT Real ae £727

[Structured understanding of this image]
### 🖼️ WHAT THE IMAGE SAYS
- NA H rocess.
- Cybex - SAP IA MM-FI Integration (Procure-to-Pay) Ocyb ras
- From Purchase Requisition to Vendor Payment — Complete Guide J Cy! ex An eel
- Configuration « Determination Logic « Accounting Entries « Examples + Reporting etutiom fors Better Tomonron: Better BS
- @ End-to-End Procure-to-Pay (P2P) Process Flow @ Process Highlights

🖼️ WHAT THE IMAGE SAYS — plete Guide J Cy! ex An eel
- Configuration « Determination Logic « Accounting Entries « Examples + Reporting etutiom fors Better Tomonron: Better BS
- @ End-to-End Procure-to-Pay (P2P) Process Flow @ Process Highlights
- Purchase Purchase © Receipt Invoice Outgoing ti
- ON, OME @ win © Ji, © SEM Q bein | © wesw
- (MESTN) (ME21N) fly (MIRO) (FT107F-53) A ©»
- tomatic account determination
- BE Ww © BB Of dl erm
- =, = eal-time postings to ACDOCA
- oe € = [1] posting
- + intemal request + Legally binding * Receive goods * MotchPO+GR+Imvoice + Automaticormanval + Balance Sheet, PBL @ supports stock, services, assets
- for goods/services contract with vendor instock or seniceentty pot vendor ably payment (SEPA, wire) = Vendor open ems (FBLIN) Hoxaos ton dicot
- i Fl ting Ma Fl posting Rh + DIGRAR Input Tax PRO fany) + Dr Vendor (AP) « Material ledger & costs @ Hands ax, discounts, variances
- Shams «Cr Vendor (AP) « CrBank (House Bank) + Audit trail (ACDOCA) @ Works forlocal and group reporting
- [2] Key Master Data Elements (MM-FI) [3] Account Assignment Categories (ME21N) [5) Material Master - 5 Level Hierarchy
- Object / Field Example (box) Purpose Description Level ProdoctCategary
- **SAP objects detected:** ME21N, MIRO, ACDOCA, OBYC, OMJJ, OMWD, VKOA, MIGO, F110.

🖼️ WHAT THE IMAGE SAYS — nt Categories (ME21N) [5) Material Master - 5 Level Hierarchy
- Object / Field Example (box) Purpose Description Level ProdoctCategary
- **SAP objects detected:** ME21N, MIRO, ACDOCA, OBYC, OMJJ, OMWD, VKOA, MIGO, F110.
- **Amounts / rates detected:** 10 EUR, 1,000 EUR, 50 EUR, 1,249.50 EUR, £727, 19%, 0%, 20%.
### 🗣️ DIRECT ANSWER TO SPEAK NOW
- **Core Concept:** End-to-end P2P at CYBEX (company code DE01): ME51N purchase requisition (no FI posting), ME21N purchase order (no FI posting), MIGO goods receipt posts Dr Inventory (BSX) / Cr GR/IR (WRX), MIRO invoice verification posts Dr GR/IR and Dr Input tax (MWS) / Cr Vendor, F110 or F-53 pays Dr Vendor / Cr Bank (house bank), and F.01 / FBL1N / ACDOCA report it. Which G/L account is hit is never typed by hand: OBYC automatic account determination reads the movement type, the transaction key, the valuation class from the material master and the account modifier.
- **Key System Benefit:** MM and FI create one document in ACDOCA at goods receipt, so stock value, GR/IR clearing and vendor liability stay reconcilable in real time for both local (HGB) and group (IFRS) reporting.

🗣️ DIRECT ANSWER TO SPEAK NOW — er.
- **Key System Benefit:** MM and FI create one document in ACDOCA at goods receipt, so stock value, GR/IR clearing and vendor liability stay reconcilable in real time for both local (HGB) and group (IFRS) reporting.
- **Execution Strategy:** Configuration order: material master valuation class (MM02), vendor master reconciliation account (XK01), purchasing org/group (OME1/OME4), movement types (OMJJ), OBYC matrix (T030), tax procedure and codes (OBYZ/OB40/FTXP), PO pricing (OMUM), account assignment (OKB9/OKB8), then the test chain ME21N to MIGO to MIRO to F110, and RD00/RD04 automatic postings with reconciliation in FBL1N, MB5S and F.01.
- **Scenario Figures I Will Use:** 10 EUR, 1,000 EUR, 50 EUR, 1,249.50 EUR, £727, 19%, 0%, 20%. I keep the same figures through the posting, clearing and test steps; if a rate or account is not given, I state it as an explicit assumption rather than inventing a project value.
- **Objects Detected In The Question/Image:** ME21N, MIRO, ACDOCA, OBYC, OMJJ, OMWD, VKOA, MIGO, F110.

### 📊 ARCHITECTURAL FLOW
```text
1. REQUISITION ME51N
 internal request for goods/services; no FI posting
 ↓
2. PURCHASE ORDER ME21N
 legally binding contract with vendor; no FI posting
 ↓
3. GOODS RECEIPT MIGO

🗣️ DIRECT ANSWER TO SPEAK NOW — F110.

### 📊 ARCHITECTURAL FLOW
```text
1. REQUISITION ME51N
 internal request for goods/services; no FI posting
 ↓
2. PURCHASE ORDER ME21N
 legally binding contract with vendor; no FI posting
 ↓
3. GOODS RECEIPT MIGO
 receive into stock; Dr Inventory (BSX) / Cr GR/IR (WRX)
 ↓
4. INVOICE VERIFICATION MIRO
 match PO + GR + invoice; Dr GR/IR, Dr Input tax (MWS) / Cr Vendor (AP)
 ↓
5. OUTGOING PAYMENT F110 / F-53
 automatic SEPA or manual payment; Dr Vendor (AP) / Cr Bank (house bank)
 ↓
6. REPORTING F.01
 balance sheet and P&L, vendor open items FBL1N, material ledger and audit trail ACDOCA
```

### ⚙️ CONFIG STEPS
1. **OMJJ** — movement types drive the posting rules: the system reads the movement type (for example 101, 102, 122) and its transaction key from the movement string (T156/T156SY) · Example: Goods receipt 101 finds transaction key BSX/WRX before any account is chosen · Ref: CYBEX MM-FI P2P guide, OBYC determination logic steps 1-2.
2.

⚙️ CONFIG STEPS — and its transaction key from the movement string (T156/T156SY) · Example: Goods receipt 101 finds transaction key BSX/WRX before any account is chosen · Ref: CYBEX MM-FI P2P guide, OBYC determination logic steps 1-2.
2. **MM02** — the valuation class on the material master (MBEW) is what OBYC keys on; maintained at plant level (MM02, Accounting view) · Example: Valuation class 3000 / 7920 on material 10001 decides the inventory and expense accounts; different classes for raw material, finished goods and trading goods · Ref: MM-FI guide, Material Master 5-level hierarchy; MM02 (Accounting view).
3. **OBYC** — automatic account determination (T030): searches chart of accounts + valuation grouping (OMWD, T001K) + transaction key + account modifier and returns the G/L account into ACDOCA · Example: BSX inventory 1213000000; GBB offsetting consumption 5000000000 (modifiers VAX/VAY/VBR); PRD price differences 5190000000 (PRA/PRF); WRX GR/IR clearing 3215000000; BSV change in stock subcontracting 4030000000; KBS consignment liability 2110000000; MWS input tax 1540000000 · Ref: MM-FI guide, OBYC tables section 4 and 6.
4.

⚙️ CONFIG STEPS — ences 5190000000 (PRA/PRF); WRX GR/IR clearing 3215000000; BSV change in stock subcontracting 4030000000; KBS consignment liability 2110000000; MWS input tax 1540000000 · Ref: MM-FI guide, OBYC tables section 4 and 6.
4. **OBYZ** — tax determination on procurement: define the tax procedure (TAXD), tax codes (FTXP, for example V1 = 19% input VAT Germany) and assign accounts in OB40 (tax type MWST to MWS) · Example: V0 0% export (EU), Z0 intra-community (EU), E0 exempt, TR1 20% Turkey; the system calculates tax during MIRO and posts to FI. Tax determination uses OBYZ/OB40 (MWST), not VKOA · Ref: MM-FI guide, Tax Determination on Procurement (TAXD / MWS).
5. **OMUM** — PO pricing: info records (ME11) store vendor, material and pricing conditions; condition types PB00 net price, K004 cash discount, ZPRO price gross, FRA1 freight, ZDIS header discount; conditions are not posted to FI until MIRO · Example: A freight condition FRA1 only becomes an accounting line at invoice verification, never at PO creation · Ref: MM-FI guide, Pricing in Purchase Order (MM).
6.

⚙️ CONFIG STEPS — iscount; conditions are not posted to FI until MIRO · Example: A freight condition FRA1 only becomes an accounting line at invoice verification, never at PO creation · Ref: MM-FI guide, Pricing in Purchase Order (MM).
6. **ME21N** — account assignment category on the PO item decides the posting logic: blank = standard stock via OBYC (BSX/WRX); K = cost center (P&L expense + cost center, GBB + VBR); A = fixed asset / asset under construction (ANL); P = WBS element (project cost GBB + VBR); F = internal order; U = unknown; L = subcontracting components (BSV, KBS); S = service entry sheet (ML81N/MIRO), P&L expense · Example: The same EUR 1,000 purchase posts to inventory, a cost center or an asset purely from this one field · Ref: MM-FI guide, Account Assignment Categories (ME21N).
7. **MIGO** — post the goods receipt; MM and FI documents are created simultaneously and land in ACDOCA · Example: 100 pieces at 10 EUR (material 3000): Dr Inventory (BSX) 1,000 / Cr GR/IR (WRX) 1,000; no tax at goods receipt for stock materials · Ref: MM-FI guide, Complete Accounting Entries - P2P Example A.
8.

⚙️ CONFIG STEPS — in ACDOCA · Example: 100 pieces at 10 EUR (material 3000): Dr Inventory (BSX) 1,000 / Cr GR/IR (WRX) 1,000; no tax at goods receipt for stock materials · Ref: MM-FI guide, Complete Accounting Entries - P2P Example A.
8. **MIRO** — post the vendor invoice against the PO; price variances are handled via condition types and PRD · Example: Invoice 1,000 EUR + 19% VAT: Dr GR/IR (WRX) 1,000, Dr Input tax (MWS) 190 / Cr Vendor (AP) 1,190. Invoice higher by 50 EUR: Dr GR/IR 1,000, Dr Price difference (PRD) 50, Dr Input tax 199.50 / Cr Vendor (AP) 1,249.50 · Ref: MM-FI guide, examples B and C.
9. **F110** — automatic payment run (or F-53 manual) settles the vendor open item through the house bank · Example: Pay vendor 1,249.50: Dr Vendor (AP) 1,249.50 / Cr Bank (House Bank) 1,249.50; SEPA XML is generated from the payment run (DMEE) · Ref: MM-FI guide, example D, Outgoing Payment (F110).
10.

⚙️ CONFIG STEPS — hrough the house bank · Example: Pay vendor 1,249.50: Dr Vendor (AP) 1,249.50 / Cr Bank (House Bank) 1,249.50; SEPA XML is generated from the payment run (DMEE) · Ref: MM-FI guide, example D, Outgoing Payment (F110).
10. **RD00** — automatic postings for master data: maintains G/L account determination data, replicates to all company codes, updates control tables (for example T030), runs after master data changes; RD04 posts open items automatically (sales orders billing due list, purchase orders GR/IR invoice, intercompany postings); proposals can be reviewed before posting · Example: After a valuation-class change, RD00/RD04 keep the determination consistent instead of hand-fixing documents · Ref: MM-FI guide, RD00 and RD04 - Automatic Postings.

### 🔧 DROP THESE OBJECT NAMES
- **OBYC** — automatic account determination matrix (T030).
- **BSX** — inventory posting (balance sheet).
- **WRX** — GR/IR clearing.
- **PRD** — price differences (PRA/PRF).
- **GBB** — offsetting entry, consumption (VAX/VAY/VBR).
- **KBS** — consignment liability.
- **T030** — OBYC account determination table.
- **T001K** — valuation area table behind OMWD grouping.
- **MB5S** — GR/IR balance list for period-end proof.
- **FBL1N** — vendor open and cleared items.

### 🧾 ACCOUNTING ENTRIES

🔧 DROP THESE OBJECT NAMES — — OBYC account determination table.
- **T001K** — valuation area table behind OMWD grouping.
- **MB5S** — GR/IR balance list for period-end proof.
- **FBL1N** — vendor open and cleared items.

### 🧾 ACCOUNTING ENTRIES
- Goods receipt (MIGO 101), 100 pcs at 10 EUR, material 3000: Dr Inventory (BSX) EUR 1,000 / Cr GR/IR (WRX) EUR 1,000. No tax at goods receipt for stock materials.
- Invoice verification (MIRO), invoice 1,000 EUR + 19% VAT: Dr GR/IR (WRX) 1,000, Dr Input tax (MWS) 190 / Cr Vendor (AP) 1,190.
- Price variance (PO 1,000, invoice 1,050): Dr GR/IR (WRX) 1,000, Dr Price difference (PRD) 50, Dr Input ta