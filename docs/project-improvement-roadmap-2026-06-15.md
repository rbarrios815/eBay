# eBay ChatGPT Project Improvement Roadmap

Added: 2026-06-15

This document incorporates the highest-value recommendations from the project research pass. It is intentionally additive. Do not delete or rewrite existing workflow files while an Agent is actively editing the spreadsheet unless Ricky explicitly asks for a cleanup pass.

## Current project model

The project is a human-in-the-loop eBay listing workflow using:

- eBay Photo Upload for new draft creation, currently grouped by Ricky as 6 photos per item.
- eBay active-listing CSV exports for already-posted listings.
- Google Sheets as the source of truth.
- ChatGPT / Agent for research, draft review, live-listing audit, recommendations, and spreadsheet writeback.
- Ricky approval in chat before any eBay draft or live listing edit.
- Separate explicit Ricky approval before publishing, ending, relisting, deleting, accepting offers, or other final eBay account actions.

## What works efficiently now

1. The project separates new-item draft creation from already-posted listing audit.
2. The spreadsheet acts as a queue, audit trail, and source of truth.
3. The Agent can write recommendations without needing immediate live eBay changes.
4. Pricing rules already prefer sold comps and preserve higher pricing for rare, complete, clean, or better-version items.
5. The no-publish rule is strong and should remain even if future automation is added.

## Highest-priority improvements

### 1. Use one live entry path

Canonical entry order:

1. `START_HERE` in the V2 spreadsheet.
2. `AGENT_CONTROL` in the V2 spreadsheet.
3. `AGENT_SAFE_HANDOFF` in the V2 spreadsheet.
4. The relevant work tab: `LIVE_LISTING_AUDIT`, `DRAFT_REVIEW_QUEUE`, `MARKET_RESEARCH`, `DRAFT_AUDIT`, `POSTED_ITEM_SUMMARY`, or `ITEMS`.
5. GitHub docs only when the sheet does not answer the process question.

Reason: older repo docs may describe no-Agent or deprecated workflows. The current process allows Agent-assisted V2 work while keeping CSV as a fallback/bridge.

### 2. Add clarity instead of overwriting during active Agent runs

When the Agent may be running, prefer:

- Add a note.
- Add a recommendation.
- Add a blocker.
- Add a new clarification tab.
- Append below existing control rows.

Avoid:

- Rewriting active item rows without verifying current state.
- Deleting older instructions while another process may be reading them.
- Changing placeholders like `Next Live Listing To Audit` without knowing the Agent has stopped.

### 3. Formalize status transitions

The spreadsheet now has `STATUS_TRANSITION_CONTRACT`. Use it to decide whether a row can move forward.

Minimum rule: no row should move from research/audit into approval-ready status unless it has:

- Exact SKU / eBay item ID / draft ID / listing URL.
- Duplicate check completed.
- Pricing label or clear reason why pricing is unknown.
- Recommendation or blocker.
- Confidence/notes.
- Ricky approval status if an edit is requested.

### 4. Keep automation read-first

Future engineering should begin with read-only validation:

- Check active listing metadata.
- Match eBay item IDs to spreadsheet SKUs.
- Detect duplicates.
- Verify missing required fields.
- Pull read-only listing facts.
- Report blockers.

Do not start with live eBay write automation. Write automation should only come after approval gates are machine-enforced.

### 5. Track quality, not just completion

Use `RESEARCH_QA_METRICS` to evaluate whether the process is getting better.

Recommended metrics:

- Rows processed per day/week.
- Comp coverage ratio.
- Price recommendation acceptance rate.
- Post-review correction rate.
- Blocker rate.
- Duplicate-work rate.
- Listing-quality defect rate.
- Sold tracking coverage.

## Agent-specific instructions

Before each work unit, the Agent should:

1. Read `START_HERE`, `AGENT_CONTROL`, and `AGENT_SAFE_HANDOFF`.
2. Identify exactly one target row or one explicit batch.
3. Check for duplicate SKU, eBay item ID, listing URL, draft URL, audit date, and research status.
4. Research using sold comps first.
5. Label the current price as `UNDERPRICED`, `GOOD PRICE`, `SLIGHTLY HIGH`, `TOO HIGH`, or `UNKNOWN`.
6. Suggest changes in the spreadsheet only.
7. Wait for Ricky approval in chat before editing eBay.
8. Record what changed after an approved edit.
9. If blocked, write the blocker and exact next action.

## Pricing guidance

Use this hierarchy:

1. eBay sold/completed comps or eBay Product Research / Terapeak when available.
2. Platform-specific sold comps for the item type.
3. Active listings only as weaker secondary evidence.
4. Manual judgment when comps are sparse, labeled as low confidence.

Use higher holding price when the item is rare, complete, clean, sealed/new, better version/variant, or hard to replace. Do not treat one extreme comp as the market average unless the reason is documented.

## Approval rule

A spreadsheet recommendation is not approval.

Approval requires Ricky to approve the exact change in chat. Publishing or other final account actions require a separate explicit approval even if a draft edit or live edit was already approved.

## Future engineering sequence

1. Documentation consolidation.
2. Sheet schema/status validation.
3. Duplicate detection checks.
4. Read-only eBay integration or export validation.
5. Pricing/research QA scoring.
6. Human-approved draft editing.
7. Human-approved live editing.
8. Publishing/final actions only if Ricky explicitly approves and safety gates are enforceable.
