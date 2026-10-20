# sap_fi_automatic_payment_run.htm

Topic: Free SAP FICO sources — auto-fetched

SAP FI - Automatic Payment Run

Home
Whiteboard
Practice Code
Graphing Calculator
Online Compilers
Articles
Tools

Categories

Explore Categories
Find the perfect tutorial for your learning journey

Python Technologies Databases Computer Programming Web Development Java Technologies Computer Science Mobile Development Big Data & Analytics Microsoft Technologies DevOps Latest Technologies Machine Learning Digital Marketing Software Quality Management Tutorials View All Categories

Tutorials
Courses
Jobs
Login

[Image description: SAP FICO Tutorial]

SAP FICO - Home

SAP FI - Overview

SAP FI - Submodules

SAP FI - Company Basics

SAP FI - Define Business Area

SAP FI - Define Functional Area

SAP FI - Define Credit Control

SAP FI - General Ledger

SAP FI - COA Group

SAP FI - Retained Earnings Account

SAP FI - G/L Account

SAP FI - Block G/L Account

SAP FI - Deleting G/L Accounts

SAP FI - Financial Statement Version

SAP FI - Journal Entry Posting

SAP FI - Fiscal Year Variant

SAP FI - Posting Period Variant

SAP FI - Field Status Variant

SAP FI - Field Status Group

SAP FI - Define Posting Keys

SAP FI - Define Document Type

SAP FI - Document Number Ranges

SAP FI - Post with Reference

SAP FI - Hold a G/L Document Posting

SAP FI - Park a G/L Document Posting

SAP FI - — Field Status Group

SAP FI - Define Posting Keys

SAP FI - Define Document Type

SAP FI - Document Number Ranges

SAP FI - Post with Reference

SAP FI - Hold a G/L Document Posting

SAP FI - Park a G/L Document Posting

SAP FI - G/L Reporting

SAP FI - Accounts Receivable

SAP FI - Customer Master Data

SAP FI - Block a Customer

SAP FI - Delete a Customer

SAP FI - Customer Account Group

SAP FI - One-Time Customer Master

SAP FI - Post a Sales Invoice

SAP FI - Document Reversal

SAP FI - Sales Returns

SAP FI - Post Incoming Payment

SAP FI - Foreign Currency Invoice

SAP FI - Incoming Partial Payments

SAP FI - Reset AR Cleared Items

SAP FI - Credit Control

SAP FI - Accounts Payable

SAP FI - Create a Vendor

SAP FI - Create Vendor Acct Group

SAP FI - Display Changed Fields

SAP FI - Block a Vendor

SAP FI - Delete a Vendor

SAP FI - One-Time Vendor

SAP FI - Post Purchase Invoice

SAP FI - Purchases Returns

Post Outgoing Vendor Payment

SAP FI - Foreign Currency Invoice

Withholding Tax in vendor invoice

SAP FI - Outgoing Partial Payments

SAP FI - Reset AP Cleared Items

SAP FI - Automatic Payment Run

SAP FI - Posting Rounding Differences

SAP FI - Month End Closing

SAP FI - Dunning

SAP FI - Exchange Rates

SAP FI - Tables in Module

SAP FI - AR Invoice Processes

t AP Cleared Items

SAP FI - Automatic Payment Run

SAP FI - Posting Rounding Differences

SAP FI - Month End Closing

SAP FI - Dunning

SAP FI - Exchange Rates

SAP FI - Tables in Module

SAP FI - AR Invoice Processes

SAP FI - AR Account Analysis

SAP FI - AR Reporting

SAP FI - AA Overview

SAP FI - AA Asset Explorer

SAP FI - Cash Management

SAP CO - Overview

SAP CO - Submodules

SAP CO - Cost Center

SAP CO - Create Cost Center

SAP CO – Post to a Cost Center

SAP CO - Internal Orders

SAP CO - Settlement of IO

SAP CO - Profit Center

SAP CO - Postings to Profit Center

Profit Center Standard Hierarchy

Assigning Cost to Profit Centers

Assigning Materials to Profit Center

SAP CO - Tables in Module

SAP CO - Product Costing

SAP CO - Profitability Analysis

SAP CO - Planning Methods

SAP FI - Integration

SAP FICO - Questions Answers

SAP FICO - Quick Guide

SAP FICO - Useful Resources

SAP FICO - Discussion

Selected Reading

UPSC IAS Exams Notes

