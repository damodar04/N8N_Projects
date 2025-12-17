flowchart LR
    A[Gmail Trigger<br/>Invoice Email] --> B[PDF Attachment Filter]
    B --> C[LlamaParse Upload]
    C --> D[LlamaParse Job Status Polling]
    D -->|SUCCESS| E[PDF → Markdown]
    E --> F[DeepSeek LLM<br/>Structured Extraction]
    F --> G[Schema Validation<br/>Structured Output Parser]
    G --> H[Google Sheets<br/>Append Rows]
    H --> I[Gmail Label<br/>invoice synced]
