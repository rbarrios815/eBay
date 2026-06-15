# Agent Start Here - V2

Live V2 Sheet: https://docs.google.com/spreadsheets/d/1JwuNuHofQ0eUn93DbDYX77ykcuznAVunc2rI72uBLfA/edit

## Read first

1. `START_HERE`
2. `AGENT_RUNBOOK`
3. `SOURCE_RULES`
4. `STATUS_CODES`
5. `DRAFT_REVIEW_QUEUE`

## Process only

Rows in `DRAFT_REVIEW_QUEUE` where `Status = READY_FOR_AGENT_REVIEW`.

## Do not process

- Blank rows
- Rows missing SKU
- Rows missing eBay Draft URL
- Rows not marked `READY_FOR_AGENT_REVIEW`
- Rows where the draft is inaccessible
- Rows where SKU in eBay conflicts with SKU in Sheet

## Required outputs

For each valid row, fill:

- `MARKET_RESEARCH`
- `DRAFT_AUDIT`
- relevant status/notes in `DRAFT_REVIEW_QUEUE`
- final summary/status in `ITEMS` when appropriate

## Hard rule

Never publish an eBay listing.
