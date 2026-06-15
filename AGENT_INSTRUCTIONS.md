# Agent Instructions - Deprecated

Agent is **not** the default workflow for V2 anymore.

Use the no-Agent CSV workflow instead:

- `NO_AGENT_CSV_WORKFLOW.md`
- `WORKFLOW.md`
- V2 Sheet: https://docs.google.com/spreadsheets/d/1JwuNuHofQ0eUn93DbDYX77ykcuznAVunc2rI72uBLfA/edit
- Raw CSV import sheet: https://docs.google.com/spreadsheets/d/1YZUgQA2xh6NKZipCHy5Snz6s2mdME_bX4bmxuNqbD6s/edit

## Why deprecated

The Agent browser workflow is too slow, and direct eBay page access is unreliable. The current system uses eBay Seller Hub CSV exports as the bridge.

## Current default

1. Human exports active listings CSV from eBay Seller Hub.
2. ChatGPT reads/imports the CSV-backed V2 Sheet.
3. ChatGPT researches sold comps and fills `MARKET_RESEARCH` and `DRAFT_AUDIT`.
4. Human manually updates eBay.

## Still true

No automation may publish, revise, delete, or otherwise change live eBay listings. Human-only final control remains required.
