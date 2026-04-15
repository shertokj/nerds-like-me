# PPTX Build Guide (pptxgenjs)

This guide covers how to build the executive summary deck using pptxgenjs.

---

## Visual Style Spec

Use the **Midnight Executive** palette throughout:

| Role | Color | Hex |
|------|-------|-----|
| Primary (dark background) | Navy | `1E2761` |
| Secondary (light backgrounds) | Ice Blue | `CADCFC` |
| Accent / headings | White | `FFFFFF` |
| Body text | Near-black | `1A1A2E` |
| Table header fill | Navy | `1E2761` |
| Table row alt fill | Light ice | `E8F0FE` |
| Diagram box fill | Ice Blue | `CADCFC` |
| Diagram box border | Navy | `1E2761` |
| Arrow color | Navy | `1E2761` |

**Fonts:**
- Titles: Calibri Bold, 36pt (cover), 28pt (section slides)
- Subtitles / section labels: Calibri, 18pt
- Body text: Calibri, 14pt
- Table text: Calibri, 12pt
- Captions: Calibri, 10pt, color `666666`

**Layout:**
- Slide size: 13.33" × 7.5" (widescreen 16:9)
- Margin: 0.5" from all edges
- Content area: 12.33" wide × 6.5" tall
- Dark slides: Cover (#1) and final slide (#9 or last) — navy background, white text
- Light slides: All content slides — white background, navy/dark text

**Motif:** Thin navy left-border bar (0.08" wide, full content height) on every light slide for visual consistency.

---

## Setup

```javascript
const pptxgen = require("pptxgenjs");
const prs = new pptxgen();
prs.layout = "LAYOUT_WIDE"; // 13.33 x 7.5

const NAVY = "1E2761";
const ICE  = "CADCFC";
const WHITE = "FFFFFF";
const DARK = "1A1A2E";
const ICE_LIGHT = "E8F0FE";
```

---

## Slide Templates

### Dark Slide (Cover & Last Slide)

```javascript
const slide = prs.addSlide();
slide.background = { color: NAVY };

// Title
slide.addText("Project Name", {
  x: 0.6, y: 2.5, w: 12.0, h: 1.0,
  fontSize: 40, bold: true, color: WHITE, fontFace: "Calibri",
  align: "center"
});

// Subtitle
slide.addText("Executive Summary", {
  x: 0.6, y: 3.7, w: 12.0, h: 0.5,
  fontSize: 20, color: ICE, fontFace: "Calibri",
  align: "center"
});

// Date
slide.addText("April 2026", {
  x: 0.6, y: 6.8, w: 12.0, h: 0.4,
  fontSize: 11, color: ICE, fontFace: "Calibri",
  align: "center"
});
```

### Light Content Slide (Standard)

```javascript
const slide = prs.addSlide();
slide.background = { color: WHITE };

// Left accent bar
slide.addShape(prs.ShapeType.rect, {
  x: 0.3, y: 0.4, w: 0.08, h: 6.6,
  fill: { color: NAVY }, line: { color: NAVY }
});

// Slide title
slide.addText("Slide Title", {
  x: 0.55, y: 0.4, w: 12.0, h: 0.6,
  fontSize: 28, bold: true, color: NAVY, fontFace: "Calibri"
});

// Body bullets
slide.addText([
  { text: "First bullet point here", options: { bullet: true } },
  { text: "Second bullet point here", options: { bullet: true } },
  { text: "Third bullet point here", options: { bullet: true } },
], {
  x: 0.55, y: 1.2, w: 12.0, h: 5.5,
  fontSize: 14, color: DARK, fontFace: "Calibri",
  valign: "top"
});
```

---

## Costs Table Slide

```javascript
const slide = prs.addSlide();
slide.background = { color: WHITE };

// Left bar + title (same as light slide)

// Table rows — build from extracted data:
// [ ["Provider", "Type", "Cost", "Frequency"], ["AWS", "Cloud hosting", "$2,400/mo", "Recurring"], ... ]

const rows = tableData.map((row, i) => row.map(cell => ({
  text: cell,
  options: {
    fill: { color: i === 0 ? NAVY : (i % 2 === 0 ? ICE_LIGHT : WHITE) },
    color: i === 0 ? WHITE : DARK,
    bold: i === 0,
    fontSize: i === 0 ? 13 : 12,
    fontFace: "Calibri",
    border: { type: "solid", pt: 0.5, color: "CCCCCC" },
    margin: [4, 8, 4, 8]
  }
})));

slide.addTable(rows, {
  x: 0.55, y: 1.2, w: 12.1,
  colW: [3.5, 2.5, 2.5, 2.5],   // adjust to content
  rowH: 0.38
});
```

---

## Data Flow Diagram

Build the diagram using shapes and connectors. Keep it simple: boxes + labeled arrows.

### Layout Strategy

- Divide slide into a 3-column or 2-row grid depending on number of systems
- Place each system as a rounded rectangle
- Use `line` shapes with arrowheads for connections
- Label arrows with a small text box placed near the midpoint

```javascript
// Example: 5-system linear flow across the slide
const systems = [
  { label: "Customer Portal", x: 0.6,  y: 2.8 },
  { label: "API Gateway",     x: 3.2,  y: 2.8 },
  { label: "App Server",      x: 5.8,  y: 2.8 },
  { label: "Database",        x: 8.4,  y: 2.8 },
  { label: "Data Warehouse",  x: 11.0, y: 2.8 },
];

const BOX_W = 1.9;
const BOX_H = 0.8;

systems.forEach(sys => {
  // Box
  slide.addShape(prs.ShapeType.roundRect, {
    x: sys.x, y: sys.y, w: BOX_W, h: BOX_H,
    fill: { color: ICE },
    line: { color: NAVY, pt: 1.5 },
    rectRadius: 0.1
  });
  // Label
  slide.addText(sys.label, {
    x: sys.x, y: sys.y, w: BOX_W, h: BOX_H,
    fontSize: 11, bold: true, color: NAVY,
    fontFace: "Calibri", align: "center", valign: "middle"
  });
});

// Arrows between consecutive boxes
for (let i = 0; i < systems.length - 1; i++) {
  const from = systems[i];
  const to   = systems[i + 1];
  slide.addShape(prs.ShapeType.line, {
    x: from.x + BOX_W,
    y: from.y + BOX_H / 2,
    w: to.x - (from.x + BOX_W),
    h: 0,
    line: { color: NAVY, pt: 1.5, endArrowType: "arrow" }
  });
}
```

### Non-Linear Flows (hub-and-spoke or branching)

If there is a central system with multiple connections (e.g., an integration hub), place the hub
in the center and radiate spokes outward. Use the same box and line pattern but adjust x/y
coordinates to create a circular or cross layout.

For complex flows (more than 8 systems), group related systems into labeled clusters using a
lightly filled background rectangle behind each group.

```javascript
// Cluster background
slide.addShape(prs.ShapeType.rect, {
  x: 0.4, y: 1.5, w: 4.0, h: 5.0,
  fill: { color: "F0F4FF" },
  line: { color: "CADCFC", pt: 1 }
});
slide.addText("Frontend", {
  x: 0.4, y: 1.5, w: 4.0, h: 0.35,
  fontSize: 10, color: NAVY, fontFace: "Calibri",
  align: "center", italic: true
});
```

---

## Save & Output

```javascript
prs.writeFile({ fileName: "/home/claude/executive-summary.pptx" })
   .then(() => console.log("Done"))
   .catch(err => console.error(err));
```

Run with: `node build-deck.js`

---

## Common Mistakes to Avoid

- Don't let text overflow boxes — test at 12pt and shorten labels if needed
- Don't use more than 5 bullets per slide — split into two slides if needed
- Don't place text below y=7.0 — it will be cut off
- Don't skip the left accent bar on light slides — it ties the deck together visually
- Arrows: use `endArrowType: "arrow"` not custom shapes
- Always set `h` on text boxes large enough for the content to avoid clipping
