# Advanced_Foreign_Currency_Valuation_FINS_FXV_Guide.pdf

Topic: S/4hana

FX
PRACTICAL CLOSE GUIDE · FINANCE
Advanced Foreign
Currency Valuation
FINS_FXV | SAP S/4HANA 2022 On-Premise
USD 1,000 × INR 80 → INR 85
Closing delta: INR 5,000 · Dr FX loss / Cr AP reconciliation
Video-based walkthrough + SAP Help research + original diagrams + timestamped source frames
Source video
What is Advanced Foreign Currency Valuation (FINS_FXV) in S/4HANA 2022
Simple SAP S/4 HANA FICO · published 4 Sep 2024 · 31:41
Scope and version note
The operational walkthrough is anchored to the user-provided S/4HANA 2022 On-Premise video. To add current
context, the guide cross-checks SAP Help pages that displayed S/4HANA On-Premise 2025 FPS02 on 14 Oct
2026. Configuration labels, delivered rules, currencies and account fields can differ by FPS/release; verify in
your own system and applicable SAP Notes before transport or production posting.
What is inside · Plain-language explanation · Posting examples · Delta logic diagram · Classic-versus-advanced
comparison · Setup checklist · FINS_FXV runbook · Troubleshooting · 22 genuine timestamped video screenshots
Prepared 14 October 2026
At a glance
Advanced Foreign Currency Valuation (FINS_FXV) remeasures eligible foreign-currency
open items and foreign-currency balance-sheet balances at a reporting-date rate. It

PRACTICAL CLOSE GUIDE · FINANCE — eo screenshots
Prepared 14 October 2026
At a glance
Advanced Foreign Currency Valuation (FINS_FXV) remeasures eligible foreign-currency
open items and foreign-currency balance-sheet balances at a reporting-date rate. It
calculates the movement needed to bring the ledger to the required carrying value,
posts that movement as an unrealized FX gain or loss, and—unlike classic
valuation—uses delta posting without a routine next-period reversal. [1,4,7]
Question Short answer
Why run it? To report monetary foreign-currency exposures at the applicable closing rate before financial
statements are prepared.
What is the transaction? FINS_FXV (On-Premise) or the “Advanced Foreign Currency Valuation” job template in Schedule
General Ledger Jobs.
What changes? The functional/local and other configured currency values of eligible balance-sheet exposure. The
document-currency quantity itself normally remains unchanged.
Where does the B/S side
post?
To the account being valued (including the relevant reconciliation account), not a separate classic
balance-sheet adjustment account.
How does the next close
work?
Delta-only: compare the current target with the carrying value already on the books; do not
assume an automatic reversal.

PRACTICAL CLOSE GUIDE · FINANCE — account), not a separate classic
balance-sheet adjustment account.
How does the next close
work?
Delta-only: compare the current target with the carrying value already on the books; do not
assume an automatic reversal.
What must be set up? Financial statement version (FSV), FX semantic tag/account scope, Advanced Valuation
activation, valuation rule/method, account determination, principle assignment, currency settings
and rates.
Most important implementation warning
Advanced valuation activation changes which closing processes are available for the affected scope. Plan a
ledger/company-code/accounting-principle cutover, test the opening/history treatment, and do not post in
production until the accounting policy, eligible account scope and resulting journal entries are signed off. SAP
states that classic valuation and related applications/jobs must not be used for the activated scope;
reversibility depends on whether production postings already exist. [1,8]
Video chapter map
Video time Topic Expanded in this guide
00:00 Introduction and roadmap Scope and purpose
01:13 Need for valuation Why remeasure at close
04:31 Realized vs unrealized gain/loss Accounting concepts and entries
05:46 Advanced valuation features What is new in FINS_FXV

Introduction and roadmap Scope and purpose
01:13 Need for valuation Why remeasure at close
04:31 Realized vs unrealized gain/loss Accounting concepts and entries
05:46 Advanced valuation features What is new in FINS_FXV
06:56 Key differences and logic Classic vs advanced
09:56 Comparison of valuation methods Rule/method reference
12:08 Simplified user interface Run parameters
13:33 Effect on existing data Cutover caution
15:16 Configuration steps Setup checklist and dependency diagram
17:56 System demonstration Worked example and screenshots
Contents
At a glance 2
1. Why foreign-currency valuation is needed 4
2. Core concepts and vocabulary 5
3. Calculation mechanics and debit/credit logic 5
4. Worked example from the video: USD supplier invoice 6
5. Delta posting: how the next close works 7
6. Unrealized valuation versus realized settlement FX 8
7. Classic FAGL_FCV versus Advanced FINS_FXV 9
8. Rules and valuation methods 9
9. Configuration checklist and dependencies 10
10. End-user runbook: test, update, review 11
11. Edge cases, grouping and clearing corrections 12
12. Troubleshooting quick reference 13
13. Activation, cutover and period-close checklist 13
14. Short glossary 14
15. Sources, verification and usage notes 14
Appendix A.

Edge cases, grouping and clearing corrections 12
12. Troubleshooting quick reference 13
13. Activation, cutover and period-close checklist 13
14. Short glossary 14
15. Sources, verification and usage notes 14
Appendix A. Genuine video screenshots with timestamps 16
Reading path
For a quick operational overview, read sections 1, 3, 7, 9 and 13. For configuration or implementation, use the
complete guide and validate all choices against your S/4HANA release and accounting policy.
1. Why foreign-currency valuation is needed
A transaction posted in a foreign currency is initially translated into the company’s functional or
company-code currency using the rate applicable when it is recognized. If the item is still open at month-,
quarteror year-end, the settlement-date or reporting-date rate may be different. Financial statements
may therefore require the monetary asset or liability to be remeasured at the closing rate. The difference
is an FX gain or loss. [1,4,7]
Typical scope includes open customer and supplier items, foreign-currency open items on G/L accounts,
and balances on foreign-currency-managed balance-sheet G/L accounts that are not open-item managed.
The rule, FSV semantic tag and account eligibility determine what the job actually selects. Do not tag

