# 💸 DMoney Transaction API – Newman Automation Report

A comprehensive API testing project for the **DMoney** digital financial platform, built with **Postman** and automated via **Newman** with an HTML Extra report.

---

## 📌 Table of Contents

- [💸 DMoney Transaction API – Newman Automation Report](#-dmoney-transaction-api--newman-automation-report)
  - [📌 Table of Contents](#-table-of-contents)
  - [📖 Project Overview](#-project-overview)
  - [🛠 Technology Stack](#-technology-stack)
  - [📄 API Documentation](#-api-documentation)
    - [Base URL](#base-url)
    - [Authentication Headers](#authentication-headers)
    - [Endpoints](#endpoints)
  - [🗂 Test Collection](#-test-collection)
  - [✅ Test Scenarios](#-test-scenarios)
  - [📁 Project Structure](#-project-structure)
  - [⚙️ Prerequisites](#️-prerequisites)
  - [🚀 Setup \& Installation](#-setup--installation)
  - [▶️ Running the Tests](#️-running-the-tests)
  - [📊 Newman Report](#-newman-report)
    - [Newman Run Dashboard](#newman-run-dashboard)
    - [📈 Test Run Summary](#-test-run-summary)
  - [👤 Author](#-author)
  - [📝 License](#-license)

---

## 📖 Project Overview

This project automates the end-to-end API testing of the **DMoney** transaction system, which simulates a mobile banking platform. The test suite covers the full transaction lifecycle — from user creation and authentication to deposits, money transfers, withdrawals, and payments.

---

## 🛠 Technology Stack

| Tool | Purpose |
|---|---|
| **Postman** | API collection authoring & manual testing |
| **Newman** | CLI runner to execute Postman collections |
| **newman-reporter-htmlextra** | Generates rich, interactive HTML test reports |
| **Node.js** | Runtime for the Newman runner script |
| **Lodash** | Random data generation inside pre-request scripts |

---

## 📄 API Documentation

> 🔗 **Postman Collection Link:** [d_Money_DB – Postman Collection](https://go.postman.co/collection/51322696-35746900-9a7c-4c9e-a1c1-2bf83f8fd2fb?source=collection_link)

The DMoney REST API is built around two main resource groups:

### Base URL
```
http://localhost:5000
```

### Authentication Headers
| Header | Value |
|---|---|
| `Authorization` | `Bearer <token>` |
| `X-AUTH-SECRET-KEY` | `ROADTOSDET` |

### Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/user/login` | Login as Admin, System, Agent, or Customer |
| `POST` | `/user/create` | Create a new user (Customer / Agent / Merchant) |
| `PATCH` | `/user/update/:id` | Update user status (e.g., activate) |
| `POST` | `/user/verify-otp` | Verify OTP to obtain user token |
| `POST` | `/transaction/deposit` | Deposit funds (System → Agent or Agent → Customer) |
| `POST` | `/transaction/sendmoney` | Send money between customers |
| `POST` | `/transaction/withdraw` | Cash-out from Customer to Agent |
| `POST` | `/transaction/payment` | Make a payment from Customer to Merchant |

---

## 🗂 Test Collection

> 🔗 **GitHub Repository:** [DMONEY-NEWMAN](https://github.com/Dima-1171/DMoney-Transaction-API)

The Postman collection file is located at:
```
collection/d_Money_DB3.json
```

Collection variables used:

| Variable | Description |
|---|---|
| `baseURL` | API base URL (`http://localhost:5000`) |
| `parnerKEY` | Partner secret key (`ROADTOSDET`) |
| `access_Token` | Admin JWT token |
| `access_Token2` | System JWT token |
| `Agent_token` | Agent JWT token |
| `customer1_token` | Customer 01 JWT token |
| `customer2_token` | Customer 02 JWT token |
| `customer_01_id` | Customer 01 user ID |
| `customer_02_id` | Customer 02 user ID |
| `agent_id` | Agent user ID |
| `merchant_id` | Merchant user ID |

---

## ✅ Test Scenarios

The collection covers **21 API requests** with **29 assertions** in a single iteration:

| # | Request Name | Method | Endpoint | Key Assertions |
|---|---|---|---|---|
| 1 | Admin Login | POST | `/user/login` | Login successful message, token captured |
| 2 | Create Customer 01 | POST | `/user/create` | User created, status is `pending` |
| 3 | Customer 1 Status Update | PATCH | `/user/update/:id` | Status code 200, user updated successfully |
| 4 | Create Customer 02 | POST | `/user/create` | User created |
| 5 | Customer 2 Status Update | PATCH | `/user/update/:id` | Status code 200, user status is `active` |
| 6 | Create Agent | POST | `/user/create` | Agent created, agent ID captured |
| 7 | Agent Status Update | PATCH | `/user/update/:id` | Status code 200, user status is `active` |
| 8 | Create Merchant | POST | `/user/create` | Merchant created, merchant ID captured |
| 9 | Merchant Status Update | PATCH | `/user/update/:id` | Merchant activated |
| 10 | System Login | POST | `/user/login` | System token captured |
| 11 | Deposit System to Agent | POST | `/transaction/deposit` | Deposit message, status 201, agent balance is `5000` |
| 12 | Agent Login | POST | `/user/login` | Agent credentials validated |
| 13 | Verify OTP (Agent) | POST | `/user/verify-otp` | OTP verified, role is Agent, agent token captured |
| 14 | Deposit Agent to Customer 01 | POST | `/transaction/deposit` | Status 201, commission is `50`, agent balance is `3050` |
| 15 | Customer 01 Login | POST | `/user/login` | Customer 01 authenticated |
| 16 | Verify OTP (Customer 01) | POST | `/user/verify-otp` | Customer 01 token captured |
| 17 | Send Money Customer 01 to Customer 02 | POST | `/transaction/sendmoney` | Fee is `5`, send money successful, balance is `995` |
| 18 | Customer 02 Login | POST | `/user/login` | Customer 02 authenticated |
| 19 | Verify OTP (Customer 02) | POST | `/user/verify-otp` | Customer 02 token captured |
| 20 | Customer 02 CashOut | POST | `/transaction/withdraw` | Withdraw successful, fee `5`, balance `495` |
| 21 | Customer 02 Payment | POST | `/transaction/payment` | Payment successful, fee `5`, balance `90` |

---

## 📁 Project Structure

```
DMONEY-NEWMAN/
├── collection/
│   └── d_Money_DB3.json          # Postman collection file
├── Reports/
│   ├── report.html               # Generated Newman HTML report
│   └── screenshots/
│       └── newman_report.png     # Newman Dashboard screenshot
├── node_modules/                 # Node.js dependencies
├── .env                          # Environment variables
├── .gitignore                    # Git ignore rules
├── package.json                  # Project metadata & scripts
├── report.js                     # Newman runner script
└── README.md                     # Project documentation
```

---

## ⚙️ Prerequisites

Make sure you have the following installed:

- **Node.js** (v14 or higher) – [Download](https://nodejs.org/)
- **npm** (comes with Node.js)
- **DMoney API server** running locally at `http://localhost:5000`

---

## 🚀 Setup & Installation

**1. Clone the repository:**
```bash
git clone https://github.com/Dima-1171/DMoney-Transaction-API.git
cd DMONEY-NEWMAN
```

**2. Install dependencies:**
```bash
npm install
```

---

## ▶️ Running the Tests

Run the Newman test suite and generate the HTML report:

```bash
npm test
```

This executes `node report.js` which:
1. Loads the Postman collection from `collection/d_Money_DB3.json`
2. Runs 1 iteration through all 21 requests
3. Generates an interactive HTML report at `Reports/report.html`

Open the report in your browser:
```bash
start Reports/report.html    # Windows
open Reports/report.html     # macOS
```

---

## 📊 Newman Report

The test report is generated using **newman-reporter-htmlextra** and saved to `Reports/report.html`.

### Newman Run Dashboard

![Newman Run Dashboard](./Reports/screenshots/newman_report.png)

### 📈 Test Run Summary

| Metric | Value |
|---|---|
| **Total Iterations** | 1 |
| **Total Requests** | 21 |
| **Total Assertions** | 29 |
| **Failed Tests** | 0 ✅ |
| **Skipped Tests** | 0 |
| **Total Run Duration** | 2.2s |
| **Total Data Received** | 3.59 KB |
| **Average Response Time** | 16ms |

> ✅ **All 29 assertions passed with 0 failures!**

---

## 👤 Author

**Sazia Afrin Dima**
QA Engineer | API Test Automation

---

## 📝 License

This project is licensed under the **ISC License**.