Developer's Best Practices

Questions and Answers

Online Resume Builder

HR Interview Questions

Computer Glossary

Who is Who

Home

Sap_fico

SAP FI - Automatic Payment Run

SAP FI - Automatic Payment Run

Previous

Quiz

Next

Best Practices

Questions and Answers

Online Resume Builder

HR Interview Questions

Computer Glossary

Who is Who

Home

Sap_fico

SAP FI - Automatic Payment Run

SAP FI - Automatic Payment Run

Previous

Quiz

Next

Automatic Payment Program (APP) serves the purpose of posting accounts payable like payment to a vendor based on vendor invoices automatically.

APP is used to find out due/overdue invoices and to process a list of customer and vendor invoices to make payments in one go. APP cannot be used for all company codes from different countries.

APP has the following categories −

Setup all company codes

Setup paying company codes

Payment method per country

Payment method per country code

Bank Selection

House Bank

Use the T-code FBZP to see all the following options.

[Image description: Automatic Payment Program]

Setup all Company Codes

Click the option All Company Code in the above screen. A new window will open. Go to New Entries.

[Image description: Setup all Company Codes]

Enter the company code in the field Paying Company Code. Select the checkboxes Pyt. Meth Suppl. and Max. Cash Discount as shown below −

[Image description: Company Code Field]

Setup Paying Company Codes

Click Paying Company Codes and go to New Entries.

aying Company Code. Select the checkboxes Pyt. Meth Suppl. and Max. Cash Discount as shown below −

[Image description: Company Code Field]

Setup Paying Company Codes

Click Paying Company Codes and go to New Entries.

[Image description: Paying Company Codes]

It will open a new window wherein you need to provide the following details −

Paying company code

Min amount for incoming payment

Min amount for outgoing payment

Exchange rate differences, separate payment for each Ref.,Bill / Exch pymt.

[Image description: Paying Company Code Detail]

Payment Method in Country

Click the option Payment Method in Country on the main window. Go to New Entries as shown below.

[Image description: Payment Method in Country]

In the next screen, input the following details −

Enter Country name, Payment method and Description.

Select payment method: Incoming/outgoing payment.

Select payment method classification.

[Image description: Payment Method Detail]

Payment Method in Company Code

Click the option Pmnt. Method in Company Code on the main window. Go to New Entries as shown below −

[Image description: Payment Method Company Code]

In the next screen, enter the following details −

Enter Paying Co Code and Pymt. Method.

Enter minimum and maximum amount limits.

Go to New Entries as shown below −

[Image description: Payment Method Company Code]

In the next screen, enter the following details −

Enter Paying Co Code and Pymt. Method.

Enter minimum and maximum amount limits.

Select Bank selection control option.

Go to form data as shown below.

[Image description: Payment Company Code Detail]

Update Form Data Type. Click the Search button and select the value.

[Image description: Update Form Data]

[Image description: Structure Form Data]

Enter the field-drawer of the form and once all the details are supplied, click the Save button.

[Image description: Enter the Field-drawer]

Bank Determination

Click the option Bank Determination in the main window. Select Paying Company Code and click the option Select Block as shown below and go to Bank Account.

[Image description: Bank Determination]

Click the button Ranking Order and go to New Entries as shown below −

[Image description: Button Ranking Order]

Enter the new bank account details as shown below to create a bank account.

[Image description: New Bank Account Detail]

House Banks

House Banks provide the details of the bank account which is used by a company to make payments to its vendors and customers.

below to create a bank account.

[Image description: New Bank Account Detail]

House Banks

House Banks provide the details of the bank account which is used by a company to make payments to its vendors and customers.

Click the option House Banks on the main screen and enter the company code as shown below −

[Image description: House Banks]

The next window will show a list of all house banks which the company is using to make payments to its vendors and customers.

[Image description: House Bank Payments]

[Image description: Tutorix - AI Tutor]

Print Page

Previous
Quiz
Next

Advertisements

8

ABOUT US
OUR TEAM
CAREERS
JOBS
CONTACT US
TERMS OF USE
PRIVACY POLICY
REFUND POLICY
COOKIES POLICY
FAQ'S

[Image description: tutorials point logo]

[Image description: Download Android App]

[Image description: Download IOS App]

Tutorials Point is a leading Ed Tech company striving to provide the best learning material on technical and non-technical subjects.

Copyright 2026. All Rights Reserved.