on G/L accounts,
and balances on foreign-currency-managed balance-sheet G/L accounts that are not open-item managed.
The rule, FSV semantic tag and account eligibility determine what the job actually selects. Do not tag
non-monetary balances such as historical-cost fixed assets for valuation. [1,2,7]
Advanced FXV in one diagram
Exposure
Open item or
foreign-currency
G/L balance
Key-date inputs
Rate type, quote,
functional currency,
ledger currencies
Valuation logic
FX semantic tag,
rule / method,
accounting principle
Target value
Amount at the
reporting-date
exchange rate
Delta-only posting
Target carrying value minus original
amount and prior valuation postings
Balance sheet
Post to the account being valued,
for example, the AP/AR control G/L
Profit and loss
Unrealized FX gain or loss; exact
account follows configured rule
Conceptual process — exact scope and postings depend on release, rules and ledger currency settings
Standards note
The broader Advanced Valuation suite covers several period-end topics. For foreign-currency remeasurement
itself, SAP Learning lists standards including IAS 21 (and IAS 29 / IFRIC 22) and US-GAAP guidance. Which items
qualify, how gains/losses are recognized, and any exceptions are matters of your approved accounting

rement
itself, SAP Learning lists standards including IAS 21 (and IAS 29 / IFRIC 22) and US-GAAP guidance. Which items
qualify, how gains/losses are recognized, and any exceptions are matters of your approved accounting
policy—not a setting to infer from the application name. [4,7]
The practical question
“What should this open USD exposure be worth in the reporting currency on the key date, and how much
of that movement has not yet been reflected in the ledger?” Advanced FCV answers that question under
the configured accounting principle, valuation rule, currency settings and account scope.
2. Core concepts and vocabulary
Term Meaning in this guide
Document / transaction currency The currency in which the source invoice, payment or other journal-entry line is denominated (for
example, USD).
Company-code / local currency The primary local currency of the company code (for example, INR or EUR).
Functional currency The currency of the primary economic environment, where configured for the
company-code/ledger combination. Advanced FCV values in functional currency; if none is set,
SAP uses company-code currency. Other configured currency types are also
remeasured/translated according to currency settings. [1,4,7]

code/ledger combination. Advanced FCV values in functional currency; if none is set,
SAP uses company-code currency. Other configured currency types are also
remeasured/translated according to currency settings. [1,4,7]
Valuation key date The reporting date whose exchange rates and balances are used in the valuation. A run may use
a fixed date or a supported dynamic date.
Open item A receivable, payable or G/L line that remains open at the key date and is within the configured
valuation scope.
Non-open-item balance A foreign-currency balance on an eligible balance-sheet G/L account not managed on an
open-item basis.
Unrealized FX gain/loss A reporting-date remeasurement of an exposure that has not yet settled. It is not a cash
payment.
Realized FX gain/loss The exchange-rate effect recognized when the exposure is settled/cleared. Clearing account
determination is distinct from period-end remeasurement configuration. [5]
Delta posting The current run posts only the difference needed to reach the required valuation after considering
original and prior valuation postings; prior valuation is not routinely reversed. [1,4,7]
Semantic tag FX A semantic identifier assigned to accounts or FSV nodes that tells the FCV rule which G/L
accounts are in scope.

g
original and prior valuation postings; prior valuation is not routinely reversed. [1,4,7]
Semantic tag FX A semantic identifier assigned to accounts or FSV nodes that tells the FCV rule which G/L
accounts are in scope. The FSV must be assigned to the relevant accounting principle. [2,4]
Accounting principle / ledger The accounting framework and ledger scope that control which rules, valuation methods and
accounting data apply. Advanced FCV uses the accounting-principle model rather than classic
valuation areas. [2,7]
Currency-type check
The number in the document currency usually does not change when the item is revalued. The effect is in the
target currency amounts. In SAP, confirm the functional currency and the source-currency relationships for
parallel currencies. If “Only manage balances in local currency” is set on a G/L master, local-currency behavior
can differ; SAP Help notes that other currency conversion postings may still occur. [1,4,7]
3. Calculation mechanics and debit/credit logic
For a single eligible exposure under a simple “always valuate” rule and direct quotation, a useful learning
formula is:
Simplified formula
Key-date value = foreign-currency exposure × key-date rate
Current delta = key-date value − carrying value already on the books

always valuate” rule and direct quotation, a useful learning
formula is:
Simplified formula
Key-date value = foreign-currency exposure × key-date rate
Current delta = key-date value − carrying value already on the books
The “carrying value already on the books” includes the initial local/functional-currency posting plus any prior
valuation adjustments. SAP’s configured rate quotation, currency ratios, method, grouping and
parallel-currency rules govern the production calculation. [1,4,7]
Sign depends on whether the exposure is an asset or a liability. In the video example, INR per USD rises
from 80 to 85: USD has become more expensive in INR, so the INR carrying amount of a USD payable
increases (loss), while the carrying amount of a USD receivable increases (gain).
Exposure Rate moves 80 → 85
INR/USD
Valuation
direction
Illustrative entry
Vendor payable (liability) Liability rises by INR 5,000 Loss Dr Unrealized FX loss; Cr AP reconciliation G/L
Customer receivable (asset) Asset rises by INR 5,000 Gain Dr AR reconciliation G/L; Cr Unrealized FX gain
Vendor payable (liability) Rate falls 80 → 75; liability falls Gain Dr AP reconciliation G/L; Cr Unrealized FX gain
Customer receivable (asset) Rate falls 80 → 75; asset falls Loss Dr Unrealized FX loss; Cr AR reconciliation G/L

