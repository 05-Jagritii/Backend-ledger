# Backend Ledger API

A **ledger-based financial transaction backend** built with **Node.js, Express, and MongoDB**.  
The system simulates core banking concepts such as **accounts, transactions, ledger entries, and system treasury funding**, ensuring **transaction consistency and auditability**.

## 📌 Features
- User authentication using **JWT**
- Account creation for users
- Ledger-based balance calculation
- Secure money transfers between accounts
- **Idempotent transactions** to prevent duplicates
- MongoDB **ACID transactions** for consistency
- System treasury account for initial funding
- Email notifications for transactions
- Token blacklist for secure logout

## 🏗️ Architecture Overview

The system follows a **ledger-based financial architecture**.

Instead of storing account balances directly, the balance is **derived from ledger entries**.

```
User
↓
Account
↓
Transaction
↓
Ledger Entries (Credit / Debit)
```
### Ledger Principle
This ensures:
- Auditability
- Financial integrity
- Immutable transaction history

## 🧰 Tech Stack

### Backend
- Node.js
- Express.js

### Database
- MongoDB
- Mongoose

### Authentication
- JWT (JSON Web Tokens)

### Email Service
- Nodemailer

### Deployment
- Render
## 📂 Project Structure
```
Backend-ledger
│
├── src
│ ├── controllers
│ ├── middleware
│ ├── models
│ ├── routes
│ ├── services
│ └── config
│
├── server.js
├── package.json
└── README.md
```
## 🔑 API Endpoints
### Authentication
Register User
```
POST /api/auth/register
```
Login User
```
POST /api/auth/login
```
Logout
```
POST /api/auth/logout
```
### Accounts
Create Account
```
POST /api/accounts
```
Get User Accounts
```
GET /api/accounts
```
Get Account Balance
```
GET /api/accounts/balance/:accountId
```
### Transactions
Transfer Money
```
POST /api/transactions
```
Create Initial Funds (System Treasury)
```
POST /api/transactions/system/initial-funds
```
## 🔁 Transaction Flow
A typical transfer follows these steps:

1. Validate request  
2. Check idempotency key  
3. Verify account status  
4. Derive sender balance from ledger  
5. Create transaction (PENDING)  
6. Create debit ledger entry  
7. Create credit ledger entry  
8. Mark transaction as COMPLETED  
9. Commit MongoDB transaction  
10. Send email notification  
## 🧪 Example Request
Transfer funds between accounts.
```
POST /api/transactions
```
Request Body:
json
```

{
  "fromAccount": "ACCOUNT_ID",
  "toAccount": "ACCOUNT_ID",
  "amount": 200,
  "idempotencyKey": "unique-key-123"
}
```
## Security Features
- JWT authentication middleware
- Token blacklist for logout protection
- Authorization checks for account ownership
- Idempotent transactions to prevent duplicate transfers


