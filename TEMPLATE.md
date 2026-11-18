# PFB Slides & Labs — Locked Template Spec

**Locked:** 2026-11-17 · **Course:** 26MB5207E · **Dept of MBA (KLVZA)** · **PFBS**

This document is the single source of truth for every new module (CO2 → CO6).
Build against this, not against screenshots or memory.

---

## 1 · Design Tokens (CSS variables — copy verbatim into every deck page)

```css
:root {
  --bg:#0F172A; --panel:#1E293B; --line:#2B3A55; --ink:#E2E8F0; --dim:#94A3B8;
  --amber:#F5B041; --code:#0B1220;
}
```

Slide background: `#14213D` (navy) · Light slides: `#FAF7F0`
Slide-number color (light): `#4A5568` · (dark/amber slides): `#8FA3C0`
Amber accent: `#F5B041` · Rusted accent (light slides): `#C2570C`

---

## 2 · Header Structure (every page)

**Rule (locked):** page headers carry at most two right-side items — an optional single CTA (intro pages only) and **`All modules`** (back to index). No `CO{X} Lab`, `Download .ipynb`, or `Intro` buttons in headers; the hub is `index.html`.

```html
<header class="top">
  <div class="brand">PFBS &middot; 26MB5207E</div>
  <div class="crumb"><a href="index.html">Course</a> &nbsp;/&nbsp; {COX} Slides</div>
  <div class="grow"></div>
  <a class="btn ghost" href="index.html">All modules</a>
</header>
```