INR/USD — yable (liability) Rate falls 80 → 75; liability falls Gain Dr AP reconciliation G/L; Cr Unrealized FX gain
Customer receivable (asset) Rate falls 80 → 75; asset falls Loss Dr Unrealized FX loss; Cr AR reconciliation G/L
Do not shortcut the sign check
First identify the exposure as an asset or liability, then establish the exchange-rate quote convention. “A higher
FX rate means a loss” is not universally true: it depends on the direction of the quote and the balance-sheet
nature of the item. Grouping rules can also net related items before choosing a gain/loss account. [7]
4. Worked example from the video: USD supplier
invoice
The source video’s training example uses a supplier open item of USD 1,000 in a company whose local
currency is INR. The invoice is posted at INR 80 per USD and remains open at the 31 August key date,
when the rate is INR 85 per USD. The example assumes the rule allows both gains and losses (for
example, the delivered SKDV key-date rule with ALWAYS_VALUATE), a valid rate on the key date and no
earlier valuation adjustment. [6,9]
Step Calculation Result
Initial posting USD 1,000 × INR 80/USD INR 80,000 payable
Key-date target USD 1,000 × INR 85/USD INR 85,000 payable
Required change INR 85,000 − INR 80,000 INR 5,000 increase in liability

INR/USD — . [6,9]
Step Calculation Result
Initial posting USD 1,000 × INR 80/USD INR 80,000 payable
Key-date target USD 1,000 × INR 85/USD INR 85,000 payable
Required change INR 85,000 − INR 80,000 INR 5,000 increase in liability
Valuation posting for the open vendor payable
Account (illustrative) Debit (INR) Credit (INR) Explanation
Unrealized foreign-exchange loss 5,000 — Recognizes the closing-date expense
Vendor AP reconciliation G/L — 5,000 Brings the liability to INR 85,000
What changes—and what does not
The vendor exposure remains USD 1,000. The ledger carrying amount of the payable becomes INR 85,000.
FINS_FXV posts to the valuated balance-sheet account (in this example, the AP reconciliation G/L) plus the
configured FX P&L account; it does not create a separate classic valuation adjustment account. The exact
journal-line dimensions and account assignment depend on your system configuration. [1,6,9]
Equivalent receivable example
If instead a customer owes USD 1,000, the initial AR value at INR 80 is INR 80,000. At INR 85, the
receivable is worth INR 85,000, an INR 5,000 gain. A simplified entry is Dr AR reconciliation G/L INR 5,000 /
Cr Unrealized FX gain INR 5,000. The same FX move increases both a USD asset and a USD liability in INR

INR/USD — , the
receivable is worth INR 85,000, an INR 5,000 gain. A simplified entry is Dr AR reconciliation G/L INR 5,000 /
Cr Unrealized FX gain INR 5,000. The same FX move increases both a USD asset and a USD liability in INR
terms; the P&L sign differs because one is an asset and the other a liability.
Reading the source demo table
One video slide labels a row “Payment,” while the narration treats the USD exposure as still open for
period-end valuation. For the INR 5,000 calculation, this guide follows the narrated open-item scenario. In a
production run, verify the item is actually open at the key date; a settled item is handled through
clearing/realized FX and any configured post-clearing correction. [5,6,9]
5. Delta posting: how the next close works
Advanced FCV uses delta logic only. If the required closing value changes from period to period, SAP
calculates the movement needed relative to the original balance and prior valuation adjustments; it does
not normally reverse last month’s valuation on day one of the new period. [1,4,7]
Initial posting
USD 1,000 × ₹80/USD
Carrying value: ₹80,000
AP credit: ₹80,000
First close
Target: ₹85,000
Delta: +₹5,000
Dr FX loss / Cr AP
Next close
Target: ₹86,000
Prior: ₹85,000
Delta only: +₹1,000

period. [1,4,7]
Initial posting
USD 1,000 × ₹80/USD
Carrying value: ₹80,000
AP credit: ₹80,000
First close
Target: ₹85,000
Delta: +₹5,000
Dr FX loss / Cr AP
Next close
Target: ₹86,000
Prior: ₹85,000
Delta only: +₹1,000
₹80,000 + ₹5,000 + ₹1,000 = ₹86,000 carrying value after the second close
Advanced FCV does not auto-reverse the prior close: each run posts only the movement required by its rule.
Date / run Key
rate
Required AP
value
Prior AP
value
This run’s
delta
Illustrative P&L / AP effect
Invoice date 80 80,000 — — Original liability posted at 80,000
31 Aug close 85 85,000 80,000 +5,000 Dr FX loss 5,000 / Cr AP 5,000
30 Sep close 86 86,000 85,000 +1,000 Dr FX loss 1,000 / Cr AP 1,000
Later close at
83
83 83,000 86,000 −3,000 Dr AP 3,000 / Cr FX gain or configured
P&L reversal
Useful reconciliation check
After the second close in the example, the AP carrying value should be INR 86,000: original INR 80,000 + INR
5,000 first delta + INR 1,000 second delta. If a rerun produces no new effect, the rate may be unchanged, the
item may be outside scope, or the valuation method may suppress the result. Never manually reverse a prior
FCV document just because a new period started. [1,4,7]
Grouping can change the account-level result.

