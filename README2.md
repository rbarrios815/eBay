# EBAY V2 No-Download Paste Pack

Live V2 Google Sheet: https://docs.google.com/spreadsheets/d/1JwuNuHofQ0eUn93DbDYX77ykcuznAVunc2rI72uBLfA/edit

This file replaces the old Drive/photo-intake system. The V2 workflow is intentionally simple:

> eBay AI creates drafts. ChatGPT Agent reviews drafts, researches sold comps, audits listing quality, fills the spreadsheet, and never publishes.

## Minimum user steps

1. Assign SKU.
2. Put SKU on physical item/bag/bin.
3. Use eBay AI/photos to create draft.
4. Put SKU in eBay Custom Label/SKU.
5. Save draft, do not publish.
6. Paste SKU + draft URL into `DRAFT_REVIEW_QUEUE`.
7. Set status to `READY_FOR_AGENT_REVIEW`.

## Minimum Agent steps

1. Open V2 Sheet.
2. Read `START_HERE`, `AGENT_RUNBOOK`, `SOURCE_RULES`, and `STATUS_CODES`.
3. Process only rows marked `READY_FOR_AGENT_REVIEW`.
4. Open eBay Draft URL.
5. Confirm SKU in eBay draft matches Sheet row.
6. Review draft photos, title, category, condition, item specifics, and description.
7. Research sold comps.
8. Populate `MARKET_RESEARCH` and `DRAFT_AUDIT`.
9. Mark row ready for human pricing/review.
10. Never publish.

## Old V1 system is deprecated

Do not use the old process that required Drive photos, photo file lists, photo manifests, marker/ruler photos, or ChatGPT grouping photos from Google Drive.

## Canonical V2 files

- `README.md`
- `WORKFLOW.md`
- `AGENT_START_HERE.md`
- `AGENT_INSTRUCTIONS.md`
- `SHEET_SCHEMA.md`
- `MARKET_RESEARCH_RULES.md`
- `HUMAN_USER_STEPS.md`
- `NO_PUBLISH_POLICY.md`
