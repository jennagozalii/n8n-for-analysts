# 03 – Customer Complaint Intake with Escalation

When complaints land in a shared inbox, urgent ones can sit unread for days. This workflow gives every complaint a ticket number, logs it, and sends urgent ones to the team straight away.

**What it does:** a customer fills in an n8n form. The workflow creates a ticket number, saves the complaint to Google Sheets, and if the urgency is High or the category is Agent conduct, posts an alert to a Slack channel. Everything else is logged without alerting anyone.

**Nodes used:** n8n Form Trigger → Edit Fields → Google Sheets → IF → Slack

▶️ **Watch the tutorial:** [YouTube](VIDEO-3-LINK)

## Setup
1. Import `03-complaint-intake.json` into n8n.
2. Create a Google Sheet with these headers in row 1:
   `ticket_id`, `received_at`, `name`, `email`, `policy_no`, `category`, `urgency`, `details`, `status`
3. In the Google Sheets node, connect your Google account and choose your sheet.
4. In Slack, create a channel (for example `#complaints-urgent`). In the Slack node, connect your account and choose that channel.
5. Click **Execute workflow**, fill in the test form, and check the sheet and Slack.

## Escalation rule
A complaint is sent to Slack if **either** of these is true:
- Urgency is **High**
- Category is **Agent conduct**

You can change the rule in the IF node to match your own team's process.

## Tip
The Edit Fields node uses `.trim()` on the category and urgency answers. It removes any hidden spaces, so the IF rule always matches correctly.
