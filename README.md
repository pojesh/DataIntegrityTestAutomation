Data Integrity Test Automation
Project Author: Pojesh

1. Project Overview
This UiPath Test Automation project is designed to perform data integrity checks between a set of test data in an Excel file and a master loan application database. The primary goal is to ensure that key information for loan applicants is consistent across both data sources.

The process operates as a data-driven test case. For each applicant listed in the Test Data.xlsx file, it queries the Loan Applications.accdb database using the UserID and verifies that the LastName and LoanAmountRequested fields match their expected values.
2. Features
Data-Driven: The test is driven by the entries in Test Data.xlsx, allowing for easy addition or modification of test cases without changing the workflow.
Database Integration: Connects to a Microsoft Access (.accdb) database to retrieve live data for comparison.
Automated Verification: Uses UiPath's testing activities to programmatically assert that data values are correct.
Detailed Logging:
Generates specific error messages upon verification failure.
Provides informational logs for each successful verification.
Independent Test Execution: Each row in the Excel file is treated as a separate test variation, ensuring all records are checked regardless of individual failures.
3. Prerequisites
UiPath Studio (v2022.10 or later recommended)
The following UiPath Activity Packages installed:
UiPath.Testing.Activities
UiPath.Database.Activities
4. Project Structure
The project follows a standard structure:

DataIntegrityTestAutomation/
│
├── Data/
│   ├── Loan Applications.accdb     # The master database file.
│   └── Test Data.xlsx              # The Excel file containing test cases.
│
├── Verify_Loan_Data.xaml           # The main data-driven test case workflow.
└── project.json                    # The project definition file.
5. Workflow Activity Structure (Verify_Loan_Data.xaml)
The following outlines the hierarchical structure of the activities within the main test case sequence. The entire sequence is executed for each data row from the test file.

Main Test Case Sequence
|
+-- Arguments (User_ID, Given_Name, Last_Name, Occupation, Age, Loan_Amount, Yearly_Income)
|
+-- Variables (dbConnection, queryResult)
|
+-- Given (Sequence)
|   |
|   +-- Connect to Database (Output: dbConnection)
|
+-- When (Sequence)
|   |
|   +-- Execute Query (Input: dbConnection, SQL with User_ID parameter; Output: queryResult)
|
+-- Then (Sequence)
|   |
|   +-- If (Condition: queryResult.Rows.Count > 0)
|       |
|       +-- Then (Sequence)
|       |   +-- Verify Expression (Check Last Name)
|       |   +-- Log Message (Success for Last Name)
|       |   +-- Verify Expression (Check Loan Amount)
|       |   +-- Log Message (Success for Loan Amount)
|       |
|       +-- Else (Sequence)
|           +-- Throw (BusinessRuleException for "User not found")
|
+-- Disconnect from Database (Input: dbConnection)
6. Setup and Configuration
Clone/Download: Place the project folder on your local machine.
Open Project: Open the root folder in UiPath Studio.
Install Dependencies: Studio should prompt you to restore dependencies. If not, open Manage Packages and ensure all required packages from the Prerequisites section are installed.
Check Data Files: Confirm that the Data folder exists and contains both Loan Applications.accdb and Test Data.xlsx. The database connection string uses absolute paths, so modify them before execution.
7. How to Run the Test Case
Open the Verify_Loan_Data.xaml file in UiPath Studio.
In the top ribbon, click "Run".
8. Understanding the Output
The results of the test run will be displayed in the Output panel.

A Passed Test: A successful verification will result in a Info log message being printed.
A Failed Test: If a verification fails, an Error message will be logged with the specific details you configured in the OutputMessageFormat property. The execution for that data row will stop, and the test runner will move on to the next row.






