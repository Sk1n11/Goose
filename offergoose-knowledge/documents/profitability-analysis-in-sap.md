# Profitability Analysis in SAP.pdf

Topic: General

Profitability Analysis
Profitability Analysis:
Profitability Analysis (CO-PA) enables you to evaluate market segments, which can be classified
according to products, customers, orders or any combination of these, or strategic business units,
such as sales organizations or business areas, with respect to your company's profit or contribution
margin.
The aim of the system is to provide your sales, marketing, product management and corporate
planning departments with information to support internal accounting and decision-making.
Two forms of Profitability Analysis are supported:
Costing-based and account-based
1. Costing-based Profitability Analysis is the form of profitability analysis that groups costs
and revenues according to value fields and costing-based valuation approaches.
It guarantees you access at all times to a complete, short-term profitability report.
2. Account-based Profitability Analysis is a form of profitability analysis organized in accounts
and using an account-based valuation approach.
The distinguishing characteristic of this form is its use of cost and revenue elements.
It provides you with a profitability report that is permanently reconciled with financial
accounting.
1. Define operating Concern

.
The distinguishing characteristic of this form is its use of cost and revenue elements.
It provides you with a profitability report that is permanently reconciled with financial
accounting.
1. Define operating Concern
On the SAP Easy Access, Enter T-code as SPRO and press enter
Click on SAP Reference IMG button
Path: Controlling→Profitability Analysis→structures→Define Operating Concern→Click on
Maintain Operating concern (or)
Enter transaction code as KEA0
Enter operating concern as 1102 and press enter
Click on yes
Click on continue
Enter description as 1102 operating concern
Select Costing-based and account-based checkboxes
Click on Save
Click on Create button
In Chars tab under Transfer Form select “REGIO-Region” and click on Transfer fields.
So the fields will transfer to “Data structure” window
Now click on Value fields
In the “Value Fields” tab under “copy form” window select the require fields
ABSMGSales quantity
ERLOSRevenue
Select KWMKAD-Advertising
KWSMKTSales & Marketing
KWVKPVSales Commission
Select VTRGK-Sales Overhead
VV001-COGS
Click on Transfer Fields
So the Field will transfer to “Data Structure” window as below.
Click on Activate button
It shows that all objects for Structure CE1102 activated
Click on Back button
Click on Yes
Click on Continue

VV001-COGS — ck on Transfer Fields
So the Field will transfer to “Data Structure” window as below.
Click on Activate button
It shows that all objects for Structure CE1102 activated
Click on Back button
Click on Yes
Click on Continue
In the Attributes tab, enter the operating concern currency as INR
Enter the Fiscal Year Variant as K4 and click on save
Click on Yes
Here the environment was generated completely
Click on Save
2. Assign Controlling Area to Operating concern
Enter T-code as SPRO in the SAP Easy Access
Click on SAP Reference IMG
Path: Enterprise Structure→Assignment→Controlling→Assign Controlling area to operating
concern (0r) Transaction code: KEKK
Click on Opco options
Select 1102 Operating Concern and click on continue
Here we see the Operating Concern and click on save
Click on create request
Enter description as below and click on save
Click on continue
Here Data was saved
Click on save
3. Set Operating Concern:
Path: SPRO→Controlling→Profitability Analysis→Structures→Set Operating Concern
Transaction Code: KEBD
Enter the operating Concern and click on enter
Select Costing-Based check box and click on continue
4. Assign Value Fields:
Path: SPRO→Controlling→Profitability Analysis→Flows of Actual Values→Transfer of Billing
Documents→Assign Value fields
Transaction Code: KE4I

VV001-COGS — Select Costing-Based check box and click on continue
4. Assign Value Fields:
Path: SPRO→Controlling→Profitability Analysis→Flows of Actual Values→Transfer of Billing
Documents→Assign Value fields
Transaction Code: KE4I
Click on Maintain Assignment of SD conditions to CO-PA Value Fields and click on choose
Click on New Entries
Maintain the below parameters
Click on Save
Click on Create request
Enter description and click on save
Click on continue
Here Data was saved
Click on Back to SPRO screen
5. Assign Quantity Fields:
Path: SPRO→controlling→Profitability Analysis→Flows of Actual values→Transfer of Billing
Documents→ Assign Quantity fields
Transaction code: E4MI
Click on New Entries
Enter below parameters
Click on Save
Click on create Request
Enter description and click on save
Click on continue
Here Data was saved
Click on back to SPRO Screen
6. Maintain PA Transfer Structure for Direct Postings
PA Transfer Structure FI is used to assign Direct MM and FI Revenue/Expenses to the CO-PA
Value.
Path: SPRO→Controlling→Profitability Analysis→Flows of Actual Values→Direct Posting from
FI/MM→ Maintain PA Transfer Structure for Direct postings
Transaction code as KE12
Select FI Check box and Click on” Assignment Lines” under Dialog Structure

