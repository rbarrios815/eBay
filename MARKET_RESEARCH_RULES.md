# Market Research Rules - V2

## Goal

For each eBay draft, the Agent should populate three useful pricing anchors:

1. Lowest comparable sold price
2. Average comparable sold price
3. Highest / rare / high-ceiling sold price

## Lowest comparable sold price

Use the lowest legitimate comparable sold result.

Do not use obviously broken comparisons unless the user's item is also broken/incomplete.

Examples of bad low comps:

- missing parts
- damaged condition when user's item is good
- local pickup only
- wrong size/version
- unrelated bundle split
- counterfeit/questionable item

## Average comparable sold price

Aim for at least 5 comparable sold prices when possible.

If fewer than 5 reliable sold comps are found, mark `PARTIAL_RESEARCH` and state the comp count.

Average description should summarize what the average comps had in common, not mathematically average text.

## Max / rare / high-ceiling sold price

Capture the highest relevant sold price, including rare/original/sealed/limited versions, but explain why it is high.

Do not let a rare outlier become the normal recommended price unless the user's item matches that rare version.

## Recommended list price

Recommend a price based on:

- condition
- completeness
- version/rarity
- recent sold comps
- platform fit
- shipping/weight concerns
- urgency vs maximizing value

## Required source behavior

- Prefer sold prices over active asking prices.
- Include URLs in the spreadsheet when available.
- Clearly mark whether the source is sold data, active listing, historical price guide, or identification-only source.
- Use confidence labels: HIGH, MEDIUM, LOW.

## Hard rule

Do not invent exact sold prices, model numbers, authenticity, or rarity claims.
