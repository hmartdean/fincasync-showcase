# 🏢 FincaSync — Multimodal Ingestion & Rule-Based Accounting Reconciliation

[![Python 3.11+](https://img.shields.io/badge/Python-3.11+-3776AB.svg?logo=python&logoColor=white)](https://www.python.org/)
[![UI Framework](https://img.shields.io/badge/UI-Streamlit-FF4B4B.svg?logo=streamlit&logoColor=white)](https://streamlit.io/)
[![LLM Engine](https://img.shields.io/badge/Extraction-Gemini_2.5_Flash-4285F4.svg?logo=google&logoColor=white)](https://ai.google.dev/)
[![Status: Engineering Showcase](https://img.shields.io/badge/Status-Engineering%20Showcase-blue.svg)]()

> **Notice:** This repository is an engineering showcase and functional MVP demonstrating the reactive UI architecture, LLM extraction integration, and rule-based verification flow. Production datasets, fine-tuned configurations, and proprietary client business logic are excluded.

---

## 📌 Overview

**FincaSync** is an automated pipeline designed to reduce manual data entry for property management firms handling utility invoices (electricity, gas, and water). 

Because generative language models are inherently probabilistic, the system pairs **multimodal structured extraction** with an **explicit Python validation layer**. Ambiguous records, unassigned supply points, or arithmetical anomalies are routed to a human review queue before records are consolidated and exported.


---

## 🎥 Interface & Pipeline Walkthrough

https://github.com/user-attachments/assets/ab6aaae1-22b6-4750-aea6-11ca76574119

---

## 🔁 Architectural Workflow

```text
[ Inbound PDF Invoices ]
           │
           ▼
[ Batch Ingestion Pipeline ]
           │
           ├─► [ Gemini 2.5 Flash API ]
           │        Structured field extraction (CUPS, Vendor, Base, VAT, Total)
           │
           ├─► [ Deterministic Validation Layer ]
           │        • Supply point matching (CUPS catalog check)
           │        • Basic arithmetic consistency checks (Base + VAT vs. Total)
           │
           ▼
[ Status Classification ]
     ├── Status: CONCILIADO (Validation checks pass)
     └── Status: REVISIÓN   (Unmatched supply points or arithmetic variances)
           │
           ▼
[ Streamlit Interface ] ──► Manual review & in-memory Excel (.xlsx) export

```

---

## ⚡ Engineering Approach

1. **Multimodal Extraction Pipeline:**
Uses Gemini 2.5 Flash to parse utility invoices into structured formats, extracting vendor identities, supply point identifiers (Spanish CUPS), taxable bases, VAT rates, and total amounts across variable document layouts.
2. **Deterministic Rules & Verification:**
The system does not treat LLM outputs as ground truth:
* **Supply Point Validation:** Cross-references extracted CUPS codes against pre-configured property registry data to detect unassigned supplies.
* **Arithmetic Consistency Checks:** Validates basic balance integrity ($\text{Base} + \text{VAT} \approx \text{Total}$) where standard tax breakdowns apply, flagging edge cases (such as surcharges, meter rentals, or adjustments) for manual oversight.

3. **Human-in-the-Loop Workflow:**
Documents with missing identifiers, unmapped accounts, or tax discrepancies are flagged as **`REVISIÓN`** for manual triage, preventing unvalidated inputs from entering financial workflows.
4. **Single-Stack Reactive UI (Streamlit):**
Built entirely in Python using Streamlit UI Layer, coupling asynchronous batch processing events directly with a reactive dashboard via WebSockets.
5. **In-Memory Structured Export:**
Generates audit-ready `.xlsx` spreadsheets on demand using `openpyxl` streams directly into binary buffers for download without unnecessary disk overhead.

---

## 🔒 Source Code & Commercial Availability

This repository is maintained as an **Engineering Showcase and Architecture Portfolio**. 

The underlying pipeline scripts, proprietary heuristic weights, client database models, and production integration layers remain private. A deep-dive walkthrough or demonstration of the complete codebase is available upon request during technical interview processes.

---

## 👤 Engineering Contact

**H. Martin Dean**

* **LinkedIn:** [linkedin.com/in/hmartdean](https://www.linkedin.com/in/hmartdean/?isSelfProfile=true)
* **Email:** [hmartdean@gmail.com](mailto:hmartdean@gmail.com)

```
