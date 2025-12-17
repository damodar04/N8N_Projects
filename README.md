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
