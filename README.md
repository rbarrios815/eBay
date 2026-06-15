# eBay Listing Tracker V2

Live V2 Google Sheet: https://docs.google.com/spreadsheets/d/1JwuNuHofQ0eUn93DbDYX77ykcuznAVunc2rI72uBLfA/edit

Raw CSV import sheet for current active listings: https://docs.google.com/spreadsheets/d/1YZUgQA2xh6NKZipCHy5Snz6s2mdME_bX4bmxuNqbD6s/edit

## Current default workflow

**No Agent by default. eBay Seller Hub CSV exports are the bridge. ChatGPT reads the CSV/Sheet, researches sold comps, audits listing data, fills the spreadsheet, and never publishes or revises live listings.**

This replaces the slow Agent-browser workflow for active listing review.

## Source-of-truth split

- **eBay** = live listings, photos, Seller Hub, final edits, publishing, deleting, and offers.
- **eBay active listings CSV** = reliable export bridge from eBay into the tracker.
- **Google Sheets V2** = live queue, imported listing data, audit output, market research, item status.
- **GitHub** = canonical instructions and version history.
- **ChatGPT without Agent** = spreadsheet reader, researcher, pricing analyst, and audit assistant.
- **Human** = exports CSV, reviews recommendations, and manually edits/publishes in eBay.

## Human workflow

1. In eBay Seller Hub, export/download the active listings CSV.
2. Upload the CSV to ChatGPT or place it in Drive.
3. ChatGPT imports/link-wires it into V2.
4. Open V2 and, if Google Sheets shows `#REF!` in `ACTIVE_CSV_IMPORT!A1`, click **Allow access** for the one-time `IMPORTRANGE` connection.
5. ChatGPT researches priority rows from `DRAFT_REVIEW_QUEUE` / `MARKET_RESEARCH`.
6. Human manually decides whether to edit price/title/condition/shipping in eBay.
7. Human publishes/revises/deletes only after manual review.

## ChatGPT no-Agent workflow

1. Read `START_HERE`, `SOURCE_RULES`, `STATUS_CODES`, and `CHATGPT_RUNBOOK`.
2. Use `ACTIVE_CSV_IMPORT`, `ITEMS`, and `DRAFT_REVIEW_QUEUE` as the source rows.
3. Process rows marked `READY_FOR_CHATGPT_RESEARCH`.
4. Research sold comps from public web sources.
5. Fill low/average/max pricing fields in `MARKET_RESEARCH`.
6. Put quality warnings and manual fix notes in `DRAFT_AUDIT`.
7. Mark items ready for human pricing/review.
8. Never publish, revise, or delete an eBay listing.

## V2 tabs

- `START_HERE`
- `ACTIVE_CSV_IMPORT`
- `DRAFT_REVIEW_QUEUE`
- `MARKET_RESEARCH`
- `DRAFT_AUDIT`
- `ITEMS`
- `SOURCE_RULES`
- `STATUS_CODES`
- `CHATGPT_RUNBOOK`
- `HUMAN_STEPS`

## Deprecated from prior V2 / Agent workflow

The default workflow does **not** require:

- ChatGPT Agent browser operation
- direct eBay URL scraping by ChatGPT
- Agent opening private drafts
- Google Drive photo intake
- photo file names as the matching system
- photo manifests
- marker/ruler photos
- ChatGPT grouping raw photos from Drive
- Agent creating or confirming drafts

## Safety rule

ChatGPT may research, audit, suggest, and populate the spreadsheet. ChatGPT must not publish, revise, delete, or otherwise change live eBay listings. Those actions are human-only.
