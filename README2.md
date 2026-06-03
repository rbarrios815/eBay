EBAY GITHUB NO-DOWNLOAD PASTE PACK

Use this document when you cannot download files to your computer.

FASTEST OPTION:

1. Open your GitHub repo in the browser.
2. Click Add file → Create new file.
3. For each section below, copy the file path into the filename box and copy the content into the editor.
4. Commit each file, or commit groups of files if GitHub lets you.
5. Minimum viable setup: create README.md, AGENT_START_HERE.md, AGENT_INSTRUCTIONS.md, CHATBOT_INSTRUCTIONS.md, WORKFLOW.md, and SHEET_SCHEMA.md.

IMPORTANT: If GitHub complains that the folder doesn't exist, just type the path with slashes, like apps-script/sync_github_docs_to_sheet.gs. GitHub creates the folder automatically.

==========================================================================================
FILE PATH: README.md
==========================================================================================

# EBAY Listing Agent System

This repository is the canonical instruction source for Ricky's eBay listing workflow.

Google Sheet live console: https://docs.google.com/spreadsheets/d/1CI763tMOFvOVLYN5QFjScOXnFAaT7idYZdAG9bQvFZY/edit

## Source-of-truth split

- **GitHub** = canonical project instructions, version history, diffs, rollback.
- **Google Sheets** = live operating console and queue.
- **Drive / Google Photos** = raw photos and source assets.
- **ChatGPT / Solace** = listing brain: visual grouping, item identification, pricing, title, description, condition, category.
- **Agent** = executor/form-filler: creates eBay drafts from prepared rows.
- **eBay** = final drafts/listings/sales state.

## Core rule

Solace prepares the listing packet.  
The Agent only processes rows marked `READY_FOR_AGENT`.  
The Agent checks for duplicates first, creates a draft, uploads photos if feasible, logs defaults/exceptions, and never publishes.

Ricky approves a listing by making the eBay draft live.

==========================================================================================
FILE PATH: WORKFLOW.md
==========================================================================================

# Workflow

## 1. Photo intake

Ricky uploads item photos to Drive or the working Google Photos/Drive intake location.

Grouping rule:

1. File names close in sequence usually belong to the same item.
2. Visual descriptions should match because angles show the same item.
3. The last photo of each item should include a ruler/measurement marker.
4. One physical item = one eBay listing.
5. No bundles for now. If multiple distinct sellable items appear in one photo, mark `NEEDS_REVIEW_NO_BUNDLE`.

## 2. Solace / Chatbot prep

Solace groups photos and prepares one row per sellable item in the Sheet.

Solace should fill:

- Item ID
- photo group / links
- title
- category guess/final category
- condition and condition notes
- description
- brand/model/size/color/material when visible
- measurements when visible
- visible defects
- included/missing items
- price estimate
- shipping/package notes if available
- confidence and missing info

Pricing rule: estimate from sold comps when available and bias the ask price about **1–5% higher** when reasonable.

## 3. Sheet handoff

The Sheet is the live console.

Main tabs:

- `ITEMS`
- `PHOTO_MANIFEST`
- `AGENT_FORM_FILL_QUEUE`
- `DRAFT_RECONCILIATION`
- `EBAY_FIELDS_LOG`
- `STATUS_CODES`
- `SYSTEM_CONTRACT`
- `GITHUB_CONNECTION_STATUS`

Only complete-enough rows should enter `AGENT_FORM_FILL_QUEUE` as `READY_FOR_AGENT`.

## 4. Agent execution

The Agent:

1. Opens `AGENT_FORM_FILL_QUEUE`.
2. Processes only `READY_FOR_AGENT` rows.
3. Checks eBay drafts/listings for duplicates before creating anything.
4. Creates a new eBay draft only when no duplicate is found.
5. Uploads photos if feasible.
6. Uses eBay suggested/default/best-fit required fields only when safe.
7. Logs any defaults or forced changes.
8. Never publishes.

## 5. Ricky approval

Done means:

> Draft created and populated as completely as possible/as makes sense.

Ricky approves by posting/making the draft live.

==========================================================================================
FILE PATH: CHATBOT_INSTRUCTIONS.md
==========================================================================================

# Chatbot / Solace Instructions

Solace is the listing brain.

## Responsibilities

Solace should:

- Read uploaded photos.
- Group photos into items using filename sequence, visual match, and ruler/end-marker photo.
- Create one listing packet per physical item.
- Avoid duplicate listings.
- Identify visible brand, model, size, color, material, measurements, condition, defects, included items, and missing items.
- Draft eBay title and description.
- Estimate category and condition.
- Estimate price from sold comps when available.
- Bias price 1–5% above recent sold comps when reasonable.
- Put uncertain or missing details into Sheet notes instead of hiding uncertainty.
- Queue only complete-enough rows as `READY_FOR_AGENT`.

