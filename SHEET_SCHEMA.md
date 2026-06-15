# V2 Sheet Schema — No-Agent CSV System

Live V2 Sheet: https://docs.google.com/spreadsheets/d/1JwuNuHofQ0eUn93DbDYX77ykcuznAVunc2rI72uBLfA/edit

Raw CSV import sheet: https://docs.google.com/spreadsheets/d/1YZUgQA2xh6NKZipCHy5Snz6s2mdME_bX4bmxuNqbD6s/edit

## `START_HERE`

High-level no-Agent instructions, current import summary, and human-only safety rules.

## `ACTIVE_CSV_IMPORT`

Linked CSV source tab. It uses `IMPORTRANGE` from the raw eBay active listings CSV import sheet.

If `ACTIVE_CSV_IMPORT!A1` shows `#REF!`, open the V2 Sheet and click **Allow access** once.

## `DRAFT_REVIEW_QUEUE`

Main research queue for ChatGPT without Agent.

Important columns:

- SKU
- eBay Listing URL
- Review Source
- User Step Complete?
- ChatGPT Action
- Status
- Blocker
- Priority
- Item Location/Bin
- User Notes
- eBay Title From CSV
- Created/Start Date
- Last Reviewed
- Reviewer
- Listing URL Accessible?
- SKU Present In eBay Export?
- Next Action
- Final Human Status

## `MARKET_RESEARCH`

ChatGPT output for sold-comps and pricing.

Important columns:

- SKU
- Corrected Item Name
- eBay Title From CSV
- ChatGPT Suggested Title
- Item ID Confidence
- Low Sold Price / Source / URL / Description
- Average Sold Price / Comp Count / URLs / Description
- Max Sold Price / Source / URL / Description
- Rare/Original Version Notes
- Recommended List Price
- Price Reasoning
- Research Status
- Confidence
- Source URLs
- ChatGPT Notes

## `DRAFT_AUDIT`

Listing-quality checklist. It is still named `DRAFT_AUDIT` for continuity, but it now applies to active listings imported from CSV as well.

Checks:

- Title accuracy
- Category accuracy
- Condition accuracy
- Photo sufficiency, when screenshots/photos are provided
- SKU presence and correctness
- Missing measurements
- Missing model/size
- Shipping concerns
- Description rewrite needs
- Human review needed

## `ITEMS`

Final inventory/listing status sheet.

Tracks:

- SKU
- Physical location/bin
- Draft URL, if any
- Listing URL
- Overall status
- Final title
- Final list price
- Final condition
- Human approval status
- Published/sold dates
- Sold price/net proceeds
- Notes

## `SOURCE_RULES`

Research rules and preferred source order. CSV, screenshots, and pasted text are allowed intake bridges. Direct eBay URL reading is reference-only because it may fail.

## `STATUS_CODES`

Shared status vocabulary for CSV imports, research, audit, and human review.

## `CHATGPT_RUNBOOK`

Step-by-step no-Agent execution rules.

## `HUMAN_STEPS`

Minimal checklist for Ricky/cousin.
