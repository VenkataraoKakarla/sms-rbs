# 📩 SMS-RBS (Reverse Bank Statement) Project

## 📌 Overview

The **SMS-RBS (Reverse Bank Statement)** project reconstructs a **bank-statement-like view** of a user’s financial behavior by analyzing **banking and transactional SMS messages**.

Unlike traditional incremental transaction tagging, this system **reprocesses historical SMS data whenever new messages arrive**, enabling **context-aware reclassification** (e.g., salary, EMI, loan disbursal) that depends on **patterns across multiple messages and time windows**.

This pipeline powers **Risk, Credit, Growth, and Collections** use-cases in an NBFC ecosystem.

---

## 🎯 Key Objectives

- Parse raw SMS messages into structured financial transactions  
- Identify **salary, loan, EMI, balance, and business income** patterns  
- Generate **bank-statement-like outputs** without direct bank integration  
- Build a scalable **feature mart** for ML & rule-based models  
- Ensure **high accuracy via historical re-evaluation**

---

## 🧠 Why Full Reprocessing (Not Incremental)?

Many financial events **cannot be identified from a single SMS**.

### Example
- **March**  
  ₹45,916 credited to your account  

- **April**  
  Salary of ₹45,916 credited  

Using April’s message, the system:
- Tags **April as salary**
- Revisits **March** and reclassifies it as **salary**

➡️ This requires **reprocessing old SMS using new context**, making incremental-only approaches insufficient.

---

## 🏗️ High-Level Architecture

Raw SMS  
→ Normalization & Cleaning  
→ Rule + ML Classification  
→ Transaction Reconstruction  
→ Feature Engineering  
→ RBS Feature Mart  

---

## 📂 Repository Structure

```
sms-rbs/
├── code/
│   ├── ingestion/
│   ├── preprocessing/
│   ├── classification/
│   ├── rbs_builder/
│   └── feature_engineering/   
│
├── data/
│   ├── sample_input/
│   └── sample_output/
│
├── tests/
├── logs/
│
├── README.md
└── .gitignore
```

---

## ⚙️ Core Components

### SMS Ingestion
- Loads raw SMS without parsing
- Supports bulk & incremental loads
- Preserves timestamps and ordering

### Preprocessing
- Text normalization
- Regex standardization
- Entity extraction (amount, bank, date)

### Classification Engine
- Rule-based tagging
- ML fallback for ambiguous cases
- Pattern recognition across messages

### Reverse Bank Statement Builder
- Transaction reconstruction
- Debit / credit identification
- Message linking (EMI reminders, debits)

### Feature Engineering
Generates features such as:
- Salary consistency & recency
- Credit/debit ratios
- Balance trends
- EMI burden indicators
- Business income frequency

---

## 📊 Outputs

- Transaction-level RBS
- Monthly RBS summaries
- Feature mart for ML models
- Tagging confidence scores

---

## 🔐 Data Privacy & Security

- All data is masked or pseudo-anonymized
- No real PII is stored
- Designed for secure, access-controlled environments

---

## 🚀 Use-Cases

- Credit underwriting (PL, CC, UCL)
- Salary verification
- Banking wellness scoring
- Fraud & anomaly detection
- Growth & collections optimization

---

## 🛠️ Tech Stack

- Python (Pandas, Polars, Regex, ML)
- SQL / Snowflake
- Rule engines + ML models
- GitHub / VS Code

---

