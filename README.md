# eBay Listing Tracker V2

Live V2 Google Sheet: https://docs.google.com/spreadsheets/d/1JwuNuHofQ0eUn93DbDYX77ykcuznAVunc2rI72uBLfA/edit

## Core workflow

**eBay AI creates the draft. ChatGPT Agent reviews the draft, researches sold comps, audits the draft, fills the spreadsheet, and never publishes.**

This V2 project removes the old Google Drive photo-intake workflow.

## Source-of-truth split

- **eBay** = photos, AI-generated drafts, draft/listing state.
- **Google Sheets V2** = live queue, audit output, market research, item status.
- **GitHub** = canonical instructions and version history.
- **ChatGPT Agent** = reviewer, researcher, pricing analyst, and spreadsheet updater.
- **Human** = creates/saves drafts and publishes only after review.

## Human workflow

1. Assign SKU to the physical item.
2. Put the SKU on the item, bag, or bin.
3. Use eBay AI/photos to create an eBay draft.
4. Put the same SKU in eBay Custom Label/SKU.
5. Save the draft, but do not publish.
6. Paste SKU + eBay Draft URL into `DRAFT_REVIEW_QUEUE`.
7. Set status to `READY_FOR_AGENT_REVIEW`.

## Agent workflow

1. Open the V2 Sheet.
2. Read `AGENT_RUNBOOK`.
3. Process only rows in `DRAFT_REVIEW_QUEUE` marked `READY_FOR_AGENT_REVIEW`.
4. Open the eBay Draft URL.
5. Confirm the SKU in eBay matches the Sheet row.
6. Review photos, title, category, condition, item specifics, and description.
7. Research sold comps across eBay and other relevant platforms.
8. Fill `MARKET_RESEARCH` and `DRAFT_AUDIT`.
9. Mark the row ready for human pricing/review.
10. Never publish.

## V2 tabs

- `START_HERE`
- `DRAFT_REVIEW_QUEUE`
- `MARKET_RESEARCH`
- `DRAFT_AUDIT`
- `ITEMS`
- `SOURCE_RULES`
- `STATUS_CODES`
- `AGENT_RUNBOOK`
- `HUMAN_STEPS`

## Deprecated from V1

The V2 workflow does **not** require:

- Google Drive photo intake
- photo file names
- photo manifests
- marker/ruler photos
- ChatGPT grouping photos from Drive
- Agent creating first-pass drafts from prepared photo rows

## Safety rule

The Agent may research, audit, suggest, and populate the spreadsheet. The Agent must not publish eBay listings.
