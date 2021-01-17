# Banking App Pt.1

## DUE: 14/9/2020

## Description:

The Bank app is a console-based application that simulates banking operations. A customer can apply for an account, view their balance, and make withdrawals and deposits. An employee can approve or deny accounts and view account balances for their customers.

## Purpose:

We want to see that you can meet deadlines and that you can code. You are expected to complete the following requirements and give a 5 minute presentation of your project.

## Requirements:

- Build the application as a Maven project using Java 8
- All interaction with the user should be done through the console using the Scanner class
- Customers of the bank should be able to register with a username and password, and apply to open an account.
  - Customers should be able to apply for joint accounts
- Once the account is open, customers should be able to withdraw, deposit, and transfer funds between accounts
  - All basic validation should be done, such as trying to input negative amounts, overdrawing from accounts etc.
- Employees of the bank should be able to view all of their customers information
  - This includes:
    - account information
    - Account balances
    - Personal information
- Employees should be able to approve/deny open applications for accounts
- Bank admins should be able to view and edit all accounts
  - This includes:
    - Approving/denying accounts
    - withdrawing, depositing, transferring from all accounts
    - canceling accounts
- All information should be persisted using text files and serialization via Object Input/Output Stream
- 100% test coverage is expected using J-Unit
  - You should be using TDD
- Logging should be accomplished using Log4J
  - All transactions should be logged