Per page type:
- **Theory deck** (`coX-theory.html`): crumb `… / {COX} Slides` + `All modules` only
- **Labs page** (`coX-labs.html`): crumb `… / {COX} Labs` + `All modules` only
- **`intro.html`**: crumb `… / Intro Slides` + CTA `Start CO1` + `All modules` (the intro's single job is to launch the course; this CTA is the exception to the "one button" rule)

---

## 2b · Labs = Colab (locked model, 2026-11-17)

Labs are **not** rendered on the website. Each module ships:

| File | Role |
|---|---|
| `co{X}-labs.html` | Short instructions page: one amber **`Open in Colab`** button per notebook (`https://colab.research.google.com/drive/{FILE-ID}`, `target="_blank"`) + a dim one-line download fallback under each (`Download the file instead` → `co{X}-lab.ipynb` / `co{X}-tutorial.ipynb` with `download` attribute, for offline/Colab-down) + 3 numbered steps (open → run cells in order, YOUR TURN cells → `Save copy in Drive`) + "what's inside" summary |
| `co{X}-lab.ipynb` | The Colab notebook: blank start, **zero pre-loaded outputs**, lecture walkthrough cells, `YOUR TURN` practical cells, optional auto-checker cell. Also uploaded to the course Google Drive (shared "anyone with the link – Viewer") — the Drive copy is the source the `Open in Colab` button points at |
| `co{X}-tutorial.ipynb` | The Tutorial notebook (added 2026-11-18): a code-along build project with `YOUR TURN` case + auto-checker cell. Same hygiene rules, own Drive link on the same labs page |

- A module may ship **one or two** notebooks (Theory & Practicals, and optionally a Tutorial); `co{X}-labs.html` carries one CTA card per notebook
- The raw download is a **fallback only** — never the primary action
- The CO1 executed lab record (`co1-lab.html`) stays on disk but is **not linked anywhere** — retired from the site
- Index tiles: `<a class="btn ghost" href="co{X}-labs.html">Labs</a>`
- Notebook student hygiene: no instructor-only model answers in the shared file (CO1 Tutorial's "INSTRUCTOR ONLY: model answer" cells 18 & 25 were stripped from the site's `co1-tutorial.ipynb` before publishing; strip equivalents before sharing any module's Drive copy)

### Per-module Colab link registry (update when a module ships)

| Module | Colab open link (Drive file ID) |
|---|---|
| CO1 Theory & Practicals | `https://colab.research.google.com/drive/1zpiq14ZD6k69-BjAxwxEKjtEZlutXGev` |
| CO1 Tutorial | `https://colab.research.google.com/drive/14Sc8HgOrB0bkZ7j0x2RxoCbFnIOSDARy` |
| CO2 | _pending upload_ |
| CO3–CO6 | _pending_ |

When a new module's notebook is uploaded to Drive: share it "anyone with the link – Viewer", copy the link, add the row here, and use its ID in the `co{X}-labs.html` button.

---

## 3 · Stage / Slide Geometry

- `.stage` = `1280 × 720px`, centered, scaled to viewport with `transform: scale(s)`
- All shapes are `<div class="shp" style="left:Lpx;top:Topx;width:Wpx;height:Hpx;…">`
- **No shape may exceed the stage bounds:** `L + W ≤ 1280` and `T + H ≤ 720`
- Slide number div: `left:1150px; top:36px; width:48px; height:29px;` (top-right, text-align right)

---

## 4 · Slide Number Convention

| Slide type | Number color | Position |
|---|---|---|
| Content slides (light bg) | `#4A5568` | top-right, `left:1150px; top:36px` |
| Recap / Checklist (dark/amber bg) | `#8FA3C0` | top-right, `left:1150px; top:36px` |

Title slide, section-divider slides, and activity slides carry **no** number.

---

## 5 · "Next:" Footer (recap + checklist slides only)

Appears on every **`· RECAP`** slide and the final **`CHECKLIST`** slide.

```html
<!-- left:601px top:667px — bottom-right, amber on dark bg -->
<div class="shp" style="left:601px;top:667px;width:618px;height:29px;…">
  <p style="">
    <span style="letter-spacing:0.9px;font-size:19px;color:#F5B041;text-align:right;width:100%">
      Next: CO{X+1} &mdash; {CO{X+1} module name from index.html}
    </span>
  </p>
</div>
```

On the **final CO** slide, change to: `Next: {CO{X+1}} · {module title}`

**Module names (from index.html, use exactly):**
- CO1: Python Fundamentals & Control Flow
- CO2: Data Wrangling with pandas & numpy
- CO3: Relational Data & SQL
- CO4: Programmatic Data Analysis
- CO5: APIs, Data Acquisition & Version Control
- CO6: End-to-End Reproducible Analysis

---

## 6 · Slide Nomenclature (exact strings from PPTX handout)

```
{COX}                         → section divider (COI badge slide)
{COX} / COI{N} / LECTURE {N} → lecture content slides
{COX} / COI{N} / LECTURE {N} · {TOPIC}   → topic sub-slide
{COX} / COI{N} / LECTURE {N} · RECAP     → recap slide
{COX} CHECKLIST                    → final checklist slide
ACTIVITY · {N} MINUTES               → practical activity slide
```

---

## 7 · Bullet Style

All bullet lines use the **inline bullet character** (`&#8226;` = `•`) inside the
same `<span>` as the text — never a separate inline-block span:

```html
<p style="margin-bottom:21px">
  <span style="font-size:37px;color:#14213D">&#8226; {bullet text}</span>
</p>
```

This is the locked format. The earlier `padding-left + inline-block` approach
collapsed visually and is no longer used.

---

## 8 · Code / Output Panel Convention (operator slides)

For slides with a code panel + output panel side-by-side:
- Code panel: right-aligned, `left:601px; top:{y}px; width:616px; height:{h}px`
- Output panel: **directly under** the code panel, same left/width:
  `left:601px; top:{y + h + 10}px; width:616px; height:{h2}px`
- Bullet text / explanation: left half, `left:62px`

---

## 9 · Nav + Keyboard Script (copy verbatim — one per deck page)

- Arrow keys / tap / swipe: advance or go back
- `F`: toggle fullscreen
- Hash routing: `#/N` (N = 1-based slide number)
- `fit()`: scales `.stage` to `min(availW/1280, availH/720)` on every resize

---

## 10 · index.html Grid Layout (1–2–2–2)

```
[ Introduction  — full width, amber "INTRODUCTION" kick ]
[ CO1  ·  FUNDAMENTALS ]  [ CO2  ·  DATA WRANGLING ]
[ CO3  ·  RELATIONAL   ]  [ CO4  ·  ANALYSIS         ]
[ CO5  ·  DATA+APIs    ]  [ CO6  ·  CAPSTONE         ]
```

- Active tiles: `<a class="btn" href="coX-theory.html">Slides</a>
                <a class="btn ghost" href="coX-labs.html">Labs</a>`
- Coming-soon tiles: `class="card soon"` + `<span class="tag-soon">Coming soon</span>`
- Footer: faculty names + coordinator (copy from current index.html footer verbatim)

### Tile promotion (when a module ships)

1. `class="card soon"` → `class="card"`
2. Replace `<span class="tag-soon">Coming soon</span>` with the two active-tile buttons above
3. No other `index.html` edits — and the `intro.html` "Start CO1" button stays as-is

---

## 11 · File Naming

| Purpose | File |
|---|---|
| Theory deck | `co{X}-theory.html` |
| Labs instructions page (Colab download + steps) | `co{X}-labs.html` |
| Lab source notebook (the actual lab, downloaded & run in Colab) | `co{X}-lab.ipynb` |
| Retired: executed lab record (CO1 only, unlinked — do not reuse the pattern) | `co1-lab.html` |
| Intro deck (shared) | `intro.html` |
| Module index | `index.html` |

---

## 12 · Verification Checklist (run before marking a module done)

- [ ] All slide numbers top-right, none at `top:667` (bottom)
- [ ] No shape exceeds `left+width>1280` or `top+height>720`
- [ ] All `href` / `src` targets exist on disk (no broken links)
- [ ] Recap + checklist slides have `Next: CO{X+1} — …` footer
- [ ] Bullet lines use inline `&#8226;` format
- [ ] Operator slides: output panel directly under code panel, same left/width
- [ ] Headers are minimal: theory + labs pages show `All modules` only; intro keeps its `Start CO1` CTA (see §2)
- [ ] Labs page: `Download Colab file` button uses the `download` attribute (file downloads, never opens) and the 5-step + what's-inside sections are present
- [ ] Notebook ships blank: zero pre-loaded outputs, no instructor-only cells
- [ ] Screenshots at `2560×1440` for all content slides, spot-check `1280×760`
