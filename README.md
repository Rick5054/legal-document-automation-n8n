# Automated Legal Document Summary Workflow (n8n)

Research-driven automation workflow that ingests legal documents from email, extracts structured insights using LLMs, and distributes results via Google Sheets and email.

---

## 🔍 Overview
This project implements an **end-to-end document intelligence pipeline** using **n8n**.  
It automatically processes incoming legal documents (complaints, contracts, filings), extracts structured summaries and key risk points using an LLM, and stores the results for operational and analytical use.

The workflow is designed to be:
- reproducible
- auditable
- production-oriented
- easily extensible

---

## ⚙️ Workflow Diagram
<p align="center">
  <img src="workflow/workflow-diagram.png" alt="n8n Workflow Diagram" width="90%">
</p>

---

## 🧠 What the workflow does (step-by-step)

1. **Gmail Trigger**
   - Monitors inbox for emails with attachments
   - Filters by keywords (Complaint, Contract, Filename)

2. **Google Drive Upload**
   - Saves attachments to a structured Drive folder
   - Maintains document traceability

3. **Document Download**
   - Fetches stored file for processing

4. **PDF Text Extraction**
   - Extracts raw text from legal PDFs

5. **LLM Processing (OpenAI via n8n)**
   - Generates:
     - concise factual summary (~200 words)
     - top 5 legal risk/issues
     - computed procedural deadline
     - structured JSON output (schema-enforced)

6. **Google Sheets Logging**
   - Appends structured results into a tracking sheet
   - Enables downstream analytics and dashboards

7. **Email Notification**
   - Sends internal summary email with key findings

---

## 📦 Output Schema (LLM)

The model returns a **strict JSON object**:

```json
{
  "RawID": "string",
  "DateReceived": "YYYY-MM-DD",
  "Summary": "string",
  "KeyIssues": ["Issue1","Issue2","Issue3","Issue4","Issue5"],
  "Deadline": "YYYY-MM-DD",
  "DeadlineAssumption": "string",
  "EmailSubject": "string",
  "SummaryEmail": "HTML string"
}