83 83,000 86,000 −3,000 Dr AP 3,000 / Cr FX gain or configured — hanged, the
item may be outside scope, or the valuation method may suppress the result. Never manually reverse a prior
FCV document just because a new period started. [1,4,7]
Grouping can change the account-level result. SAP describes grouping of related items; an individual item’s line
difference may have the opposite sign to its group’s net difference. Therefore the configured gain/loss account can follow
the net group balance, not just a single row in isolation. Check the “group ID” and valuation line type in the result list. [7]
6. Unrealized valuation versus realized settlement
FX
Stage What happened? Accounting meaning
Invoice posting Recognize a foreign-currency receivable, payable or
balance at the transaction-date rate.
Initial book value.
Period-end FCV Item remains open; use the closing rate to
remeasure.
Unrealized valuation gain/loss. Advanced FCV
posts a delta.
Payment / receipt /
clearing
The open item is settled at the settlement-date rate. Realized FX difference is determined through
clearing/payment account determination.
Post-clearing FCV
follow-up
Previously posted unrealized valuation may need
correction after the open item is cleared.
The subsequent Advanced FCV run corrects the
residual adjustment according to the configured

83 83,000 86,000 −3,000 Dr AP 3,000 / Cr FX gain or configured — nation.
Post-clearing FCV
follow-up
Previously posted unrealized valuation may need
correction after the open item is cleared.
The subsequent Advanced FCV run corrects the
residual adjustment according to the configured
realized/reset accounts; do not reverse by hand.
[5]
Standalone realized-loss example (no prior period-end FCV)
Suppose the USD 1,000 supplier invoice was initially recorded at INR 80/USD (INR 80,000) and then paid at
INR 86/USD (INR 86,000), with no earlier period-end valuation. A simplified clearing entry is:
Account Debit (INR) Credit (INR)
AP reconciliation / supplier liability 80,000 —
Realized FX loss 6,000 —
Bank — 86,000
Prior valuation changes the settlement split
If a period-end valuation was posted before settlement, the payable control balance and unrealized P&L have
already moved. The settlement posting and the next FCV correction are then split according to the clearing and
Advanced FCV account-determination configuration. The simplified INR 6,000 example above is specifically for
the no-prior-valuation case. [5]
7. Classic FAGL_FCV versus Advanced FINS_FXV
Dimension Classic foreign currency valuation Advanced foreign currency valuation
On-Prem transaction Usually FAGL_FCV (New G/L); older ECC programs
vary.

-valuation case. [5]
7. Classic FAGL_FCV versus Advanced FINS_FXV
Dimension Classic foreign currency valuation Advanced foreign currency valuation
On-Prem transaction Usually FAGL_FCV (New G/L); older ECC programs
vary.
FINS_FXV, or “Advanced Foreign Currency Valuation”
job template.
Accounting scope Valuation areas and valuation methods are key
selection/configuration concepts.
Accounting-principle-based rules;
ledger/company-code/key date are central run
parameters.
Posting logic Classic can use reversal logic (commonly default)
or, where configured, delta logic.
Delta-only; prior valuation is considered. No standard
choice to reverse each period.
Balance-sheet offset Open-item valuation commonly uses a
balance-sheet adjustment account.
Posts to the account being valued (for example, the
AP/AR reconciliation G/L); no additional valuation
adjustment account is needed.
P&L setup Gain/loss accounts plus classic
adjustment-account settings may be needed.
P&L FX accounts are configured in valuation
rules/account determination; realized/reset account
fields vary by release.
Scope selection Classic selection screen has separate open-item
and G/L/balance parameters and more processing
flags.
FSV plus semantic tags define account scope; the run
UI is leaner.
Ledger/currency
handling

release.
Scope selection Classic selection screen has separate open-item
and G/L/balance parameters and more processing
flags.
FSV plus semantic tags define account scope; the run
UI is leaner.
Ledger/currency
handling
Valuation area/ledger-group approach depends on
classic setup.
Run is ledger-specific; uses functional currency when
defined and supports other configured currency types.
Cutover impact Classic reports/jobs remain usable only where
Advanced Valuation is not active for the scope.
After activation, do not use displaced classic
valuation/related reports for the same activated
scope; plan carefully.
Decision gate
This is not just a new transaction code. It changes account scope, posting destinations, period logic and the
close process. Compare both models, validate unsupported account categories and migration/opening
balances, and test clearing behavior before activating Advanced Valuation in production. [1,7,8]
8. Rules and valuation methods
A valuation rule describes which items are selected and how they are valuated; its steps can specify the
business transaction type, exchange-rate type, semantic tag and valuation method. The method
determines when a gain or loss is recognized. SAP Help documents the following standard valuation

d; its steps can specify the
business transaction type, exchange-rate type, semantic tag and valuation method. The method
determines when a gain or loss is recognized. SAP Help documents the following standard valuation
approaches; availability and delivered defaults should be checked in the installed release. [3,4]
Method / rule Plain-language behavior Use / caution
LOWEST_VALUE Post only when the valuation result meets the
configured loss condition relative to the initial amount.
A conservative/local-GAAP style approach;
account polarity and grouping matter.
STRICT_LOWEST_VALUE Post only when the new valuation establishes a worse
low value than the prior lowest valuation.
A worsening loss can be posted; recovery from
the lowest point is generally not posted as a
gain under this method.
ALWAYS_VALUATE Reflect the current key-date value whether it produces
a gain or loss.
SAP Learning states SKDV (Key Date FCV) is
delivered with ALWAYS_VALUATE by default.
GAIN_ONLY Post gains only; suppress losses. Use only where the approved accounting rule
requires it.
DE_BILMOG_VALUATE Combines ALWAYS_VALUATE for current items / net
due date under one year with STRICT_LOWEST_VALUE
for non-current items.
STDV time-dependent rule; SAP docs describe
the German Accounting Modernization Act
logic.

