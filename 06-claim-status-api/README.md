# 06 – Internal API with Webhooks and Error Alerts

Analysts often get the same question again and again: "Can you check the status of this claim?" This project turns that question into a small, secure API that any team or system can call. It also adds an alert workflow, so I hear about failures before anyone else does.

**What it does:**
- **Claim Status API:** a webhook link that takes a claim ID, looks it up in Google Sheets, and returns the claim's type, amount and status as JSON. Unknown claims return a 404 "Claim not found". The link is protected with a secret key sent in a header.
- **Error Alerts:** a separate workflow that runs whenever another workflow fails, and posts the workflow name, the failed node, the error message and a link to the run in Slack.

**Nodes used:**
- API: Webhook (Header Auth) → Google Sheets → IF → Respond to Webhook (×2)
- Alerts: Error Trigger → Slack

▶️ **Watch the tutorial:** [YouTube](VIDEO-6-LINK)

## Setup
1. Use the **Claims Clean** tab from project 05, and add a `status` column (for example Approved, In review, Paid).
2. Import both `06-claim-status-api.json` and `00-error-alerts.json` into n8n.
3. In the API workflow:
   - Webhook node: create a **Header Auth** credential with Name `X-API-Key` and a long random value as your secret key.
   - Google Sheets node: connect your account. Set the sheet **By Name** to `Claims Clean`.
4. In the error workflow: connect Slack and choose a channel (for example `#n8n-alerts`), then save.
5. In the API workflow, go to **⋯ → Settings → Error Workflow** and choose the error alerts workflow.
6. **Publish** the API workflow. Changes only go live after you publish.

## Try it
Replace the address and key with your own:

    curl -H "X-API-Key: YOUR_SECRET_KEY" "https://YOUR-N8N-ADDRESS/webhook/claim-status?claim_id=CL-1001"

Example response:

    {
      "claim_id": "CL-1001",
      "claim_type": "Hospital",
      "amount_myr": 1200,
      "status": "Approved"
    }

Without the key, the API returns "Authorization data is wrong".

## Tips
- Never put a real key in a screenshot or video. In Windows Command Prompt, save it first with `set KEY=...` and use `%KEY%` in the command.
- Error workflows only run for live (production) calls, not for test runs in the editor.
- Set the same error workflow on all your other workflows, so every failure reaches you.
