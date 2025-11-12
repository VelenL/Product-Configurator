# 🧩 Product Configurator

This project provides a **dual-interface tool** designed to support both **product configuration** and **reverse lookup**. It enables users to generate valid product part numbers based on defined rules and constraints, and to decode existing part numbers back into detailed specifications.

---

## 🧭 Overview

The configurator consists of two main modules:

### 🔢 Part Number Generator

A dynamic interface that allows users to select product attributes step by step. Each choice updates the next available options according to dependency rules and compatibility constraints.

**Key Features**

* Sequential attribute selection (e.g., series → type → color → voltage)
* Rule-based validation and live feedback
* Incompatibility tooltip with explanations
* Warning and error handling for missing or invalid combinations
* Automatic **part code composition** and configuration summary
* Real-time image or product preview (optional)

**Example user flow**

1. Select product family and series
2. Choose attributes in sequence
3. The system filters incompatible options dynamically
4. When all selections are valid, the final part number is generated

---

### 🔍 Customer Product Search

A reverse lookup tool that allows users to **input a part number** and retrieve its full attribute breakdown.

**Key Features**

* Series detection from code prefix
* Attribute decoding via a shared position map
* Tolerance for partial or fuzzy input
* Rule-based constraint interpretation
* Output of full product specification summary

**Example user flow**

1. Enter the existing part number
2. The system identifies the series and retrieves attribute positions
3. Attributes are decoded and displayed with details
4. Optional validation or compatibility notes are shown

---

## 🧱 System Architecture

```
                                 ┌────────────────────────────────┐
                                 │         Streamlit UI           │
                                 │ Tabs: Part Number / Customer   │
                                 └───────────────┬────────────────┘
                                                 │
 ┌───────────────────────────────────────────────┼───────────────────────────────────────────────┐
 │                                               │                                               │
 ▼                                               ▼                                               ▼
┌──────────────────────┐               ┌──────────────────────────┐                ┌──────────────────────────┐
│  Series Hunter       │               │  Part Number Generator   │                │  Customer Product Search │
│  (needs → candidate  │               │ - ordered attributes     │                │ - parse part-number      │
│   series)            │               │ - dependency filtering   │                │ - detect series prefix   │
│                      │               │ - incompatibility checks │                │ - decode attributes      │
│  - fuzzy matching    │               │ - live validation        │                │ - consistency checks     │
│  - constraint hints  │               │ - optional image preview │                │ - constraint hints       │
└───────────┬──────────┘               └───────────┬──────────────┘                └───────────┬──────────────┘
            │                                          │                                          │
            ▼                                          ▼                                          ▼
      ┌───────────────┐                        ┌────────────────┐                         ┌────────────────┐
      │ Candidate     │                        │ Final Part#    │                         │ Decoded series │
      │ Series list   │                        │+ config summary│                         │ + full spec    │
      └───────────────┘                        └────────────────┘                         └────────────────┘


              ┌────────────────────────── Shared Data & Logic ──────────────────────────┐
              │ • Attribute dictionary (per series, ordered sequence)                   │
              │ • Code schema / positional mapping (for encoding & decoding)            │
              │ • Constraint rules (Include/Exclude/Condition_on attribute/value)       │
              │ • Product & attribute images                                            │
              └─────────────────────────────────────────────────────────────────────────┘
```

---

## 🧠 Core Architecture

Both tools share the same underlying dataset and logic engine:

| Layer                          | Description                                                      |
| ------------------------------ | ---------------------------------------------------------------- |
| **Streamlit UI**               | Two main tabs for the generator and search tools                 |
| **Attribute Dictionary**       | Defines the ordered sequence of attributes for each series       |
| **Constraint Rules**           | Include / Exclude / Conditional relationships between attributes |
| **Code Schema & Position Map** | Rules to encode or decode part numbers                           |
| **Shared Assets**              | Attribute labels, product metadata, and optional images          |

This structure ensures **consistency** between generation and decoding, and allows future extension to new product families or rule sets.

---

## ⚙️ Technical Stack

* **Language:** Python
* **Framework:** Streamlit
* **Data Source:** Structured CSV / attribute mapping tables
* **Logic Engine:** Custom rule validator and encoding–decoding parser
* **UI Features:** Tooltips, dynamic dropdowns, contextual feedback messages

---

## 📈 Project Goals

* Streamline product configuration for internal or customer use
* Reduce manual errors in part number creation
* Enable transparent reverse lookup and product verification
* Provide a foundation for future smart configurator or chatbot integration

---

## 🧩 Module Summary

| Module                       | Purpose                                     | Input                    | Output                           |
| ---------------------------- | ------------------------------------------- | ------------------------ | -------------------------------- |
| **Part Number Generator**    | Build a valid configuration and part number | User-selected attributes | Generated part code + summary    |
| **Customer Product Search**  | Decode and explain an existing code         | Part number              | Attribute breakdown + validation |
| **Series Hunter (optional)** | Suggest relevant series based on needs      | Text input / specs       | Candidate series list            |

---

## 🚀 Future Extensions

* Multi-family support (e.g., switches, connectors, LEDs)
* Integration with a backend database for live data
* Export of results in JSON or CSV format
* User login and saved configurations
* Chat assistant interface for guided configuration

---

## 🔒 Privacy Note

This repository **does not include** proprietary datasets, rule files, or UI screenshots to ensure confidentiality and compliance with internal data policy. All descriptions here represent **functional logic only**.

---

## 🧑‍💻 Author

Weilun LIN
