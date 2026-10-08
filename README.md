# 🏦 Banking Customer 360 & Branch Intelligence Assistant

An AI-powered, natural language-to-SQL analytics tool designed for Branch Heads, Relationship Managers, and Audit Teams. This application allows non-technical banking staff to query complex customer portfolios, track loan delinquency, identify cross-sell opportunities, and monitor service SLAs using plain English—while strictly adhering to ISG (Information Security Group) compliance and data governance standards.

### ✨ Features

* **Governed Text-to-SQL:** Leverages Google's Gemini API integrated with a banking domain semantic layer (CASA, NPA, DPD definitions) to translate plain English into accurate, executable SQL queries.
* **Zero-Trust Security (AST Validation):** Utilizes `sqlglot` to parse the Abstract Syntax Tree (AST) of generated queries before execution, guaranteeing 100% deflection of non-`SELECT` operations and blocking unauthorized access to sensitive columns.
* **Hard Row-Level Security (RLS):** Dynamically injects role-based filters (Branch ID, RM ID) outside of the LLM prompt to ensure strict zero-trust data boundary isolation across accounts.
* **ISG Audit Logging & PII Masking:** Automatically obfuscates sensitive identifiers (like phone numbers and account numbers) and records 100% of user queries, execution latency, and rule violations into an immutable compliance ledger.
* **Transparent Explainability:** Delivers dual-pane outputs featuring the executed SQL alongside a plain-English explanation of the logic, aligning with "Fair to Bank, Fair to Customer" transparency principles.

### 🛠️ Tech Stack

* **Frontend UI:** Streamlit (Python)
* **LLM Engine:** Google Gemini API
* **Database:** SQLite (Local synthetic staging)
* **Security & AST Parsing:** `sqlglot`
* **Data Processing:** `pandas`, `faker` (Synthetic Data Generation)
* **Environment Management:** `python-dotenv`

### 🗄️ Database Schema

The application queries a local SQLite database (`banking_c360.db`) structured with a relational schema containing over 130,000 synthetic records:

* **CUSTOMER_MASTER:** Anchor table containing demographics, segments (Retail/Salary/HNI), and KYC status.
* **BRANCH_DIMENSION:** Lookup table for regional branches, tier classification, and branch heads.
* **ACCOUNT_PORTFOLIO:** Tracks product holdings (Savings/Current/Loans), balances, credit card status, and delinquency days (DPD).
* **TRANSACTION_LEDGER:** Operational core tracking debit/credit volumes across channels (UPI, iMobile, NetBanking, ATM, Branch).
* **SERVICE_REQUEST:** Tracks customer complaints, resolution TAT (Turnaround Time), and SLA breach metrics.
* **AUDIT_LOG:** Immutable compliance table recording system telemetry, query history, and RBAC validations.

### 🚀 Getting Started

**Prerequisites**

* Python 3.8+
* A valid Google Gemini API Key

**Installation & Setup**

1. Clone the repository and install the required dependencies from `requirement.txt`:
```bash
pip install -r requirement.txt

```


2. Configure your environment variables by adding your Gemini key to the `.env` file:
```env
GOOGLE_API_KEY="your_api_key_here"

```


3. Generate the synthetic banking database (this will seed the 6 tables with 130,000+ realistic, PII-free banking records):
```bash
python setup_db.py

```


4. Launch the Streamlit application:
```bash
streamlit run app.py

```
