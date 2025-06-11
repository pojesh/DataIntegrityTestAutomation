# Data Integrity Test Automation

**Author:** Pojesh  
**Technology Stack:** UiPath Studio, Microsoft Access (.accdb)

---

## 1. Project Overview

This UiPath automation project performs data integrity testing between a test dataset in Excel and a master loan application database.

It uses a **data-driven** approach: for each loan applicant in `Test Data.xlsx`, the workflow queries `Loan Applications.accdb` using `UserID` and checks whether the `LastName` and `LoanAmountRequested` match expected values.

---

## 2. Features

- **Data-Driven Testing**  
  Easily extend or modify test cases via `Test Data.xlsx`—no need to change workflow logic.

- **Database Integration**  
  Connects directly to an `.accdb` Access database to retrieve live data.

- **Automated Verification**  
  Uses UiPath's testing activities to assert values programmatically.

- **Detailed Logging**  
  - Info logs for successful checks  
  - Specific error logs for failed assertions

- **Independent Test Execution**  
  Each row in the Excel file is treated as a separate test case. Execution continues even if some records fail.

---

## 3. Prerequisites

- **UiPath Studio**: v2022.10 or later  
- Install these packages from Manage Packages:
  - `UiPath.Testing.Activities`
  - `UiPath.Database.Activities`

---

## 4. Project Structure

DataIntegrityTestAutomation/
├── Data/
│ ├── Loan Applications.accdb # Master loan database
│ └── Test Data.xlsx # Test case inputs
├── Verify_Loan_Data.xaml # Main test workflow
└── project.json # Project definition

---

## 5. Workflow Breakdown (Verify_Loan_Data.xaml)

The workflow structure is as follows:

Main Test Case Sequence
├── Arguments:
│ ├── User_ID
│ ├── Given_Name
│ ├── Last_Name
│ ├── Occupation
│ ├── Age
│ ├── Loan_Amount
│ └── Yearly_Income
├── Variables:
│ └── dbConnection, queryResult
├── Given:
│ └── Connect to Database (dbConnection)
├── When:
│ └── Execute SQL Query with User_ID (queryResult)
├── Then:
│ ├── If queryResult.Rows.Count > 0:
│ │ ├── Verify Last Name
│ │ ├── Log Success (Last Name)
│ │ ├── Verify Loan Amount
│ │ └── Log Success (Loan Amount)
│ └── Else:
│ └── Throw BusinessRuleException ("User not found")
└── Disconnect from Database

---

## 6. Setup & Configuration

1. **Clone/Download** the project to your local system.
2. **Open** the root folder in UiPath Studio.
3. **Install Dependencies** via Manage Packages if not auto-restored.
4. **Check Data Files**: Ensure both `Loan Applications.accdb` and `Test Data.xlsx` are present in the `Data/` folder.
5. **Modify Connection Strings**: Update database paths if needed (they may be absolute).

---

## 7. How to Run

1. Open `Verify_Loan_Data.xaml` in UiPath Studio.
2. Click **Run** from the ribbon or use **Test Explorer**.

---

## 8. Test Output

- **Pass**: Logged as informational messages.
- **Fail**: Error messages logged with specific detail.
- Execution continues for all records, even if one fails.



