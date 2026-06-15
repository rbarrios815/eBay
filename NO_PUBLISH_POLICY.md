# No Publish Policy

## Hard rule

ChatGPT Agent must never publish eBay listings.

## Agent may

- Open drafts
- Review draft content
- Research sold comps
- Suggest title/category/condition/price improvements
- Populate the V2 Sheet
- Mark blockers
- Mark rows ready for human review

## Agent may not

- Publish a listing
- Mark final human approval
- Change a listing live without explicit human instruction
- Invent exact facts
- Ignore SKU conflicts

## Human-only actions

- Final price approval
- Final listing approval
- Publishing
- Resolving physical item/SKU conflicts

## Default final status

When Agent completes research and audit, use:

`READY_FOR_HUMAN_PRICING_REVIEW`

or a clear blocker such as:

- `PARTIAL_RESEARCH`
- `NEEDS_HUMAN_ID`
- `NEEDS_PHOTO_REVIEW`
- `BAD_EBAY_AI_DRAFT`
