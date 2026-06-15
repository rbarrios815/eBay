# Project V2 Spec

## Name

eBay Listing Tracker V2 - eBay AI Draft Review System

## Live Sheet

https://docs.google.com/spreadsheets/d/1JwuNuHofQ0eUn93DbDYX77ykcuznAVunc2rI72uBLfA/edit

## One-sentence system

The human creates an eBay AI draft with SKU; ChatGPT Agent reviews the draft, researches sold comps, audits quality, fills the spreadsheet, and never publishes.

## Simplification target

The user should only have to:

1. SKU the item.
2. Create/save eBay AI draft.
3. Put SKU in eBay Custom Label/SKU.
4. Paste SKU + draft URL in the Sheet.

The AIs do the heavy lifting.

## Heavy lifting by eBay AI

- photo-based first-pass draft creation
- title/category/item specifics suggestions
- draft creation inside eBay

## Heavy lifting by ChatGPT Agent

- verify item from eBay draft/photos
- research sold comps
- fill low/average/max pricing fields
- explain rare/high-ceiling comps
- recommend list price
- audit draft quality
- update Sheet

## Human-only final control

- final approval
- final price decision
- publishing
