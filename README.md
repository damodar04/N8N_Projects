# 📄 Automated Invoice Extraction with n8n, LlamaParse & DeepSeek

This repository contains an **end-to-end automated invoice processing workflow** built using **n8n**, **LlamaParse (LlamaIndex Cloud)**, and **DeepSeek LLMs**.

The system automatically reads invoice emails, extracts PDF attachments, parses complex invoice layouts, converts unstructured data into a structured schema, and stores the results in Google Sheets — all without manual intervention.

---

## 🔍 Problem Statement

Traditional PDF-to-text solutions fail when invoices contain:
* **Tables and multi-line items**
* **Complex layouts**
* **Scanned documents**
* **Inconsistent formatting**

This project solves these challenges using **cloud-grade document parsing** and **LLM-driven structured extraction**.

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
Architecture OverviewGmail Trigger: Listens for incoming emails with PDF attachments.Validation Layer: Filters valid PDFs and prevents duplicates via labels.Document Parsing (LlamaParse): Converts complex PDFs (tables, layouts) into Markdown via LlamaIndex Cloud.LLM Extraction (DeepSeek): Uses schema-constrained extraction to turn Markdown into JSON.Persistence Layer: Writes structured data into Google Sheets.Idempotency Control: Marks the email as "synced" to prevent re-processing.✨ Key Features✅ Fully automated invoice ingestion.✅ Supports scanned and digital PDFs.✅ Accurate extraction of tables and line items.✅ Schema-validated structured output.✅ Google Sheets integration.✅ DeepSeek V3/Chat integration (OpenAI-compatible).🛠 Technology StackLayerToolWorkflow Automationn8nEmail IngestionGmail TriggerDocument ParsingLlamaParseLLM EngineDeepSeek ChatOutput ValidationLangChain Structured Output ParserData StorageGoogle Sheets📦 Extracted Invoice FieldsThe workflow extracts and validates the following fields:Header Info: Invoice date, number, and PO number.Entities: Supplier & Customer names, addresses, and VAT IDs.Items: Line item descriptions, unit prices, and discounts.Totals: Subtotal (excl. VAT), VAT amount, and Grand Total.🚀 Getting Started1️⃣ Prerequisitesn8n (Cloud or Self-Hosted)Gmail & Google Sheets API accessLlamaIndex Cloud API KeyDeepSeek API Key2️⃣ Import WorkflowOpen n8n.Navigate to Workflows -> Import from File.Select n8n-invoice-extraction-workflow.sanitized.json.3️⃣ Configure CredentialsGmail OAuth2: Required for reading and labeling emails.Google Sheets OAuth2: Required for data persistence.DeepSeek LLM:Base URL: https://api.deepseek.com/v1Model: deepseek-chatLlamaParse: Set Header Authorization: Bearer <YOUR_API_KEY>.🔐 Security & Best PracticesCredential Management: Never hardcode API keys. Use n8n's built-in credential manager.Labeling: Ensure you create a Gmail label named invoice synced before starting the workflow.Scaling: For high volumes, consider adjusting the LlamaParse polling interval.👨‍💻 AuthorDamodar Bhawsar
