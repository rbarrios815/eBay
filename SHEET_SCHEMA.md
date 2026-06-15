# V2 Sheet Schema

Live V2 Sheet: https://docs.google.com/spreadsheets/d/1JwuNuHofQ0eUn93DbDYX77ykcuznAVunc2rI72uBLfA/edit

## `START_HERE`

High-level project instructions.

## `DRAFT_REVIEW_QUEUE`

Main input queue for the Agent.

Important columns:

- SKU
- eBay Draft URL
- Draft Source
- User Step Complete?
- Agent Action
- Status
- Blocker
- Priority
- Item Location/Bin
- User Notes
- eBay AI Title
- Created Date
- Last Reviewed
- Draft Accessible?
- SKU Confirmed In Draft?
- Next Action
- Final Human Status

## `MARKET_RESEARCH`

Agent output for sold-comps and pricing.

Important columns:

- SKU
- Corrected Item Name
- eBay AI Title
- Agent Suggested Title
- Item ID Confidence
- Low Sold Price / Source / URL / Description
- Average Sold Price / Comp Count / URLs / Description
- Max Sold Price / Source / URL / Description
- Rare/Original Version Notes
- Recommended List Price
- Price Reasoning
- Research Status
- Confidence
- Source URLs
- Agent Notes

## `DRAFT_AUDIT`

Agent output for draft quality control.

Checks:

- Title accuracy
- Category accuracy
- Condition accuracy
- Photo sufficiency
- SKU presence and correctness
- Missing measurements
- Missing model/size
- Shipping concerns
- Description rewrite needs
- Human review needed

## `ITEMS`

Final inventory/listing status sheet.

Tracks:

- SKU
- Physical location/bin
- Draft URL
- Listing URL
- Overall status
- Final title
- Final list price
- Final condition
- Human approval status
- Published/sold dates
- Sold price/net proceeds
- Notes

## `SOURCE_RULES`

Research rules and preferred source order.

## `STATUS_CODES`

Shared status vocabulary.

## `AGENT_RUNBOOK`

Step-by-step Agent execution rules.

## `HUMAN_STEPS`

Minimal checklist for Ricky/cousin.