itability Analysis→Flows of Actual Values→Direct Posting from
FI/MM→ Maintain PA Transfer Structure for Direct postings
Transaction code as KE12
Select FI Check box and Click on” Assignment Lines” under Dialog Structure
Click on Controlling Area as 2018 and click on continue
Click on New entries
Enter new Assignment values like “60, 70” with Text and save
Select Assignment line “60” and click on “Source” under Dialog Structure
Enter cost element values
Select Cost element tab, controlling area is 2018 and click on Start search
Select the line and click on continue
Here we see the Cost element as 400400 and click on “Value Fields” under Dialog Structure
Click on new entries
Enter Quantity /Value as value field
Fixed/Variable as 3 and Value Field as KWSMKT
Select the line and click on “Assignment lines” Under Dialog Structure
Select the 70 Assignment and click on “source” under Dialog Structure
Enter cost element values and click on “Value Fields”
Click on New Entries
Enter below Parameters and click on enter
Click on enter
Click on create request
Enter description and click on save
Click on continue
Here we data was saved
Click on Save
7. Define Structure of Cost Center Assessment Process Cost Assessment

and click on enter
Click on enter
Click on create request
Enter description and click on save
Click on continue
Here we data was saved
Click on Save
7. Define Structure of Cost Center Assessment Process Cost Assessment
Path: SPRO→Controlling→Profitability Analysis→Flows Of Actual Values→Transfer of
overhead→Assess Cost Center Costs/Process costs→Define Structure of cost center
Assessment/Process Cost Assessment
Transaction Code: KEU1
Click on Create Actual Assessment and click on choose
Enter Cycle as ASS110 and Start Date as 04/06/2018 and click on enter
Enter Text as Process Cost Assessment and enter CO Area as 2018
Click on save
Here Cycle ASS110, with starting date has been saved
Click on back
Click on Change Actual Assessment and click on choose
Enter the Cycle as ASS110 and Start date and Click on next
Click on Attach Segment
Enter Segment name as s1 (segment1)
In the Segment Header tab, enter the
Field Value field as KWSMKT
Val. Fld Var. Cst as KWSMKT
Alloc. Structure as L1
Enter below details
In the Allocation Structure, Right click on it and click on create allocation structure
Select the L1 Allocation structure and Click on Assignments under Dialog Structure
Click on New entries
Enter below entries in the assignments and click on source under dialog structure

ck on create allocation structure
Select the L1 Allocation structure and Click on Assignments under Dialog Structure
Click on New entries
Enter below entries in the assignments and click on source under dialog structure
Enter the cost elements and click on Assessment Cost element under Dialog structure
Click on New entries
Enter the assessment Cost element and click on Settlement Cost elements
Click on new entries
Enter below entries
Click on Save
Click on create Request
Enter description as allocation structure and click on save
Click on Continue
Here Data was saved
Click on Back
In the Senders/Receivers Tab, Enter Sender Cost Center and cost element
In the receiver, enter the Company code as 2018
Creating cost center ks01
Country as IN
Division as 00
In the Receiver Tracing Factor tab, Enter Record type as A
Plan/Act. Indic as 0
Click on Receiver Weighting Factors tab
Select the Company Code check box and click on continue
Click on Save
Here Cycle ASS110 has been saved
Click on back
8. Activate Profitability Analysis:
Path: SPRO→Controlling→Profitability Analysis→Flows of Actual Values→ Activate
Profitability Analysis
Transaction Code as KEKE
Click on options On the Active Status
Select 4 (component active for both types of profitability Analysis) and click on Continue

Analysis→Flows of Actual Values→ Activate
Profitability Analysis
Transaction Code as KEKE
Click on options On the Active Status
Select 4 (component active for both types of profitability Analysis) and click on Continue
Click on Save
Click on Create request
Enter description and click on save
Click on continue
Here data was saved
9. Define Key Figure schemes
Path: SPRO→Controlling→Profitability Analysis→Flows of Actual Values→Information
Systems→Report Components→Define Key Figure schemes
Transaction code: KER1
Click on New entries
Enter new values for Key figure scheme as 01
Medium-Length Text as 1102 Key Figure and click on Elements of the key figure scheme Under
Dialog Structure
Click on New Entries
Enter below details
Enter below details short text, medium-length text, Long Text
Click on formula Editor
In the value field, enter Revenue and click on entry
Here we see Revenue in Formula line and click on this symbol
Here we see Formula Line ‘Revenue’ – and in the Value field, enter COGS and click on entry
In the Formula Line ‘Revenue’ –‘COGS’ and click on check
Click on Back
Click on Save
Click on Create Request
Enter description and click on Save
Click on Continue
Key figure Scheme was saved
10. Create Profitability Report

