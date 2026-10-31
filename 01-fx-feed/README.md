# 01 – Daily FX Rates Feed

Finance teams often copy exchange rates into a spreadsheet by hand every morning. This workflow does it automatically.

**What it does:** every day at 8:00 a.m. (Kuala Lumpur time), it gets the latest USD rates for MYR, IDR and SGD from the free Frankfurter API and adds them as a new row in Google Sheets.

**Nodes used:** Schedule Trigger → HTTP Request → Edit Fields → Google Sheets

▶️ **Watch the tutorial:** [YouTube](VIDEO-1-LINK)

## Setup
1. Import `01-fx-feed.json` into n8n.
2. Create a Google Sheet with these headers in row 1: `date`, `base`, `MYR`, `IDR`, `SGD`, `logged_at`.
3. Connect your Google account in the Google Sheets node and choose your sheet.
4. In workflow Settings, set the timezone to your own.
