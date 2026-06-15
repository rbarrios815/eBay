# No-Agent CSV Workflow

## Why this exists

Agent browser workflows are slow, and direct eBay URL reading can fail. The reliable no-Agent bridge is the seller's own eBay Seller Hub CSV export.

## Live files

- V2 Sheet: https://docs.google.com/spreadsheets/d/1JwuNuHofQ0eUn93DbDYX77ykcuznAVunc2rI72uBLfA/edit
- Raw CSV import sheet: https://docs.google.com/spreadsheets/d/1YZUgQA2xh6NKZipCHy5Snz6s2mdME_bX4bmxuNqbD6s/edit

## Human steps

1. Go to eBay Seller Hub.
2. Export/download the active listings CSV.
3. Upload the CSV to ChatGPT or Drive.
4. ChatGPT imports or links the CSV into V2.
5. Open V2. If `ACTIVE_CSV_IMPORT!A1` shows `#REF!`, click **Allow access** once.
6. Ask ChatGPT to research priority rows.
7. Manually apply any final eBay edits.

## ChatGPT steps

1. Read `START_HERE`, `SOURCE_RULES`, `STATUS_CODES`, and `CHATGPT_RUNBOOK`.
2. Use `ACTIVE_CSV_IMPORT` as the source of eBay listing data.
3. Use `DRAFT_REVIEW_QUEUE` for research priority.
4. For each row, research sold comps and source URLs.
5. Fill `MARKET_RESEARCH` low/average/max sold price fields.
6. Fill `DRAFT_AUDIT` with warnings and manual review notes.
7. Mark completed rows for human price/revision review.

## Do not do

- Do not use Agent as the default workflow.
- Do not depend on ChatGPT opening live eBay item URLs directly.
- Do not publish, revise, delete, accept offers, or change shipping through automation.
- Do not invent item model, condition, authenticity, rarity, or measurements.

## Allowed bridges when CSV is not enough

- screenshots of the listing page
- screenshots of photos
- pasted descriptions/item specifics
- Drive folder with item photos
- manual notes in the Sheet
