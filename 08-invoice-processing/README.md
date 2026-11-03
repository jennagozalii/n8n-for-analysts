# 08 – AI Invoice Processing with Manager Approval

In many finance teams, someone opens every invoice PDF, types the details into a spreadsheet, and then chases a manager to approve the large ones. This workflow automates the whole process, with a manager still making the final call on big amounts.

**What it does:**
1. Watches an inbox for emails with "invoice" in the subject and a PDF attached.
2. Reads the PDF and uses a Gemini model to pull out the vendor, invoice number, invoice date, due date, total, currency and a short description.
3. Invoices up to RM 5,000 are approved automatically. Anything above that is sent to a manager in Slack with **Approve** and **Decline** buttons, and the workflow waits for their decision.
4. Every invoice is saved to an Invoice Register in Google Sheets, with the decision.

**Nodes used:** Gmail Trigger → Extract from File → Information Extractor (with Google Gemini Chat Model) → IF → Slack (Send and Wait for Response) → Edit Fields → Google Sheets

▶️ **Watch the tutorial:** [YouTube](VIDEO-8-LINK)

## Sample invoices
| File | Vendor | Total | Expected result |
|---|---|---|---|
| `invoice-1.pdf` | Bright Office Supplies Sdn Bhd | RM 1,280.00 | Auto-approved |
| `invoice-2.pdf` | KL Cloud Hosting Sdn Bhd | RM 18,600.00 | Sent to Slack for approval |
| `invoice-3.pdf` | Seri Catering | RM 3,400.00 | Auto-approved |

All companies and invoices are made up for this demo.

## Setup
1. Use a **separate test Gmail account**.
2. Create a Google Sheet called **Invoice Register** with these headers in row 1:
   `received_at`, `vendor_name`, `invoice_number`, `invoice_date`, `due_date`, `total_amount`, `currency`, `description`, `approval`, `sender`
3. Create a Slack channel for approvals (for example `#approvals`).
4. Get a free Gemini API key from Google AI Studio (aistudio.google.com → Get API key).
5. Import `08-invoice-processing.json` into n8n and connect your accounts:
   - Gmail Trigger: your test Gmail account. Keep **Download Attachments** on.
   - Google Gemini Chat Model: your API key.
   - Slack: for the Approve/Decline buttons to work, use a Slack app credential with an access token **and** the app's Signing Secret.
   - Google Sheets: your account and the Invoice Register sheet.
6. **Publish** the workflow, then email the three sample PDFs to your test account, each with "Invoice" in the subject.

## What I'd add before using it for real
- A **duplicate check**: look up the invoice number in the register first, so the same invoice is never paid twice.
- A **check for unclear invoices**: if the AI can't find a total, send it to a person instead of guessing.
- A **monthly spend summary** by vendor, using the approach from project 07.
