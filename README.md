# eBay Listing Tracker V2

Live V2 Google Sheet: https://docs.google.com/spreadsheets/d/1JwuNuHofQ0eUn93DbDYX77ykcuznAVunc2rI72uBLfA/edit

Raw CSV import sheet for current active listings: https://docs.google.com/spreadsheets/d/1YZUgQA2xh6NKZipCHy5Snz6s2mdME_bX4bmxuNqbD6s/edit

Older visual-prep / draft tracker sheet, if needed for prior batches: https://docs.google.com/spreadsheets/d/1CI763tMOFvOVLYN5QFjScOXnFAaT7idYZdAG9bQvFZY/edit

## Current approved workflow

As of 2026-06-15, Ricky approved an Agent-assisted V2 workflow in addition to the existing CSV/no-Agent workflow.

Canonical Agent instructions: `docs/agent-v2-workflow.md`

## Source-of-truth split

- eBay = live listings, photos, Seller Hub, drafts, final account actions, offers, and sold status.
- eBay Photo Upload = first-pass draft creator for new items. Ricky uploads 6 photos per item.
- eBay active listings CSV = reliable bridge for already-posted active listing data.
- Google Sheets V2 = tracker, resume markers, audit output, market research, approval status, draft/live URLs, and sold status when easy.
- GitHub = canonical instructions and version history.
- ChatGPT / Agent = spreadsheet reader, eBay draft/live listing inspector when available, pricing researcher, quality-control reviewer, and approved editor.
- Ricky = approval authority for edits and final account actions.

## New-item draft workflow

1. Ricky uses eBay Photo Upload with 6 photos per item.
2. eBay creates draft listings from those photo groups.
3. Agent inspects the 6 photos inside each eBay draft when possible.
4. Agent records draft URLs, draft IDs, and status in the V2 spreadsheet.
5. Agent researches pricing once and writes suggested title, description, category, condition, item specifics, price, shipping, and SKU improvements into the spreadsheet.
6. ChatGPT reads proposed changes to Ricky for approval.
7. Agent edits the eBay draft only after Ricky approves.
8. Publishing requires separate explicit approval.

Google Drive photo intake is not required unless eBay draft photos are inaccessible or unclear.

## Live / already-posted listing audit workflow

1. Start from active eBay listings and cross-reference the V2 spreadsheet / active listings CSV.
2. Match listings by eBay item ID, live URL, SKU/custom label, title, photos, and other available identifiers.
3. Populate missing data in `LIVE_LISTING_AUDIT`.
4. Audit every active listing once unless marked `AUDIT_REDO` or `RESEARCH_REDO`.
5. Use sold comps first; use active listings only when sold comps are weak.
6. Record low/average/high sold comps, rare/version high-end note, comp URLs, recommended price, and reasoning.
7. Classify price as `UNDERPRICED`, `GOOD PRICE`, `SLIGHTLY HIGH`, `TOO HIGH`, or `UNKNOWN`.
8. Hold higher for rare, complete, clean, better-version, or hard-to-replace items.
9. Propose non-price fixes too: title, keywords, category, condition notes, item specifics, and description.
10. Agent edits live listings only after Ricky approves in chat.

## Approval rule

Every draft edit and live-listing edit requires Ricky approval in chat for now. Publishing and other final account actions require separate explicit approval.

## Required tabs

- `AGENT_CONTROL`
- `LIVE_LISTING_AUDIT`

Agent must read `START_HERE` and `AGENT_CONTROL` first, then continue from row/status/next-action markers instead of duplicating completed work.

## Previous no-Agent CSV workflow

The no-Agent CSV workflow remains a fallback for active listing review when Agent access is unavailable or too slow.
