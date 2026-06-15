# Project V2 Spec

## Name

eBay Listing Tracker V2 - No Agent CSV System

## Live Sheet

https://docs.google.com/spreadsheets/d/1JwuNuHofQ0eUn93DbDYX77ykcuznAVunc2rI72uBLfA/edit

## Raw CSV Import Sheet

https://docs.google.com/spreadsheets/d/1YZUgQA2xh6NKZipCHy5Snz6s2mdME_bX4bmxuNqbD6s/edit

## One-sentence system

The human exports active listings from eBay Seller Hub as CSV; ChatGPT without Agent reads the CSV-backed V2 tracker, researches comps, audits listing data, fills the spreadsheet, and never publishes or revises live eBay listings.

## Simplification target

The user should only have to:

1. Export active listings CSV from eBay.
2. Upload the CSV to ChatGPT or Drive.
3. Let ChatGPT populate/research V2 from the CSV-backed Sheet.
4. Manually decide and apply any final eBay edits.

## Heavy lifting by eBay / Seller Hub

- keeps the live listing records
- exports active listing CSV data
- remains the only place where live listing edits/publishing/deleting happen

## Heavy lifting by ChatGPT without Agent

- import/link CSV rows into V2
- identify high-priority rows from price/watchers/missing data
- research sold comps
- fill low/average/max pricing fields
- explain rare/high-ceiling comps
- recommend list price
- audit listing-data quality from CSV/screenshots/pasted text
- update Sheet fields and notes

## Deprecated default approach

ChatGPT Agent is no longer the default workflow because it is too slow and direct eBay page access is unreliable. Use CSV exports, screenshots, or pasted listing text as the bridge instead.

## Human-only final control

- final approval
- final price decision
- eBay edits/revisions
- publishing/deleting
- offer decisions
