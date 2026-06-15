# Agent V2 Workflow — eBay Photo Upload Drafts + Live Listing Audit

Updated: 2026-06-15

## Goal

Scale Ricky's eBay process toward 1,000 items by using eBay's built-in tools for first-pass draft creation and using ChatGPT/Agent for review, research, recommendations, and approved edits.

The spreadsheet remains the source of truth. Agent must not duplicate completed work and must preserve resume markers.

## Primary sheet

Live V2 Google Sheet:
https://docs.google.com/spreadsheets/d/1JwuNuHofQ0eUn93DbDYX77ykcuznAVunc2rI72uBLfA/edit

Older visual-prep / draft tracker sheet, if needed for prior batches:
https://docs.google.com/spreadsheets/d/1CI763tMOFvOVLYN5QFjScOXnFAaT7idYZdAG9bQvFZY/edit

## Required tabs to read first

1. `START_HERE`
2. `AGENT_CONTROL`
3. `SOURCE_RULES`
4. `STATUS_CODES`
5. `ITEMS`
6. `ACTIVE_CSV_IMPORT`
7. `MARKET_RESEARCH`
8. `DRAFT_AUDIT`
9. `LIVE_LISTING_AUDIT`

If working from the older tracker, read its `AGENT_CONTROL`, `UNIVERSAL_EBAY_AGENT_RULES`, `SYSTEM_CONTRACT`, `AGENT_FORM_FILL_RUNBOOK`, `AGENT_FORM_FILL_QUEUE`, `ITEMS`, and `DRAFT_RECONCILIATION` first.

## New-item draft workflow

Ricky uses eBay Photo Upload, not bulk upload, and tells eBay to create one item per 6 photos.

Process:

1. Ricky uploads photos through eBay Photo Upload.
2. eBay creates draft listings from each 6-photo group.
3. Agent opens eBay drafts and inspects the 6 attached photos directly when possible.
4. Agent records draft URL, draft ID, draft status, and matching spreadsheet row.
5. Agent improves title, description, category, condition notes, item specifics, price, shipping assumptions, and SKU/custom label suggestions.
6. Agent researches pricing once per item unless marked `RESEARCH_REDO`.
7. Agent writes proposed changes into the spreadsheet.
8. ChatGPT reads proposed changes to Ricky for approval.
9. Agent edits eBay only after Ricky approves the proposed changes.
10. Publishing requires a separate explicit approval.

Do not require Google Drive unless eBay draft photos cannot be inspected clearly.

## Live / already-posted listing audit workflow

For active listings, start from active eBay listings and cross-reference with the V2 spreadsheet / CSV import.

Process:

1. Match each active eBay listing to the spreadsheet by eBay item ID, live URL, SKU/custom label, title, photos, and other available identifiers.
2. Populate missing data in `LIVE_LISTING_AUDIT`.
3. Audit every active listing once unless marked `AUDIT_REDO` or `RESEARCH_REDO`.
4. Research prices using sold comps first. Use active listings only when sold comps are weak or missing.
5. Record low sold comp, average sold comp, high sold comp, rare/version high-end note, comp URLs, recommended price, and price-change amount.
6. Classify the price as `UNDERPRICED`, `GOOD PRICE`, `SLIGHTLY HIGH`, `TOO HIGH`, or `UNKNOWN`.
7. Hold higher when the item is rare, complete, clean, a better version/variant, or hard to replace.
8. Also propose non-price improvements: title keywords, category, item specifics, condition notes, descriptions, and obvious listing errors.
9. Clearly wrong live listings are urgent and should be flagged in the spreadsheet.
10. Agent edits live listings only after Ricky approves in chat.

Done for live audit means price reviewed, recommendation written, and approved changes applied. Track sold status if possible, easy, and quick.

## Approval and safety rules

- Every draft edit requires Ricky approval in chat for now.
- Every live-listing edit requires Ricky approval in chat for now.
- Publishing requires separate explicit approval.
- Ending, relisting, deleting, accepting offers, revising shipping, or changing major listing terms requires separate explicit approval.
- Never ask Ricky to paste eBay credentials into chat.
- Ricky handles login, 2FA, security checks, and any sensitive account prompts.

## No duplicate work rules

Before doing work, check:

- audit status
- research status
- edit status
- approval status
- audit date
- research date
- last agent action
- next agent action

Redo work only if Ricky requests it or the row is marked `RESEARCH_REDO`, `AUDIT_REDO`, or equivalent.

## Spreadsheet formatting rule

In `LIVE_LISTING_AUDIT`, the `Price Judgment` cell should be:

- bold for `GOOD PRICE`
- bold and yellow for `SLIGHTLY HIGH`
- yellow for `UNDERPRICED`, `TOO HIGH`, or `UNKNOWN`

## Agent stop conditions

Stop and write the exact blocker if blocked by login, 2FA, eBay security, file picker/photo access, missing required data, unclear item identity, missing approval, or risk of publishing/revising without approval.
