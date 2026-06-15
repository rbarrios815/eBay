# Agent Safe Handoff Checklist

Added: 2026-06-15

This checklist is for Agent runs that touch eBay drafts, active listings, or the eBay Listing Tracker V2 spreadsheet. It is additive and concurrency-safe: use it to clarify behavior, not to overwrite active rows while another Agent may be running.

## Non-negotiable safety rules

- Do not publish.
- Do not end listings.
- Do not relist.
- Do not delete listings.
- Do not accept offers.
- Do not revise live listings without explicit Ricky approval for the exact edit.
- Do not edit drafts without explicit Ricky approval for the exact edit.
- Do not handle login, 2FA, password, payment, or security prompts. Ricky handles those.
- Do not invent item identity, brand, model, condition, defects, completeness, rarity, or sold-comp support.

## Required first read

Before doing work, read these spreadsheet tabs in order:

1. `START_HERE`
2. `AGENT_CONTROL`
3. `AGENT_SAFE_HANDOFF`
4. `STATUS_TRANSITION_CONTRACT`
5. The specific work tab for the task:
   - `LIVE_LISTING_AUDIT` for already-posted listings.
   - `DRAFT_REVIEW_QUEUE` for draft review queue.
   - `MARKET_RESEARCH` for pricing/comps.
   - `DRAFT_AUDIT` for title/category/condition/shipping/photo problems.
   - `POSTED_ITEM_SUMMARY` for concise live listing recommendations.
   - `ITEMS` for item/listing source-of-truth status.

## Work-unit rule

Work one listing or one explicit batch at a time.

Before starting, identify:

- Internal SKU / custom label.
- eBay item ID or eBay draft ID.
- Listing URL or draft URL.
- Spreadsheet row/tab being updated.
- Current status.
- Last action and next action.

If the target cannot be identified, write `BLOCKED_TARGET_UNCLEAR` and stop.

## Duplicate check

Before researching or editing, search for the same:

- SKU.
- eBay item ID.
- Draft ID.
- Listing URL.
- Draft URL.
- Title if SKU/ID is missing.

Check at least:

- `ITEMS`
- `LIVE_LISTING_AUDIT`
- `MARKET_RESEARCH`
- `DRAFT_AUDIT`
- `POSTED_ITEM_SUMMARY`

If there is already completed work and Ricky did not request redo, write a note and do not duplicate the work.

## Pricing labels

Every price review should use one label:

- `UNDERPRICED`
- `GOOD PRICE`
- `SLIGHTLY HIGH`
- `TOO HIGH`
- `UNKNOWN`

Use sold comps first. Active asking prices are weaker evidence and should be labeled as such. If the item is rare, complete, clean, sealed, or a better version/variant, it is acceptable to recommend holding higher if the reason is written clearly.

## Approval states

A recommendation in the spreadsheet does not equal approval.

Use these concepts:

- `RESEARCH_COMPLETE_NEEDS_APPROVAL`: research/recommendation is ready for Ricky.
- `AWAITING_RICKY_APPROVAL`: exact edit has been proposed but not approved.
- `APPROVED_FOR_DRAFT_EDIT`: Ricky approved exact draft edit.
- `APPROVED_FOR_LIVE_EDIT`: Ricky approved exact live listing edit.
- `DRAFT_EDITED_PENDING_REVIEW`: approved draft edit completed and needs review.
- `LIVE_EDITED_PENDING_REVIEW`: approved live edit completed and needs review.
- `BLOCKED_NEEDS_RICKY`: cannot proceed without Ricky.

Publishing/final account actions require separate explicit approval and should never be implied from another approval.

## Writeback rule

When work is complete, write:

- What was reviewed.
- What evidence was used.
- Price label and recommendation.
- Suggested title/category/description/condition/photo/shipping improvements if relevant.
- Confidence level.
- Whether Ricky approval is needed.
- Exact next action.

If blocked, write one clear blocker and the exact next action Ricky or the Agent should take.

## Recommended blocker labels

- `BLOCKED_LOGIN_OR_2FA`
- `BLOCKED_TARGET_UNCLEAR`
- `BLOCKED_DUPLICATE_CONFLICT`
- `BLOCKED_MISSING_PHOTOS`
- `BLOCKED_PHOTO_ACCESS`
- `BLOCKED_ITEM_ID_MISSING`
- `BLOCKED_DRAFT_URL_MISSING`
- `BLOCKED_NO_RELIABLE_COMPS`
- `BLOCKED_REQUIRED_ITEM_FACTS_MISSING`
- `BLOCKED_AWAITING_RICKY_APPROVAL`

## Default behavior when unsure

When unsure, do not edit eBay. Add a note, add a recommendation, or write a blocker in the spreadsheet.
