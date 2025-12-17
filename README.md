# 📄 Automated Invoice Extraction with n8n, LlamaParse & DeepSeek

This repository contains an **end-to-end automated invoice processing workflow** built using **n8n**, **LlamaParse (LlamaIndex Cloud)**, and **DeepSeek LLMs**.

The system automatically reads invoice emails, extracts PDF attachments, parses complex invoice layouts, converts unstructured data into a structured schema, and stores the results in Google Sheets — all without manual intervention.

---

## 🔍 Problem Statement

Traditional PDF-to-text solutions fail when invoices contain:
- Tables and multi-line items
- Complex layouts
- Scanned documents
- Inconsistent formatting

This project solves these challenges using **cloud-grade document parsing** and **LLM-driven structured extraction**.

---

## 🧠 Solution Overview

The workflow:
1. Listens for invoice emails in Gmail
2. Validates and extracts PDF attachments
3. Uses LlamaParse to convert PDFs into structured Markdown
4. Applies DeepSeek LLM with schema constraints
5. Writes structured invoice data into Google Sheets
6. Labels processed emails to prevent duplication

---

## 🏗 Architecture Diagram

```mermaid
flowchart LR
    A[Gmail Trigger<br/>Invoice Email] --> B[PDF Attachment Filter]
    B --> C[LlamaParse Upload]
    C --> D[Job Status Polling]
    D -->|SUCCESS| E[PDF → Markdown]
    E --> F[DeepSeek LLM<br/>Structured Extraction]
    F --> G[Schema Validation<br/>Structured Output Parser]
    G --> H[Google Sheets<br/>Append Rows]
    H --> I[Gmail Label<br/>invoice synced]

### Architecture Overview

The workflow follows an event-driven, asynchronous architecture:

1. **Gmail Trigger**
   - Listens for incoming emails with PDF attachments.

2. **Validation Layer**
   - Filters only valid PDF invoices.
   - Prevents duplicate processing using Gmail labels.

3. **Document Parsing (LlamaParse)**
   - Uploads invoice PDFs to LlamaIndex Cloud.
   - Converts complex PDFs (tables, layouts) into Markdown.

4. **LLM Extraction (DeepSeek)**
   - Uses an OpenAI-compatible DeepSeek chat model.
   - Applies schema-constrained extraction via Structured Output Parser.

5. **Persistence Layer**
   - Writes structured invoice data into Google Sheets.
   - One row per invoice or per line item.

6. **Idempotency Control**
   - Adds a Gmail label after successful processing.

✨ Key Features

✅ Fully automated invoice ingestion

✅ Supports scanned and digital PDFs

✅ Accurate extraction of tables and line items

✅ Schema-validated structured output

✅ Google Sheets integration

✅ Duplicate processing prevention

✅ OpenAI-compatible DeepSeek integration

✅ Production-ready n8n workflow

🛠 Technology Stack
Layer	Tool
Workflow Automation	n8n
Email Ingestion	Gmail Trigger
Document Parsing	LlamaParse (LlamaIndex Cloud)
LLM Engine	DeepSeek Chat
Output Validation	LangChain Structured Output Parser
Data Storage	Google Sheets
📦 Extracted Invoice Fields

The workflow extracts the following information:

Invoice date

Invoice number

Purchase order number

Supplier name

Supplier address

Supplier VAT identification number

Customer name

Customer address

Customer VAT identification number

Shipping addresses

Line items (description, price, discount)

Subtotal without VAT

Subtotal with VAT

Total price

All extracted data is validated against a predefined JSON schema.

🚀 Getting Started
1️⃣ Prerequisites

n8n (Cloud or Self-Hosted)

Gmail account

Google Sheets account

LlamaIndex Cloud account

DeepSeek API key

2️⃣ Import Workflow

Open n8n

Navigate to Workflows → Import

Upload the file:

n8n-invoice-extraction-workflow.sanitized.json

3️⃣ Configure Credentials in n8n

Create the following credentials:

📧 Gmail OAuth2

Used for:

Reading incoming invoice emails

Adding labels after processing

📊 Google Sheets OAuth2

Used for:

Writing structured invoice data

📄 LlamaParse (HTTP Request)

Add the following header manually:

Authorization: Bearer <LLAMA_CLOUD_API_KEY>

🧠 DeepSeek LLM

Base URL:

https://api.deepseek.com/v1


Model:

deepseek-chat

🏷 Gmail Label Setup

Create a Gmail label named:

invoice synced


This label is applied after successful processing to avoid duplicate ingestion.

📊 Google Sheets Output

Each invoice is stored as structured rows in Google Sheets.

Recommended Columns

invoice_number

invoice_date

supplier_name

customer_name

line_item_description

price_without_vat

price_with_vat

total_price

🔁 Handling Multiple Line Items

Invoices containing multiple line items can be:

Written as multiple rows (one per line item)

Or aggregated per invoice depending on business needs

This can be customized easily in n8n.

🔐 Security Best Practices

❌ Never commit API keys to GitHub

✔ Use n8n credentials or environment variables

✔ Rotate keys if exposed accidentally

🧩 Customization & Extensions

This workflow can be extended to:

Push data into ERP systems (SAP, Tally, QuickBooks)

Validate invoices against purchase orders

Perform anomaly or fraud detection

Store PDFs in cloud storage

Integrate with accounting systems

📚 References

n8n Documentation: https://docs.n8n.io

LlamaIndex Cloud: https://cloud.llamaindex.ai

DeepSeek API: https://platform.deepseek.com

👨‍💻 Author

Damodar Bhawsar