_VALUATE Combines ALWAYS_VALUATE for current items / net
due date under one year with STRICT_LOWEST_VALUE
for non-current items.
STDV time-dependent rule; SAP docs describe
the German Accounting Modernization Act
logic.
Standard rules noted in SAP Learning
SKDV = Key Date Foreign Currency Valuation; the default method is ALWAYS_VALUATE. STDV =
Time-Dependent Foreign Currency Valuation; the delivered example combines ALWAYS_VALUATE and
STRICT_LOWEST_VALUE based on remaining term. Both standard rules use exchange-rate type M (average
rate) in the documented configuration, but the delivered rules and settings can be changed. [4]
Important: the words “loss” and “gain” must be interpreted with the item’s debit/credit nature and the relevant grouping
rule. For an AP liability, a higher functional-currency carrying value is normally a loss; for an AR asset, a higher carrying
value is normally a gain. A method can suppress gains/losses depending on its policy. Test with both debit and credit
exposures.
9. Configuration checklist and dependencies
SAP Help’s current On-Premise checklist identifies the FSV, FSV-to-accounting-principle assignment, FX
semantic tags, Advanced Valuation activation, account-determination rules, FCV valuation rules and rule

dependencies
SAP Help’s current On-Premise checklist identifies the FSV, FSV-to-accounting-principle assignment, FX
semantic tags, Advanced Valuation activation, account-determination rules, FCV valuation rules and rule
assignment to accounting principles as core prerequisites. [2]
1 · Define scope
FSV + monetary G/Ls
tagged with FX; assign
FSV to principle
2 · Prepare system
Maintain rates/currencies;
activate by principle,
ledger, company code, period
3 · Define valuation
Rule + step + method;
rate type, semantic tag,
P&L / account determination
4 · Assign rule
Assign FCV rule to the
accounting principle;
ledger-specific if needed
5 · Test and inspect
Run simulation; validate
eligible accounts, rates,
signs and messages
6 · Update and reconcile
Post once approved; review
job/application logs and
journal entry evidence
Sequence is a practical checklist; IMG labels and configuration screens differ by S/4HANA release.
# Configuration activity / check What to verify
1 Design the accounting scope Choose legal accounting principle, ledger, company code, currencies and eligible
monetary accounts. Decide the method before building.
2 Maintain exchange rates and ratios Maintain required key-date rates/rate types (for example, OB08 in classic on-premise

1 Design the accounting scope Choose legal accounting principle, le — dger, company code, currencies and eligible
monetary accounts. Decide the method before building.
2 Maintain exchange rates and ratios Maintain required key-date rates/rate types (for example, OB08 in classic on-premise
currency maintenance) and translation ratios/cross-rate setup where applicable.
Confirm direct/indirect quotation.
3 Define the financial statement version
(FSV)
Use the FSV appropriate to the chart of accounts and accounting principle. The
video/article references OB58 for classic FSV maintenance; app/configuration paths
vary by release.
4 Assign FSV to accounting principle Confirm the same FSV is used by the principle and that the relevant chart of
accounts is assigned.
5 Assign semantic tag FX to source scope Tag the monetary G/L accounts or account nodes to be valued. Include the intended
reconciliation accounts/open-item G/Ls; exclude non-monetary accounts. New
accounts within a tagged range may automatically enter scope.
6 Activate Advanced Valuation Activate for the accounting principle and maintain the starting ledger/company
code/fiscal-year/period point. Verify cutover implications before production.
7 Define account determination Map required P&L gain/loss accounts and any realized/reset accounts supported by
the installed release.

3 Define the financial statement version — company
code/fiscal-year/period point. Verify cutover implications before production.
7 Define account determination Map required P&L gain/loss accounts and any realized/reset accounts supported by
the installed release. Where applicable, keep clearing/payment realized FX
determination (for example, transaction key KDF) distinct from FCV’s
unrealized/reset accounts.
8 Define FCV rule and steps Set the scope/tag, business transaction, exchange-rate type, method, grouping and
account assignment settings according to local policy. Standard rules cited by SAP
Learning include SKDV and STDV.
# Configuration activity / check What to verify
9 Assign rule to accounting principle Assign the rule to the applicable principle; if needed, make it ledger-specific. Confirm
no conflicting rule assignment exists.
10 Test end-to-end in non-production Verify invoice and balance-sheet scenarios, both debit/credit directions, key-date
rates, document links, logs, clearing and parallel-currency amounts before transport.
Release-sensitive account fields
Older video demonstrations may show only unrealized gain/loss accounts, while later
documentation/configuration screens distinguish unrealized accounts from realized/reset accounts used after
clearing.

Configuration activity / check What to verify — ive account fields
Older video demonstrations may show only unrealized gain/loss accounts, while later
documentation/configuration screens distinguish unrealized accounts from realized/reset accounts used after
clearing. The exchange-rate difference accounts used by payment clearing are a separate configuration. Follow
the exact IMG/SSCUI documentation and SAP Notes for your installed S/4HANA release. [4,5]
10. End-user runbook: test, update, review
You can execute Advanced FCV directly in the back end with transaction FINS_FXV or schedule it in
Schedule General Ledger Jobs using the “Advanced Foreign Currency Valuation” template. In both routes,
specify the company code, ledger and valuation key date, then choose test or update processing. The job
template can be scheduled once or recurrently with fixed or dynamic date options where supported. [1]
Step Action Control point
1 · Prepare Finish postings/interfaces through the key date; confirm
the FX-rate file and accounting period.
Use the correct reporting date and rate convention.
Check missing currency pairs/translation ratios.
2 · Select run FINS_FXV or Schedule General Ledger Jobs → Advanced
Foreign Currency Valuation. Enter company code,
ledger and fixed/dynamic key date.

1 · Prepare Finish postings/interfaces through the key date; confirm — and rate convention.
Check missing currency pairs/translation ratios.
2 · Select run FINS_FXV or Schedule General Ledger Jobs → Advanced
Foreign Currency Valuation. Enter company code,
ledger and fixed/dynamic key date.
Confirm the accounting principle/rule resolved for that
ledger/company-code combination.
3 · Simulate Run a test/simulation first. Apply only supported filters
and technical optimization settings.
No production posting should be created by the test run;
review results and exceptions.
4 · Analyze Review eligible lines/balances, result list, valuation line
type, messages and run/application logs.
Investigate missing rates, excluded accounts,
unexpected signs or no-result statuses.
5 · Update After approval, execute update run or schedule the
productive job.
Avoid concurrent duplicate postings; retain the job/run
identifier and authorizations trail.
6 · Verify Open the generated journal entry, inspect currency
amounts and assigned dimensions, and reconcile
P&L/B/S movement.
Confirm original journal-entry link, posting period/date,
ledger, document type and totals.
What to review in the output
• Header / selection parameters: company code, ledger, key date, processing option and run status.

6 · Verify Open the generated journal entry, inspect currency — Confirm original journal-entry link, posting period/date,
ledger, document type and totals.
What to review in the output
• Header / selection parameters: company code, ledger, key date, processing option and run status.
• Result list: valuated items and G/L balances, proposed/posted amount, valuation line type and any original
journal-entry reference. The display currency can be changed among supported currency views.
• Run log and application log: completion status and item-level messages; use the messages to distinguish an
unchanged rate from an ineligible or erroneous item.
• Posted journal entry: confirm the B/S account being valued and the configured FX P&L account; verify
functional/local/group currency amounts and account assignments.
• Evidence retained: key-date rate source, test-run approval, update-run/job ID, application log, result output and
posted document reference.
Run log is not the accounting proof by itself
A successful job status means the job completed; it does not prove the accounting scope, valuation sign or
account assignment is correct. Tie the result list to the journal entry and reconcile the B/S/P&L movement. [1,4]
11. Edge cases, grouping and clearing corrections

6 · Verify Open the generated journal entry, inspect currency — does not prove the accounting scope, valuation sign or
account assignment is correct. Tie the result list to the journal entry and reconcile the B/S/P&L movement. [1,4]
11. Edge cases, grouping and clearing corrections
Advanced FCV is designed to retain traceability between a valuation journal entry and the original line
item and to show item-level processing status. SAP’s Advanced Valuation concept also supports grouping
rules. For example, items cleared by the same clearing document can be grouped, while not-cleared items
and non-open-item balances use different grouping keys. The group balance can control which gain/loss
account is used. [7]
Situation Why it matters Operational check
Invoice + credit/debit note Related items may be grouped and evaluated on
a net basis.
Inspect group ID and configured grouping rule; do
not expect every row to map 1:1 to a P&L line.
Cleared open items Existing valuation adjustments are not
necessarily removed at the instant of clearing.
Run the appropriate follow-up FCV process; the
subsequent run corrects the residual adjustment
based on the configured realized/reset accounts. [5]
Non-open-item G/L balance The system values eligible foreign-currency
balances rather than each document as an AR/AP
open item.

6 · Verify Open the generated journal entry, inspect currency — t run corrects the residual adjustment
based on the configured realized/reset accounts. [5]
Non-open-item G/L balance The system values eligible foreign-currency
balances rather than each document as an AR/AP
open item.
Check the account’s currency management and the
rule/semantic-tag scope.
Parallel currencies Valuation in functional currency and
remeasurement/translation of other currency
types depend on ledger settings.
Verify source currency relationships and compare
the result in functional, company-code and
group-currency views. [1,4,7]
Known restrictions to verify in your release
SAP-managed introductory material lists tax accounts and GR/IR-category accounts among known
restrictions for Advanced FCV, and notes that postings cannot be made to an additional adjustment
account. Because support can change across releases/FPS and account categories, confirm the current
On-Premise release documentation or an applicable SAP Note before including tax/GR/IR balances. [7]
Scope exclusions
Never tag non-monetary accounts (for example, fixed assets held at historical cost) as FCV source accounts.
The FX semantic tag is a scope selector, not just a reporting label. Correct a wrong FSV/FX scope in
configuration and in any posted valuation history under controlled change management.

cal cost) as FCV source accounts.
The FX semantic tag is a scope selector, not just a reporting label. Correct a wrong FSV/FX scope in
configuration and in any posted valuation history under controlled change management. [1,2]
12. Troubleshooting quick reference
Symptom Likely cause First checks
“No G/L accounts to valuate
found”
Wrong/missing semantic tag, FSV not
assigned to principle, or rule not
assigned/active for ledger and company
code.
Confirm FSV + FX tag on the intended account/node;
FSV-to-principle assignment; activation period; FCV
rule and step tag.
No valuation line or zero delta Unchanged rate, item not open at key date,
item outside account scope, or method
suppresses the gain/loss.
Check key date, exchange rate, status, method,
group ID and whether prior valuation already brought
the balance to target.
Missing/incorrect exchange rate Rate type, currency pair, valid-from date,
quote direction or translation ratio is wrong.
Check the rate table (for example, OB08), rate type
from the rule, ratio/cross-rate setup and date validity.
Unexpected debit/credit sign Asset/liability sign misunderstood, quote
convention reversed, or item/group net
differs.
Recompute the target amount, identify AR vs AP vs
G/L balance, inspect group net and compare result

