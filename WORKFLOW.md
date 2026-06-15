# V2 Workflow

Live V2 Sheet: https://docs.google.com/spreadsheets/d/1JwuNuHofQ0eUn93DbDYX77ykcuznAVunc2rI72uBLfA/edit

## Goal

Make the user workflow stupid simple and push the heavy work to eBay AI and ChatGPT Agent.

## Division of labor

- eBay AI creates first-pass drafts from photos.
- Human assigns SKU and saves the draft.
- ChatGPT Agent audits and researches the draft.
- Google Sheets stores the queue and output.
- Human publishes only after review.

## Human intake flow

1. Assign a SKU to the item.
2. Put the SKU on the physical item, bag, or bin.
3. Use eBay AI/photos to create an eBay draft.
4. Enter the same SKU into eBay Custom Label/SKU.
5. Save the draft.
6. Paste SKU and eBay Draft URL into `DRAFT_REVIEW_QUEUE`.
7. Set `Status` to `READY_FOR_AGENT_REVIEW`.

## Agent review flow

1. Read `AGENT_RUNBOOK`.
2. Process only rows marked `READY_FOR_AGENT_REVIEW`.
3. Open the eBay Draft URL.
4. Confirm draft accessibility.
5. Confirm SKU matches the Sheet row.
6. Review photos, title, category, condition, description, item specifics, and shipping concerns.
7. Research sold comps from eBay and relevant platforms.
8. Populate `MARKET_RESEARCH`.
9. Populate `DRAFT_AUDIT`.
10. Mark row `READY_FOR_HUMAN_PRICING_REVIEW` or an appropriate blocker status.

## Removed from V2

- Google Drive photo intake
- photo file names as a required matching system
- photo manifest
- marker/ruler photo requirement
- ChatGPT grouping raw photos from Drive
- Agent creating first-pass drafts from raw photo groups

## Non-negotiable rule

Agent never publishes listings.
