🧪 Data Integrity Test Automation
Author: Pojesh
Technology: UiPath Test Automation

📌 Project Overview
This UiPath automation project validates data integrity between a test dataset in Excel and a master Microsoft Access loan application database.

It operates as a data-driven test:
For each loan applicant listed in Test Data.xlsx, it queries the Loan Applications.accdb database using the UserID and verifies whether LastName and LoanAmountRequested match expected values.

🚀 Features
🔁 Data-Driven Testing
Easily extend or modify test cases via Test Data.xlsx—no workflow changes required.

🗃️ Database Integration
Connects directly to an .accdb Access database to fetch and compare live data.

✅ Automated Verification
Leverages UiPath’s testing activities to assert that records match.

📋 Detailed Logging

Informational logs on successful verifications

Specific error messages on failures

🧷 Independent Test Execution
Each Excel row is treated as a separate test variation. Execution continues even if some rows fail.

📦 Prerequisites
UiPath Studio – Version 2022.10 or later recommended

Install these Activity Packages via Manage Packages:

UiPath.Testing.Activities

UiPath.Database.Activities

🗂️ Project Structure
bash
Copy
Edit
DataIntegrityTestAutomation/
├── Data/
│   ├── Loan Applications.accdb     # Master loan database
│   └── Test Data.xlsx              # Test cases
├── Verify_Loan_Data.xaml           # Main test workflow
└── project.json                    # UiPath project configuration
🧩 Workflow Breakdown — Verify_Loan_Data.xaml
Main Test Case Sequence
plaintext
Copy
Edit
Main Sequence
├── Arguments: User_ID, Given_Name, Last_Name, Occupation, Age, Loan_Amount, Yearly_Income
├── Variables: dbConnection, queryResult
├── Given (Connect to database)
├── When (Execute SQL query using User_ID)
├── Then
│   ├── If (Result found?)
│   │   ├── ✔ Verify Last Name
│   │   ├── ✔ Log Success
│   │   ├── ✔ Verify Loan Amount
│   │   └── ✔ Log Success
│   └── Else (Throw "User not found" exception)
└── Finally: Disconnect from Database
⚙️ Setup & Configuration
Clone/Download this repository.

Open Project in UiPath Studio (.xaml or folder).

Restore Dependencies if prompted, or install them manually.

Verify Data Files
Ensure the Data/ folder contains:

Loan Applications.accdb

Test Data.xlsx

Update Connection Strings
Database connections may use absolute paths—update them before running.

▶️ Running the Test Case
Open Verify_Loan_Data.xaml in UiPath Studio.

Click Run in the top ribbon.

📊 Output and Test Results
✅ Pass: Successful checks log Info messages in the Output panel.

❌ Fail: Failed checks log Error messages with clear failure reasons.

Execution continues for remaining data rows even after individual failures.

