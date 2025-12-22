#  Automated Invoice Extraction with n8n, LlamaParse & DeepSeek

This repository contains an **end-to-end automated invoice processing workflow** built using **n8n**, **LlamaParse (LlamaIndex Cloud)**, and **DeepSeek LLMs**.

The system automatically reads invoice emails, extracts PDF attachments, parses complex invoice layouts, converts unstructured data into a structured schema, and stores the results in Google Sheets — all without manual intervention.

---

## Problem Statement

Invoices often fail with traditional PDF/OCR tools due to:

Complex tables and multi-line items
Scanned or image-based PDFs
Inconsistent vendor formats
Manual data entry is slow, error-prone, and not scalable.

This project solves these challenges using **cloud-grade document parsing** and **LLM-driven structured extraction**.

---

## Solution Overview

The workflow follows these automated steps:
1. **Listens** for invoice emails in Gmail.
2. **Validates** and extracts PDF attachments.
3. **Uses LlamaParse** to convert PDFs (even tables) into structured Markdown.
4. **Applies DeepSeek LLM** with schema constraints for extraction.
5. **Writes** structured invoice data into Google Sheets.
6. **Labels** processed emails to prevent duplication.

---

## Architecture Diagram
```mermaid
flowchart LR
    A[Gmail Trigger] --> B[PDF Filter]
    B --> C[LlamaParse Upload]
    C --> D[Job Status Polling]
    D -->|SUCCESS| E[PDF → Markdown]
    E --> F[DeepSeek LLM]
    F --> G[Schema Validation]
    G --> H[Google Sheets]
    H --> I[Gmail Label: synced]
```

---

## Key Features

-  **Fully Automated**: No manual data entry required.
-  **High Accuracy**: Supports scanned and digital PDFs with complex tables.
-  **Structured Output**: Guaranteed JSON format for database/sheet integration.
-  **Cost-Effective**: Uses DeepSeek V3 for high-performance, low-cost extraction.
-  **Production Ready**: Includes duplicate prevention and error handling.

---

## Technology Stack

| Layer | Tool |
|-------|------|
| Workflow Automation | n8n |
| Email Ingestion | Gmail Trigger |
| Document Parsing | LlamaParse |
| LLM Engine | DeepSeek Chat (V3/R1) |
| Data Storage | Google Sheets |

---

## Extracted Invoice Fields

The workflow extracts the following information automatically:

- **Header Info**: Invoice date, Invoice number, PO number.
- **Vendor & Client**: Names, addresses, and VAT/Tax IDs.
- **Line Items**: Descriptions, quantities, unit prices, and discounts.
- **Financials**: Subtotal without VAT, Total VAT, and Grand Total.

---

## Getting Started

### Prerequisites

- n8n (Cloud or Self-Hosted).
- Gmail & Google Sheets accounts.
- LlamaIndex Cloud API Key.
- DeepSeek API Key.

### 2️Import Workflow

1. Open your n8n instance.
2. Go to **Workflows** → **Import from File**.
3. Upload: `n8n-invoice-extraction-workflow.sanitized.json`.

### 3️Configure Credentials

- **Gmail/Sheets**: Connect via OAuth2.
- **DeepSeek**: Set Base URL to `https://api.deepseek.com/v1`.
- **LlamaParse**: Add header `Authorization: Bearer <YOUR_API_KEY>`.

### 4️Gmail Label Setup

Create a label in your Gmail account named: **`invoice synced`**. This is used to flag emails that have already been processed.

---

##  Security Best Practices

- **Environment Variables**: Use n8n credentials for all API keys.
- **Data Privacy**: Be mindful of PII (Personally Identifiable Information) in invoices when using cloud LLMs.

---

##  Author

**Damodar Bhawsar**

---

##  License

This project is open source and available under the [MIT License](LICENSE).

---


---

## ⭐ Show Your Support

Give a ⭐️ if this project helped you!