Unexpected debit/credit sign Asset/liability sign misunderstood, quote
convention reversed, or item/group net
differs.
Recompute the target amount, identify AR vs AP vs
G/L balance, inspect group net and compare result
list to journal entry.
Unexpected P&L account Rule or account determination differs from
assumption; realized/reset and unrealized
fields may be separate.
Inspect the rule’s gain/loss account mapping and
clearing account determination (do not assume they
are one setting).
Cleared item still has valuation
effect
Open item was cleared after prior valuation;
the remaining unrealized adjustment is
corrected in the next run.
Review the post-clearing run and realized/reset
account settings; avoid manual reversal. [5]
Classic report unavailable /
rejected
Advanced Valuation is active for the
relevant scope.
Use FINS_FXV for that scope and check the activation
and cutover design. [1,8]
Differences in local vs group
currency
Currency-type source settings or “only local
currency” account flag affect update
currency.
Review ledger/company-code currency settings,
functional currency and account master indicators.
[1,4,7]
A disciplined diagnosis order
1) Key date and rate → 2) item/account eligibility and FX tag → 3) accounting principle/ledger/rule assignment

currency settings,
functional currency and account master indicators.
[1,4,7]
A disciplined diagnosis order
1) Key date and rate → 2) item/account eligibility and FX tag → 3) accounting principle/ledger/rule assignment
→ 4) valuation method and grouping → 5) account determination → 6) posted document and currency view. This
sequence avoids changing configuration before establishing the calculation inputs.
13. Activation, cutover and period-close checklist
The activation decision is consequential. SAP documentation warns that once Advanced Valuation is
active, classic foreign-currency valuation and certain related jobs/apps must not be used for the affected
scope. Deactivation may be possible before productive advanced-valuation postings exist; after postings,
reversal of the decision may no longer be available. Align with your release-specific activation screen and
migration plan. [1,8]
Use this checklist before the first production update run:
[ ] Confirm accounting policy, company-code functional currency, accounting principle, ledger and valuation method.
[ ] Define the production cutover date / activation fiscal year and period; document treatment of legacy classic valuation
balances.

