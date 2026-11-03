# 05 – Clean and Flag Insurance Claims Data

Data exports are rarely clean. Dates come in different formats, amounts are stored as text with "RM" and commas, and some rows appear twice. This workflow cleans the data automatically and flags the claims a claims or fraud team should review.

**What it does:** reads a messy claims sheet, standardises dates, amounts and claim types, finds duplicates, and checks every claim against four rules. Clean claims go to one tab, flagged claims go to another, each with a plain-English reason.

**Nodes used:** Manual Trigger → Google Sheets → Code (JavaScript) → IF → Google Sheets (×2)

▶️ **Watch the tutorial:** [YouTube](VIDEO-5-LINK)

## Flag rules
A claim is flagged if any of these are true:
- Duplicate claim ID
- Invalid claim date (for example, 32/10/2026)
- Amount above RM 20,000
- Claim made within 30 days of the policy start date

The thresholds are examples. In a real company, they would come from the claims or fraud team.

## Setup
1. Create a Google Sheet with three tabs: `Claims Raw`, `Claims Clean` and `Claims Flagged`.
2. Import `claims_raw.csv` into **Claims Raw** (File → Import → Upload). Untick "Convert text to numbers, dates, and formulas" so the messy values stay as they are.
3. In **Claims Clean** and **Claims Flagged**, add these headers in row 1:
   `claim_id`, `policy_no`, `claim_type`, `claim_date`, `policy_start`, `amount_myr`, `days_since_start`, `flagged`, `flag_reasons`
4. Import `05-claims-cleaning.json` into n8n and connect your Google account in the three Google Sheets nodes.
5. Click **Execute workflow**. You should get 3 clean claims and 4 flagged claims.

## Tip
To run this every night instead of by hand, replace the Manual Trigger with a Schedule Trigger. Clear the output tabs before each test run, because the workflow adds rows rather than replacing them.
