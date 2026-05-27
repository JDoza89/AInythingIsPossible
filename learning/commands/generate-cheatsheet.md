Generate a self-contained HTML cheat sheet file at `cheatsheet.html` based on the concepts covered in `memory.md`.

## Rules

- Only include concepts listed as **covered** in `memory.md` — never include concepts listed as gaps or not yet covered
- Every entry must use the learner's own examples from the session where they exist — do not invent generic examples if a session example is available
- This is a reference tool, not a teaching tool — no new concepts, no introductions, no preamble

## Reading memory.md

Before generating, read `memory.md` and extract:

1. The subject being learned
2. The learner's background knowledge (what they're mapping from)
3. All covered concepts — grouped by whatever category structure exists in memory
4. Strong areas and gaps — strong areas get full entries, gaps are skipped entirely
5. Any analogies or examples that landed well — use these in the cheat sheet
6. The core mental model if one has been established — this becomes the first entry

## Output format

A single self-contained `cheatsheet.html` file. No external dependencies — all CSS and JS inline.

### Structure

- Dark background (`#11111b`)
- Sidebar navigation with one item per section
- Sections derived from the category structure in `memory.md` — not hardcoded
- Each section has tabs, one per concept
- Each tab contains:
  - A TL;DR line — one sentence maximum
  - If the learner has a background being mapped from: side-by-side code or comparison blocks (learner's prior knowledge on the left, new concept on the right)
  - If no mapping exists: a single clear example block
  - Insight callouts (💡) for mental model shifts and the "why" behind a concept
  - Gotcha callouts (⚠️) for traps specific to the learner's background

### Visual spec

- Sidebar: `#0d0d1a` background, section headers colored by section, active item highlighted
- Code blocks: `#0d0d1a` background, `#cdd6f4` text, `14px` monospace
- Left/prior knowledge block: blue label and border
- Right/new concept block: green label and border
- 💡 Insight: blue-tinted background, blue left border
- ⚠️ Gotcha: red-tinted background, red left border
- TL;DR bar: `#1e1e2e` background, muted label

### Tab content rules

- Code examples must be concise — minimum needed to demonstrate the concept
- Use session examples first, invent only if none exist
- One primary concept per tab — do not combine unrelated ideas
- Gotchas must be specific to the learner's background — not generic warnings

## After generating

Confirm the file was written and list:

1. The subject and learner background detected from `memory.md`
2. How many sections and concepts were included
3. Which concepts were skipped because they were in the gaps list
4. Which session examples were used