, company-code functional currency, accounting principle, ledger and valuation method.
[ ] Define the production cutover date / activation fiscal year and period; document treatment of legacy classic valuation
balances.
[ ] Confirm the FSV is assigned to the right accounting principle and FX tags include only eligible monetary source
accounts.
[ ] Verify relevant exchange rates, rate type, quotation and translation ratios at the exact key date.
[ ] Test vendor payable, customer receivable, G/L open-item and foreign-currency balance-sheet scenarios, including
both favorable and unfavorable movements.
[ ] Test grouping, multiple currencies, clearing and post-clearing correction/reset behavior.
[ ] Validate P&L gain/loss and realized/reset account determination; verify dimension assignments and document
splitting/ledger behavior.
[ ] Review test output with accounting and SAP functional owners; retain sign-off and result evidence.
[ ] Run the update once approved; verify journal-entry totals, original-document link, posting period and B/S/P&L
reconciliation.
[ ] Keep the next period’s FCV delta process in the close calendar—do not schedule an automatic reversal of the FCV
document.
Run sequence in the broader Advanced Valuation close

sting period and B/S/P&L
reconciliation.
[ ] Keep the next period’s FCV delta process in the close calendar—do not schedule an automatic reversal of the FCV
document.
Run sequence in the broader Advanced Valuation close
SAP’s Advanced Valuation overview lists the related jobs as discounting long-term assets/liabilities, Advanced
Foreign Currency Valuation, credit-risk-based impairment and balance-sheet reclassification. Sequence and
dependencies should follow the product documentation and your organization’s close design. [7]
14. Short glossary
Term Definition
AP / AR control or reconciliation
account
General Ledger account that represents supplier/customer balances in the financial statements. In
Advanced FCV, valuation postings can be made directly to the valued account.
Company code Legal accounting entity in SAP Financial Accounting.
FINS_FXV On-Premise transaction/report for Advanced Foreign Currency Valuation.
FAGL_FCV Classic/New G/L Foreign Currency Valuation report; not the Advanced FCV transaction.
FSV Financial Statement Version; its account nodes/accounts define statement structure and, with
semantic tagging, can define advanced-valuation scope.
FX semantic tag SAP semantic tag used to mark source accounts relevant to FX valuation.

ent Version; its account nodes/accounts define statement structure and, with
semantic tagging, can define advanced-valuation scope.
FX semantic tag SAP semantic tag used to mark source accounts relevant to FX valuation.
Key-date rate Rate valid on the period-end or other reporting date used for remeasurement.
OB08 / OBBS Common classic on-premise transactions for maintaining exchange rates and translation ratios,
respectively; exact configuration options vary by release.
Schedule General Ledger Jobs Fiori app that provides the Advanced Foreign Currency Valuation job template and scheduling
options.
Valuation area Classic foreign-currency valuation concept; Advanced FCV uses accounting-principle-based rules
instead.
15. Sources, verification and usage notes
The guide combines the user-provided video, SAP product documentation/training and a SAP Community
walkthrough. Product behavior can change; the on-premise Help references below displayed version 2025
FPS02 when checked on 14 October 2026. For configuration or production use, search the exact
release/FPS and relevant SAP Notes.
[1] SAP Help Portal — Advanced Foreign Currency Valuation (S/4HANA On-Premise, 2025 FPS02). Use,
prerequisites, currency behavior, run steps, results and output.
Open source ↗

