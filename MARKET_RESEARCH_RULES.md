# Market Research Rules - V2 No-Agent CSV System

## Goal

For each eBay listing row, ChatGPT should populate three useful pricing anchors:

1. Lowest comparable sold price
2. Average comparable sold price
3. Highest / rare / high-ceiling sold price

## Required source hierarchy

Use these sources in this order when practical. Sold data beats asking prices.

| Priority | Site / Source | Best use | How to treat it |
|---:|---|---|---|
| 1 | eBay sold listings / Terapeak | Primary source for anything that will be sold on eBay | Best source when accessible; use sold prices, not active asks. |
| 2 | WorthPoint | Old toys, antiques, vintage collectibles, obscure items | Historical price-guide/sales source; useful when eBay public search is weak. |
| 3 | 130Point | eBay sold comps and Best Offer research | Use to supplement eBay sold data. |
| 4 | Discogs | Vinyl, CDs, cassettes, Latin music releases | Best exact-release identity and marketplace history source for music media. |
| 5 | Popsike | Vinyl records and rare record auction history | Use for vinyl high-ceiling and rare comps. |
| 6 | Etsy | Vintage/decor/collectibles active listing comps | Mostly asking prices; use as a ceiling/sanity check, not proof of sold value. |
| 7 | Mercari | Everyday used goods, toys, media, small collectibles | Good for active/market pressure; weaker than sold eBay comps. |
| 8 | Facebook Marketplace | Local pickup and bulky/local goods | Local asking prices only; weak sold-price proof. |
| 9 | OfferUp | Local used goods and small collectibles | Local asking/negotiation range; not strong sold proof. |
| 10 | Poshmark / Depop | Clothing, shoes, accessories, trendy vintage | Use mainly for apparel/fashion items. |

## Source classification labels

Every comp should be labeled as one of these:

- `SOLD_PRICE`
- `ACTIVE_ASKING_PRICE`
- `HISTORICAL_PRICE_GUIDE`
- `IDENTIFICATION_ONLY`
- `NO_PUBLIC_COMP_FOUND`

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
- current watchers from the eBay CSV
- current active price from the eBay CSV

## Required source behavior

- Prefer sold prices over active asking prices.
- Include URLs in the spreadsheet when available.
- Clearly mark whether the source is sold data, active listing, historical price guide, or identification-only source.
- Use confidence labels: HIGH, MEDIUM, LOW.
- If the 10-source search finds no reliable comp, write `NO_PUBLIC_COMP_FOUND` instead of guessing.

## Hard rule

Do not invent exact sold prices, model numbers, authenticity, or rarity claims.
