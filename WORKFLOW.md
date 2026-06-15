# V2 Workflow — No-Agent CSV System

Live V2 Sheet: https://docs.google.com/spreadsheets/d/1JwuNuHofQ0eUn93DbDYX77ykcuznAVunc2rI72uBLfA/edit

Raw CSV import sheet: https://docs.google.com/spreadsheets/d/1YZUgQA2xh6NKZipCHy5Snz6s2mdME_bX4bmxuNqbD6s/edit

## Goal

Make the user workflow fast and simple by using the eBay active listings CSV as the bridge instead of ChatGPT Agent browser automation.

## Division of labor

- eBay Seller Hub exports the active listings CSV.
- Google Sheets stores the CSV import, review queue, market research, audit output, and item status.
- ChatGPT without Agent reads the Sheet/CSV and researches comps.
- Human manually updates eBay and publishes/revises/deletes only after review.

## Human intake flow

1. Export active listings CSV from eBay Seller Hub.
2. Upload the CSV to ChatGPT or Drive.
3. ChatGPT imports or links the CSV into V2.
4. In V2, if `ACTIVE_CSV_IMPORT!A1` shows `#REF!`, click **Allow access** for the one-time `IMPORTRANGE` link.
5. Review `DRAFT_REVIEW_QUEUE` priorities.
6. Let ChatGPT research selected rows.
7. Manually edit live eBay listings only after reviewing the recommendations.

## ChatGPT review flow without Agent

1. Read `START_HERE`, `SOURCE_RULES`, `STATUS_CODES`, and `CHATGPT_RUNBOOK`.
2. Use `ACTIVE_CSV_IMPORT` as the imported eBay source.
3. Use `DRAFT_REVIEW_QUEUE` for research order.
4. Use item title, category, condition, current price, watchers, and listing URL from the CSV.
5. Research sold comps from public web sources.
6. Populate `MARKET_RESEARCH` with low/average/max comps, source URLs, recommended price, and reasoning.
7. Populate `DRAFT_AUDIT` with quality warnings and manual fix notes.
8. Mark rows `READY_FOR_HUMAN_PRICE_REVIEW` when research is complete.

## Removed from default workflow

- ChatGPT Agent browser operation
- direct eBay URL scraping as the required bridge
- Agent opening private drafts
- Google Drive photo-intake as a required first step
- photo file names as the required matching system
- photo manifest
- marker/ruler photo requirement
- ChatGPT grouping raw photos from Drive
- Agent creating or confirming drafts

## Non-negotiable rule

ChatGPT never publishes, revises, deletes, or changes live eBay listings. Human-only final control remains required.