## Constraints

- No bundle workflow for now.
- If multiple sellable items appear in one photo, mark `NEEDS_REVIEW_NO_BUNDLE`.
- Do not invent exact model numbers, authenticity claims, measurements, or defects.
- Do not publish listings.
- Approval happens when Ricky makes an eBay draft live.

## Output

Solace writes to:

- `ITEMS`
- `PHOTO_MANIFEST`
- `AGENT_FORM_FILL_QUEUE`
- `STATUS_CODES`
- `EBAY_FIELDS_LOG` when relevant

The Agent should never have to decide the core listing strategy inside eBay.

==========================================================================================
FILE PATH: AGENT_INSTRUCTIONS.md
==========================================================================================

# Agent Instructions

The Agent is the executor/form-filler, not the listing brain.

## Start here

1. Open the Google Sheet.
2. Read `SYSTEM_CONTRACT`.
3. Read `AGENT_FORM_FILL_RUNBOOK`.
4. Open `AGENT_FORM_FILL_QUEUE`.
5. Process only rows marked `READY_FOR_AGENT`.

## Hard rules

- Do not publish.
- Do not create duplicate listings.
- Search existing eBay drafts/listings first.
- Create brand-new eBay drafts only after duplicate check.
- Paste prepared fields from the Sheet.
- Upload photos if feasible.
- If photo upload fails, still save the most complete text draft possible and log `NEEDS_PHOTO_BRIDGE`.
- If eBay requires a missing field, use suggested/default/best-fit only when safe and log it.
- Do not invent important exact facts.

## Required logging

After each item, update:

- Draft URL
- Draft ID if visible
- Draft status
- Photo upload status
- Agent blocker / next action
- Last updated
- Any default values used by eBay
- Any forced edits due to eBay field/length limits

## Completion status

Use one of:

- `DUPLICATE_FOUND_SKIP`
- `DRAFT_CREATED_WITH_PHOTOS`
- `DRAFT_CREATED_NO_PHOTOS`
- `NEEDS_PHOTO_BRIDGE`
- `NEEDS_INFO`
- `NEEDS_RICKY_FIX`
- `DRAFT_COMPLETE_PENDING_RICKY_APPROVAL`

==========================================================================================
FILE PATH: SHEET_SCHEMA.md
==========================================================================================

# Sheet Schema

Live Sheet: https://docs.google.com/spreadsheets/d/1CI763tMOFvOVLYN5QFjScOXnFAaT7idYZdAG9bQvFZY/edit

## Main tabs

### `ITEMS`

Main item database. One row per physical sellable item/listing.

Important fields include:

- Item ID
- Status
- Drive Folder URL
- Main Photo URL
- Photo Count
- Item Name / Short Label
- Item Location
- Category Guess
- eBay Category Final
- Title Draft / Final
- Condition
- Condition Notes
- Description Draft / Final
- Brand / Model / Size / Color / Material
- Measurements
- Defects
- Included Items
- Missing Items
- Price Suggested Low / High / Final
- Listing Format
- Quantity
- Shipping Weight
- Box dimensions
- Shipping Service
- Photo Order
- AI Confidence
- Missing Info
- eBay Draft URL / ID / Status

### `PHOTO_MANIFEST`

Per-photo tracking.

Use this for:

- file names
- Drive links
- batch IDs
- grouping
- item ID assignment
- ruler/end-marker status
- visual notes

### `AGENT_FORM_FILL_QUEUE`

Executable queue. Agent processes only rows marked `READY_FOR_AGENT`.

### `DRAFT_RECONCILIATION`

Agent writes draft results and duplicate findings.

### `EBAY_FIELDS_LOG`

Agent logs eBay defaults, forced choices, and missing/required item specifics.

### `STATUS_CODES`

Shared status vocabulary.

### `SYSTEM_CONTRACT`

Current live copy of the system contract.

### `GITHUB_CONNECTION_STATUS`

Shows whether repo visibility, GitHub write access, and sync are actually working.

==========================================================================================
FILE PATH: HANDOFF_CHECKLIST.md
==========================================================================================

# Ready-for-Agent Handoff Checklist

A row can be marked `READY_FOR_AGENT` only when it is complete enough to create a truthful eBay draft.

## Required

- [ ] Item ID exists.
- [ ] Photos are grouped to one physical item.
- [ ] No duplicate listing/draft known.
- [ ] Main photo selected.
- [ ] Photo links/order available.
- [ ] Title to use is written.
- [ ] Description to use is written.
- [ ] Category is selected or reasonably guessed.
- [ ] Condition is selected.
- [ ] Condition notes are written when needed.
- [ ] Price to use is written.
- [ ] Listing format is set, usually Buy It Now.
- [ ] Quantity is set, usually 1.
- [ ] Shipping/package fields are filled or intentionally marked with a safe placeholder.
- [ ] Important uncertainty is in Missing Info / Notes.

