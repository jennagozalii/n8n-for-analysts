# 02 – Daily KPI Report by Email

In many teams, someone builds the daily numbers email by hand every morning. This workflow builds and sends it automatically.

**What it does:** every weekday at 8:30 a.m., it reads a sales sheet, finds the latest day, totals premium and policies by channel, works out the percentage of target, and emails managers a formatted HTML report. Channels below 80% of target are highlighted in red.

**Nodes used:** Schedule Trigger → Google Sheets → Code (JavaScript) → Gmail

▶️ **Watch the tutorial:** [YouTube](https://youtu.be/8idacZnWaAo?si=QWfHtzJxLbe0Tiq7)

## Setup
1. Import `02-kpi-email.json` into n8n.
2. Create a Google Sheet and import `daily_policy_sales.csv` (File → Import → Upload). Untick "Convert text to numbers, dates, and formulas" so the dates stay as text.
3. In the Google Sheets node, connect your Google account and choose your sheet.
4. In the Gmail node, connect your account and change the **To** address from `you@example.com` to your own.
5. Run it once with **Execute workflow** and check your inbox.

## Sample data
`daily_policy_sales.csv` has made-up daily sales for four channels: Agency, Bancassurance, Digital and Broker.
