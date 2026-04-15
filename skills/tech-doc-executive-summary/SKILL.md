---
name: tech-doc-executive-summary
description: >
  Analyzes technical documents (Word .docx and PowerPoint .pptx files) describing app design,
  databases, data flows, governance, infrastructure, security, and costs — and produces a polished
  executive-ready PowerPoint deck. Use this skill whenever a user uploads technical design docs and
  asks for an executive summary, a summary deck, a stakeholder presentation, or wants to translate
  technical documentation into business-friendly slides. Trigger even if the user says something
  casual like "turn these docs into a deck for my boss" or "summarize this for leadership." Always
  use this skill when the input is one or more technical documents AND the desired output involves
  a presentation, summary, or executive briefing.
---

# Tech Doc → Executive Summary Skill

Converts technical design documents into a clean, professional executive PowerPoint deck.
Designed for non-technical users: they upload files, you do the work, they get a polished deck.

---

## Output Deck Structure

Always produce exactly these slides (in order):

| # | Slide | Purpose |
|---|-------|---------|
| 1 | **Cover** | Project/app name, subtitle "Executive Summary", date |
| 2 | **Business Need** | Why this solution exists — the problem being solved |
| 3 | **Solution Overview** | What was built/designed — plain-language summary |
| 4 | **System Data Flow** | High-level diagram: boxes (systems/services) + arrows |
| 5 | **Data Governance & Security** | Key governance rules, compliance, security posture |
| 6 | **Infrastructure Summary** | Hosting, platforms, environments (no deep technical detail) |
| 7 | **Costs & Providers** | Table: Service providers, consultants, cost estimates |
| 8 | **Key Risks & Recommendations** | Top 3–5 risks or open questions surfaced from the docs |
| 9 | **Next Steps** | Action items or decisions required (if present in docs) |

If a topic is not covered in the source documents, include the slide with a note: *"Not addressed in source documentation."*

---

## Step-by-Step Workflow

### Step 1 — Read the skill references

Before doing anything else, read:
- `references/extraction-guide.md` — what to look for in each document type
- `references/pptx-build-guide.md` — how to build the deck with pptxgenjs

### Step 2 — Extract content from uploaded documents

For each `.docx` file:
```bash
pandoc --track-changes=all "file.docx" -o extracted.md
```

For each `.pptx` file:
```bash
python -m markitdown "file.pptx"
```

Read ALL extracted content carefully before building the deck.

### Step 3 — Synthesize content into slide data

Map extracted content to the 9 slides using the extraction guide.
Write in plain business language — no jargon, no acronyms without explanation.
Keep bullet points to 3–5 per slide. Prefer short, punchy statements.

### Step 4 — Build the data flow diagram

Identify all named systems, services, databases, and external integrations.
Build a high-level diagram using pptxgenjs shapes:
- Boxes (rectangles with labels) for each system/service
- Arrows between them showing data flow direction
- Keep it to one slide; group tightly related services if needed
- See `references/pptx-build-guide.md` → "Data Flow Diagram" section

### Step 5 — Build the deck

Read `references/pptx-build-guide.md` for full pptxgenjs instructions and the visual style spec.
Install if needed: `npm install -g pptxgenjs`
Build to `/home/claude/executive-summary.pptx`

### Step 6 — QA

```bash
# Content check
python -m markitdown /home/claude/executive-summary.pptx

# Convert to images for visual inspection
python scripts/office/soffice.py --headless --convert-to pdf /home/claude/executive-summary.pptx
pdftoppm -jpeg -r 150 /home/claude/executive-summary.pdf /home/claude/slide
ls -1 /home/claude/slide*.jpg
```

Visually inspect every slide image. Fix overlaps, truncated text, and layout issues.
Re-render and re-check until clean.

### Step 7 — Deliver

Copy to output and present to the user:
```bash
cp /home/claude/executive-summary.pptx /mnt/user-data/outputs/executive-summary.pptx
```

Use the `present_files` tool to share the file. Add a 2–3 sentence summary of what was found and highlight any slides where source docs were thin or silent.

---

## Handling Missing or Ambiguous Information

- If costs are mentioned without totals, sum them and note the assumption.
- If governance/security sections are absent, say so clearly on the slide — never fabricate.
- If multiple apps or projects are described, create a section per app on the relevant slides.
- If the user uploads only one document type (e.g., only Word, no PowerPoint), proceed with what's available.

---

## Dependencies

- `pandoc` — Word doc extraction
- `pip install "markitdown[pptx]"` — PowerPoint extraction  
- `npm install -g pptxgenjs` — deck creation
- LibreOffice + Poppler — visual QA (pre-installed in sandbox)
