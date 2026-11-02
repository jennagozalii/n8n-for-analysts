# 04 – AI Inbox Triage

Support teams often spend the first hour of the day just sorting emails. This workflow does the sorting automatically.

**What it does:** when a new email arrives, a Gemini model reads the subject and body and puts it into one of five categories: Claims, Billing, Policy Change, Complaint or Other. n8n then adds the matching Gmail label. Complaints also send an alert to a Slack channel, so a manager sees them within a minute.

**Nodes used:** Gmail Trigger → Text Classifier (with Google Gemini Chat Model) → Gmail (Add Label) → Slack

▶️ **Watch the tutorial:** [YouTube](https://youtu.be/gLLuvihQBC4)

## Setup
1. Use a **separate test Gmail account**. Please don't connect this to a real inbox until you've tested it.
2. In that Gmail, create 5 labels: `Claims`, `Billing`, `Policy Change`, `Complaint`, `Other`.
3. Get a free Gemini API key from Google AI Studio (aistudio.google.com → Get API key).
4. Import `04-ai-inbox-triage.json` into n8n.
5. Connect your test Gmail account in the Gmail Trigger and the Gmail label nodes.
6. Add your Gemini API key in the Google Gemini Chat Model node.
7. In the Slack node, connect your account and choose a channel.
8. Activate the workflow and send yourself the emails in `test-emails.md`.

## Tips
- The category **descriptions** matter more than the names. The AI uses them to decide, so make them specific to your business.
- Keep the **Other** category, so the AI has a safe option when it isn't sure.
- Before using this on real emails, log every decision to a sheet for a few weeks and check the accuracy.