e exact
release/FPS and relevant SAP Notes.
[1] SAP Help Portal — Advanced Foreign Currency Valuation (S/4HANA On-Premise, 2025 FPS02). Use,
prerequisites, currency behavior, run steps, results and output.
Open source ↗
[2] SAP Help Portal — Customizing Requirements Checklist for Advanced Foreign Currency Valuation (2025
FPS02). FSV, semantic tags, activation, rules and assignments.
Open source ↗
[3] SAP Help Portal — Valuation Rules and Examples of Valuations (2025 FPS02). LOWEST_VALUE,
STRICT_LOWEST_VALUE, ALWAYS_VALUATE, GAIN_ONLY and DE_BILMOG_VALUATE.
Open source ↗
[4] SAP Learning — Configuring Advanced Foreign Currency Valuation. SKDV/STDV defaults, rate type M,
methods, semantic tags and account determination.
Open source ↗
[5] SAP Community (SAP-managed) — Behavior of Advanced Foreign Currency Valuation after Clearing (7
May 2024). Clearing correction and separate realized/unrealized account configuration.
Open source ↗
[6] SAP Community member article — Elevate your financials using Advanced Foreign Currency Valuation
(FINS_FXV) in S/4HANA 2022 OP (4 Sep 2024). Exact INR 80→85 example and demonstration.
Open source ↗
[7] SAP Community (SAP-managed) — Introduction into Advanced Foreign Currency Valuation (5 Dec 2023).

rrency Valuation
(FINS_FXV) in S/4HANA 2022 OP (4 Sep 2024). Exact INR 80→85 example and demonstration.
Open source ↗
[7] SAP Community (SAP-managed) — Introduction into Advanced Foreign Currency Valuation (5 Dec 2023).
Delta logic, currency concept, grouping, restrictions and classic comparison; primarily public-cloud-oriented
but notes On-Premise availability since OP 2022.
Open source ↗
[8] SAP Community (SAP-managed) — Perform Foreign Currency Valuation with the new Advanced
Valuations (20 Apr 2022). Advanced FCV features and activation side effects; Cloud release context.
Open source ↗
[9] User-provided YouTube source — What is Advanced Foreign Currency Valuation (FINS_FXV) in S/4HANA
2022 (Simple SAP S/4 HANA FICO; 4 Sep 2024; 31:41). The screenshot appendix uses genuine stills captured
from this public video.
Open source ↗
Use and attribution
Screenshots in Appendix A are authentic still frames from the public source video, reproduced as timestamped
illustrative references for this guide. They are not SAP system screenshots captured from the reader’s tenant
and do not replace current product documentation. Account numbers, company codes, interface labels and
examples are demo-specific.
Appendix A. Genuine video screenshots with
timestamps

captured from the reader’s tenant
and do not replace current product documentation. Account numbers, company codes, interface labels and
examples are demo-specific.
Appendix A. Genuine video screenshots with
timestamps
The following are representative source frames, not AI-generated reconstructions. Each time stamp links
to the corresponding point in the original video. The gallery covers the video’s key teaching slides,
configuration screens, valuation run and posted-result review; it is a curated key-frame set rather than
every video frame.
Source
What is Advanced Foreign Currency Valuation (FINS_FXV) in S/4HANA 2022 ↗ · Simple SAP S/4 HANA FICO · 4
Sep 2024
Time Frame Time Frame
00:01 Video title and learning agenda 01:13 Need for period-end valuation
04:35 Realized versus unrealized FX 06:00 Advanced valuation features
07:05 Classic vs advanced differences 09:58 Comparison / methods
12:15 Run-screen comparison 13:40 Activation effects
15:25 Configuration overview 17:40 INR/USD example and entry
18:20 IMG navigation 20:10 Valuation-rule setup
21:10 Account / semantic tag 22:40 Rule steps and rate/method
24:40 Exchange-rate maintenance 26:20 Supplier open item
27:55 FINS_FXV parameters 28:10 Test-run result
28:45 Valuation result list 29:20 Update-run result

21:10 Account / semantic tag 22:40 Rule steps and rate/method
24:40 Exchange-rate maintenance 26:20 Supplier open item
27:55 FINS_FXV parameters 28:10 Test-run result
28:45 Valuation result list 29:20 Update-run result
30:30 Posted journal entry 31:00 Local-currency lines
00:01 · Video title and learning agenda Watch at this time ↗
01:13 · Need for valuation: period-end remeasurement before financial statements Watch at this time ↗
04:35 · Realized versus unrealized foreign-exchange gain/loss Watch at this time ↗
06:00 · Advanced valuation feature overview Watch at this time ↗
07:05 · Classic versus advanced: key differences and posting logic Watch at this time ↗
09:58 · Comparison table and valuation-method section Watch at this time ↗
12:15 · Classic and advanced selection-screen comparison Watch at this time ↗
13:40 · Effect on existing data after Advanced Valuation activation Watch at this time ↗
15:25 · Configuration overview and prerequisites Watch at this time ↗
17:40 · Video’s INR/USD example and proposed journal entry Watch at this time ↗
18:20 · IMG configuration navigation Watch at this time ↗
20:10 · Valuation-rule and method setup screen Watch at this time ↗
21:10 · Account / semantic-tag configuration screen Watch at this time ↗

Watch at this time ↗
18:20 · IMG configuration navigation Watch at this time ↗
20:10 · Valuation-rule and method setup screen Watch at this time ↗
21:10 · Account / semantic-tag configuration screen Watch at this time ↗
22:40 · Valuation rule steps and exchange-rate/method fields Watch at this time ↗
24:40 · Exchange-rate maintenance screen Watch at this time ↗
26:20 · Supplier invoice and open-item example Watch at this time ↗
27:55 · FINS_FXV parameters: company code, ledger, key date and test run Watch at this time ↗
28:10 · Test-run result view Watch at this time ↗
28:45 · Valuation result list and line-level differences Watch at this time ↗
29:20 · Update-run results and posting reference Watch at this time ↗
30:30 · Posted general-ledger document display Watch at this time ↗
31:00 · Local-currency journal lines and account view Watch at this time ↗
End of guide. Review the cited SAP Help pages for your exact product version before configuring or posting in a live system.