the Formula Line ‘Revenue’ –‘COGS’ and click on check
Click on Back
Click on Save
Click on Create Request
Enter description and click on Save
Click on Continue
Key figure Scheme was saved
10. Create Profitability Report
Path: SPRO→Controlling→Profitability Analysis→Information System→Report
Components→Create profitability Report
Transaction code: KE31
Select Create Profitability Report and click on choose
Enter Report name and select Basic Report and click on create button
Select Country and Region checkboxes in the characteristics tab
Select company code and fiscal year
Click on Transfer fields
Click on check box against “Country”
Enter Local Variable as country and click on continue
Click on Region Check box
Enter Local Variable as Region and click on continue
Click on check box against “Company code”
Enter Local Variable as Comcode and click on continue
Click on check box against “Fiscal Year”
Enter Local Variable as Fiscal year and click on continue
Here all check boxes are selected
Click on Key figure tab
Enter the report description as region wise Profitability Report
Enter key Figure Scheme as 1102 Key Figure
Select the contribution as 1102 and click on Transfer fields
Click on Variables tab,
Enter below details
Click on save
Report was saved
Click on back
11.

se Profitability Report
Enter key Figure Scheme as 1102 Key Figure
Select the contribution as 1102 and click on Transfer fields
Click on Variables tab,
Enter below details
Click on save
Report was saved
Click on back
11. Set Control Parameters for Actual Data
Path: SPRO→ Controlling→Profit center Accounting →Controlling Area Settings→Activate
Direct Postings→Click on Set Control Parameters for actual data
Enter controlling area as 2018 and click on continue
Click on New entries
Enter below details from Year 2018, Select the line items and online transfer checkbox
Click on save
Here data was saved
12. Maintain Plan Versions
Path: SPRO→Controlling→Profit center Accounting→Basic settings→controlling Area
Settings→Activate Direct postings→Plan Versions→Maintain Plan Versions
Transaction Code: OKEQ
Select ‘0’ version and click on Settings for profit center accounting
Click on New entries
Enter below details and select online transfer and Line items check box and Enter ExRateType as
M
Click on save
Click on create Request
Enter Description as Maintain plan versions and click on save
Click on Continue
Here data was saved
13. Define Number ranges for local Documents
Path: SPRO→Controlling→Profit center Accounting→Actual Postings→Define number ranges
for local documents

plan versions and click on save
Click on Continue
Here data was saved
13. Define Number ranges for local Documents
Path: SPRO→Controlling→Profit center Accounting→Actual Postings→Define number ranges
for local documents
Transaction code: GB02
Click on define groups
Click on create
Enter the company code as 2018 and click on get
Enter group as 1102 number ranges and enter below details
Click on save
Click on continue
Number ranges were saved
14. Maintain Automatic Account Assignment of Revenue Elements
Path: SPRO→Controlling→Profit center Accounting→Actual postings→Maintain Automatic
account Assignment of Revenue Elements
Transaction code: OKB9
Click on New entries
Enter below details and click on enter
Select the line and click on detail per business area/valuation area
Click on New entries
Enter below details and click on save
Click on Create request
Enter below description and click on save
Click on continue
Here data was saved
15. Choose Additional Balance Sheet and P&L Accounts:
Path: SPRO→Controlling→Profit center Accounting→Actual postings→Choose Additional
Balance Sheet and P&L accounts→Choose Accounts
Click on new entries
Enter the below details
Click on Prctr Det icon
Click on create step
Enter below description
Enter below details and click on Maintain Rule Values

onal
Balance Sheet and P&L accounts→Choose Accounts
Click on new entries
Enter the below details
Click on Prctr Det icon
Click on create step
Enter below description
Enter below details and click on Maintain Rule Values
Click on Save
Enter below details and click on enter
Click on save
Here Data was saved
16. Raise an sales order
Path: Logistics→Sales and Distribution→Sales→VA01-Create
Transaction code: VA01
Enter below details and click on next
Enter the Sold-to-party and customer reference and click on enter
Enter the material in the all items
Double click on Material 216
Choose Shipping tab, enter Storage Location as 01
Click on save
Click on Save
Here order was saved
17. Posting outbound delivery
Path: Logistics→Sales and Distribution→Shipping and Transportation→outbound
Delivery→create→Single Document→VL01N-with reference to sales order
Enter the shipping point as 2018 and order number and click on continue
Here we see our material
In the Picking tab, enter the picked quantity as 1
Enter Post Goods Issue button
Here outbound delivery has been saved
18. Billing the document:
Path: Logistics→Sales and distribution→Billing→Billing document→VF01-create
Transaction Code as VF01
Here we see saved document and click on enter
Click on save
Here Document was saved