## Do not queue if

- Photos are still an unsorted batch.
- The item is not identified.
- Multiple distinct sellable items appear in one photo and no decision has been made.
- A duplicate draft/listing likely exists and has not been reconciled.
- Title, description, condition, category, or price is missing.

==========================================================================================
FILE PATH: PHOTO_PREP_RUNBOOK.md
==========================================================================================

# Photo Prep Runbook

## Intake

Ricky uploads photos first.

## Grouping logic

Use all three signals:

1. **Filename closeness** — photos close in number are likely one item.
2. **Visual match** — same object, same color/material/markings.
3. **Ruler marker** — the last photo of each item should include a ruler/measurement marker.

## Rules

- One physical item = one listing.
- Multiple angles of one item stay together.
- No duplicate listings.
- No bundle workflow for now.
- If one photo contains multiple distinct sellable items, mark `NEEDS_REVIEW_NO_BUNDLE`.

## Output

For every grouped item:

- assign Item ID
- select main photo
- list photo URLs in order
- capture measurements from ruler photo if visible
- create or update `ITEMS`
- update `PHOTO_MANIFEST`

==========================================================================================
FILE PATH: EBAY_DRAFT_RULES.md
==========================================================================================

# eBay Draft Rules

## Agent may do

- Create brand-new eBay drafts.
- Search drafts/listings to prevent duplicates.
- Paste prepared title, description, condition, category, price, quantity, and item specifics.
- Upload photos if feasible.
- Use eBay suggested/default/best-fit values only when safe.
- Log all defaults and forced changes.

## Agent may not do

- Publish.
- Invent important facts.
- Create duplicate listings.
- Turn ambiguous multi-item photos into bundles.
- Rewrite the listing strategy unless eBay limits require best-fit formatting.

## Done definition

Done means:

> Draft created and populated as completely as possible/as makes sense.

Ricky approves by posting the draft live.

==========================================================================================
FILE PATH: AGENT_START_HERE.md
==========================================================================================

# Agent Start Here

Live Sheet: https://docs.google.com/spreadsheets/d/1CI763tMOFvOVLYN5QFjScOXnFAaT7idYZdAG9bQvFZY/edit

Follow this exact order:

1. Read `SYSTEM_CONTRACT`.
2. Read `AGENT_FORM_FILL_RUNBOOK`.
3. Open `AGENT_FORM_FILL_QUEUE`.
4. Process only rows marked `READY_FOR_AGENT`.
5. Check for duplicate eBay drafts/listings first.
6. Create brand-new draft only if no duplicate exists.
7. Upload photos if feasible.
8. Log results in the Sheet.
9. Never publish.

The Agent is not the listing brain. Solace prepares rows; the Agent executes rows.

==========================================================================================
FILE PATH: repository_manifest.json
==========================================================================================

{
  "project": "EBAY Listing Agent System",
  "spreadsheet_id": "1CI763tMOFvOVLYN5QFjScOXnFAaT7idYZdAG9bQvFZY",
  "spreadsheet_url": "https://docs.google.com/spreadsheets/d/1CI763tMOFvOVLYN5QFjScOXnFAaT7idYZdAG9bQvFZY/edit",
  "canonical_source": "GitHub markdown files",
  "live_operating_console": "Google Sheets",
  "required_files": [
    "README.md",
    "WORKFLOW.md",
    "CHATBOT_INSTRUCTIONS.md",
    "AGENT_INSTRUCTIONS.md",
    "SHEET_SCHEMA.md",
    "HANDOFF_CHECKLIST.md",
    "PHOTO_PREP_RUNBOOK.md",
    "EBAY_DRAFT_RULES.md",
    "AGENT_START_HERE.md",
    "apps-script/sync_github_docs_to_sheet.gs",
    "scripts/validate_instruction_files.py",
    ".github/workflows/validate-instructions.yml"
  ],
  "core_statuses": [
    "PHOTO_UPLOADED",
    "NEEDS_AI_IDENTIFICATION",
    "NEEDS_GROUPING_REVIEW",
    "NEEDS_REVIEW_NO_BUNDLE",
    "READY_FOR_AGENT",
    "DO_NOT_CREATE_DRAFT",
    "DUPLICATE_FOUND_SKIP",
    "DRAFT_CREATED_WITH_PHOTOS",
    "DRAFT_CREATED_NO_PHOTOS",
    "NEEDS_PHOTO_BRIDGE",
    "NEEDS_RICKY_FIX",
    "NEEDS_INFO",
    "DRAFT_COMPLETE_PENDING_RICKY_APPROVAL",
    "POSTED"
  ]
}

