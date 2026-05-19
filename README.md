# Telecom-Bill-to-Odoo-Approvals-Automator-n8n-Workflow-
An enterprise cost-control automation workflow built in n8n that parses telecommunication billing items (e.g., corporate phone bills), loops through individual line expenses, and automatically generates **Approval Requests** inside Odoo ERP for financial clearance.
## 🎯 Problem Solved
Processing corporate telecom bills manually is a tedious, error-prone auditing chore. Accounts payable teams usually have to break down large master invoices, match each phone number to its corresponding department/product code, and manually create expense approval forms.

This workflow fully automates the auditing and loading stages:
1. **Data Ingestion:** Extracts individual corporate phone numbers and their respective monthly bill amounts.
2. **ERP Product Lookup:** Dynamically queries Odoo to search for the specific service product corresponding to each corporate phone line.
3. **Automated Auditing & Routing:** If a line matches, it computes the data and creates a structured **Odoo Approval Request** (`approval.request`) with pre-set routing tags for managers to review instantly.

---

## ⚡ Workflow Architecture
[ Ingest Billing Data (JSON/Array) ]
↓
[ Loop Through Each Line ]
↓
[ Query Odoo: Search Product by Phone ]
↓
🚦 Product Located?
├── Yes → [ Create Odoo Approval Request ] → Save ID & Loop Next
└── No  → Log Warning & Loop Next
↓
[ Compile & Post Final Run Summary ]


---

## 🔧 Tech Stack
| Tool | Role |
| :--- | :--- |
| **n8n** | Processing orchestration, complex sub-item looping, and logic gates |
| **Odoo ERP API** | Target operational ledger (`approval.request` & `product.product`) |
| **JavaScript (Code Node)** | Object grouping, initial billing array injection, and data formatting |

---

## 📋 Key Features & Safeguards
* **🔄 Advanced Looping Architecture:** Uses an optimal looping framework to securely step through multiple phone lines one by one without hitting API timeout bottlenecks.
* **🔎 Dynamic Product Matching:** Uses exact string fields to cross-examine phone numbers against internal product codes or barcodes in Odoo.
* **📊 Run Analytics:** Concludes executions with a **Final Summary** compiler to log successful ingestions versus missing infrastructure associations.

---

## 🚀 Setup Instructions

### Prerequisites
* n8n instance (Self-hosted or Cloud).
* Odoo ERP Instance with the **Approvals Module** installed active.
* Standard permissions to read products and execute approval requests inside Odoo.

### Steps to Deploy
1.  **Import:** Download and import `Telecom_Bill_to_Odoo_Approvals.json` into your n8n workspace.
2.  **Bill Input Setup:** Replace the hardcoded mock array in the initial JavaScript node with your dynamic input source (e.g., an Email PDF parser, an Excel Reader, or an API call from your telecom provider).
3.  **Connect Odoo Instance:** Enter your target Odoo URL, DB name, username, and secure API Key.
4.  **Field Validation:** Ensure the product lookup search key aligns with the custom field where you save corporate numbers inside your Odoo catalog (e.g., `default_code`).
5.  **Activate:** Trigger the pipeline once or configure a monthly trigger to run automatically the day your bill releases.

---

## 📁 Repository Structure
```bash
telecom-bill-odoo-approvals/
├── Telecom_Bill_to_Odoo_Approvals.json # The clean n8n auditing workflow file (Import this)
├── approvals-pipeline-canvas.png        # Visual screenshot of the automated looping structure
└── README.md                            # Project documentation
👤 Author
Asem Ahmed — AI Automation Engineer
