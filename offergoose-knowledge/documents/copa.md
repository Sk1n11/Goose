# Copa

Topic: Cybex

Here is the complete, line-by-line text transcribed directly from both image documents:
Account-based vs Costing-based CO-PA: one example
Cybex · controlling area / operating concern GB01 · combined CO-PA
Same billing, read in KE24 in both views
The example (1 stroller, third-party B2B)
Company code DE02 · billing type F2 · account assignment group T1. Prices are the real chain from your discount-analysis emails; COGS and VAT are ILLUSTRATIVE.
| Cond. | Meaning | EUR | G/L (VKOA) |
|---|---|---|---|
| Z001 | List price | 346.40 | 4111000000 Goods Sales 3rd Party |
| Z312 | Promo discount 5% | -17.32 | 4411000000 Discounts |
| Z205 | General discount 10% | -32.91 | 4411000000 Discounts |
| | Net sales | 296.17 | Customer account |
| MWST | VAT 19% ILLUSTR. | 56.27 | Output VAT (balance sheet) |
| VPRS | Cost of goods ILLUSTR. | 150.00 | COGS 5111000000 at PGI |
Step by step: what is posted and what each view shows
 * Step 1 - Sales order (VA01)
 * FI posting: None. Pricing calculated; profitability segment derived (KEDR).
 * Account-based shows: Nothing (no P&L impact)
 * Costing-based shows: A statistical line (segment is filled)
 * Step 2 - Goods issue (VL01N)
 * FI posting: Dr COGS 5111000000 150.00 / Cr Inventory 150.00
 * Account-based shows: COGS line 150.00

hing (no P&L impact)
 * Costing-based shows: A statistical line (segment is filled)
 * Step 2 - Goods issue (VL01N)
 * FI posting: Dr COGS 5111000000 150.00 / Cr Inventory 150.00
 * Account-based shows: COGS line 150.00
 * Costing-based shows: No separate line; cost arrives in the billing record via VPRS
 * Step 3 - Billing F2 (VF01)
 * FI posting: Dr Customer 352.44 · Dr Discounts 17.32 + 32.91 / Cr Sales 346.40 · Cr VAT 56.27 (Debits 402.67 = credits 402.67)
 * Account-based shows: 3 P&L lines: sales, two discount lines. No customer, no VAT.
 * Costing-based shows: One record with value fields (list price, discounts, net sales, COGS, margin)
> VF03 – Accounting overview shows 3 documents: accounting, controlling and profitability analysis document. If PGI is missing before billing, COGS is missing in CO-PA.
> 
Account-based (Margin analysis) in KE24
Meaning: the P&L lines of the accounting documents, tagged with characteristics. Stored in ACDOCA. The G/L account is the value, so it always reconciles to FI.
| Ref. document | Co. | G/L account (cost element) | Amount |
|---|---|---|---|
| PGI material doc | DE02 | 5111000000 Cost of sales | 150.00 |
| F2 billing | DE02 | 4111000000 Goods sales 3rd party | -346.40 |
| F2 billing | DE02 | 4411000000 Discounts (Z312) | 17.32 |

| Amount |
|---|---|---|---|
| PGI material doc | DE02 | 5111000000 Cost of sales | 150.00 |
| F2 billing | DE02 | 4111000000 Goods sales 3rd party | -346.40 |
| F2 billing | DE02 | 4411000000 Discounts (Z312) | 17.32 |
| F2 billing | DE02 | 4411000000 Discounts (Z205) | 32.91 |
| Net P&L (credit = margin) | | | -146.17 |
 * Credits are negative, as in ACDOCA. Currency: transaction currency only. Also shown: profit center, functional area, controlling document no. VERIFY discount lines may be aggregated in your layout.
Costing-based in KE24
Meaning: a separate profitability record: characteristics plus value fields. Stored in CE1 to CE4 of GB01. No G/L accounts are shown; value fields come from SD conditions mapped in KE4I.
| Record | Qty | Std price list | Promo | General | Net sales | COGS | Margin |
|---|---|---|---|---|---|---|---|
| Sales order (statistical) | 1 | order values | | expected | - | - | - |
| Billing F2 (record type F) | 1 | 346.40 | -17.32 | -32.91 | 296.17 | 150.00 | 146.17 |
 * Same line carries the characteristics (company code, sales org, plant, customer, product, IC sales type...). Currencies: local (type 10), group (type 30) or transaction. VERIFY exact value-field names in KE46.
The difference in one table
| Feature | Account-based | Costing-based |

, plant, customer, product, IC sales type...). Currencies: local (type 10), group (type 30) or transaction. VERIFY exact value-field names in KE46.
The difference in one table
| Feature | Account-based | Costing-based |
|---|---|---|
| Sales order visible? | No | Yes |
| G/L accounts visible? | Yes | No |
| Money shown as | G/L amounts (revenue, discounts, COGS) | Value fields (list price, discounts, net sales, COGS) |
| Reconciles to G/L | Always | Only if mapped (can differ by design) |
| Future | SAP direction (in ACDOCA) | Being phased out |
How to see it yourself
 * VF03 on the billing doc \rightarrow Accounting overview \rightarrow open the profitability analysis document.
 * KEBD (or the KE24 radio button): choose Margin analysis \rightarrow KE24 \rightarrow area GB01 \rightarrow select by sales order.
 * KEBD \rightarrow Costing-based \rightarrow KE24 \rightarrow same sales order, currency type 10.
 * Compare account-based revenue with FAGLL03H (same company code, period, ledger 0L).
 * KEKE status 4 only confirms both types are active; it is not the switch.
Say it in 20 seconds
> "Both types are active in GB01. Account-based shows the P&L lines of the accounting documents, so it always ties to the G/L.

KEKE status 4 only confirms both types are active; it is not the switch.
Say it in 20 seconds
> "Both types are active in GB01. Account-based shows the P&L lines of the accounting documents, so it always ties to the G/L. Costing-based shows a profitability record with value fields such as list price, discounts and COGS. The same billing creates both, so KE24 can show either."
> 
Source: your 17 Sep 2026 COPA session with Bonpathi and the pricing-procedure emails (Dec 2025).