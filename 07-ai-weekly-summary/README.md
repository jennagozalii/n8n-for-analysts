# 07 – AI Weekly Analytics Summary

Sending numbers is easy. Explaining what they mean is what takes time every Monday. This workflow calculates the weekly results in code, then has an AI model write a short summary email for managers.

**What it does:** every Monday at 8:00 a.m., it reads daily sales data, compares this week with last week for each channel, and works out the percentage change and percentage of target. A Gemini model then writes a headline, up to three findings and one suggested action, using only those numbers, and the result is sent as an HTML email.

**Nodes used:** Schedule Trigger → Google Sheets → Code (JavaScript) → Basic LLM Chain (with Google Gemini Chat Model) → Gmail

▶️ **Watch the tutorial:** [YouTube](VIDEO-7-LINK)

## Why code does the maths
Language models can make arithmetic mistakes, and one wrong number in a report is enough to lose a manager's trust. So every figure is calculated in the Code node first. The AI only receives the final results, and the prompt tells it not to calculate or invent anything.

## Expected numbers (sample data)
| Channel | This week (RM) | Last week (RM) | Change | % of target |
|---|---|---|---|---|
| Agency | 121,500 | 117,000 | +3.8% | 101.3% |
| Bancassurance | 114,000 | 94,500 | +20.6% | 103.6% |
| Digital | 61,000 | 47,500 | +28.4% | 122.0% |
| Broker | 84,000 | 108,000 | −22.2% | 84.0% |

Use this table to check the AI's email against the real figures.

## Setup
1. Create a Google Sheet and import `daily_policy_sales_2weeks.csv` (File → Import → Upload). Untick "Convert text to numbers, dates, and formulas" so the dates stay as text.
2. Get a free Gemini API key from Google AI Studio (aistudio.google.com → Get API key).
3. Import `07-ai-weekly-summary.json` into n8n.
4. Connect your Google account in the Google Sheets and Gmail nodes, and your Gemini key in the chat model node.
5. In the Gmail node, change the **To** address from `you@example.com` to your own.
6. Click **Execute workflow** and compare the email with the table above.

## Tip
Send the email only to yourself for the first few weeks. Check the numbers and wording, and only send it to managers once you trust it. The AI writes the first draft; the analyst still owns the conclusion.
