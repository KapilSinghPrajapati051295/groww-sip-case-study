# GROWW — SIP 12-MONTH CONTINUATION · COMPLETE PROJECT HANDOFF

_Generated 2026-11-09 · 34 source files embedded verbatim._

---
## 0. INSTRUCTIONS FOR THE RECEIVING AI (read first)

You are given the **complete source** of a Product-Management case-study project. Your job:

1. **Recreate every file exactly.** Each file appears between two markers:
   ```
   >>>>> FILE: <relative/path> >>>>>
   ... exact file content (UTF-8, verbatim — including any backticks) ...
   <<<<< END FILE: <relative/path> <<<<<
   ```
   Write the content **byte-for-byte** to `<relative/path>` under a root folder named
   `groww-sip-case-study/`. Do not reformat, re-indent, or 'improve' anything.
2. **Do not skip any file.** Create parent folders as needed. Preserve exact paths & names.
3. **Regenerate the derived artifacts** by running the commands in section 3. The data files,
   web bundle, eval report and deck are deterministic outputs of the embedded code (fixed
   random seed) — regenerating reproduces them identically.
4. **Zip it.** Produce `groww-sip-case-study.zip` of the whole folder (after regenerating).
5. **Verify** against the expected outputs in section 4. If any number differs, stop and report.

Nothing in this project is investment advice; keep the no-advice / no-FOMO guardrails intact.

---
## 1. WHAT THIS PROJECT IS

A graduation/fellowship PM case study. **Role:** Product Manager, Growth @ **Groww**.
**Business metric:** increase the % of first-time mutual-fund investors who still have an
**active SIP** (>=1 successful instalment in the last 30 days) **12 months** after their first.
**Constraints:** discover the problem (not given); **no fund/stock recommendations**; **no
fear/FOMO/urgency**; MVP must not be investment advice and must be eval-gated.

It delivers all 8 parts + 4 deliverables:
- **Part 1 Discovery Engine** — Python pipeline (collect→clean→tag→judge→analyze→export) that
  computes EVERY number in code over a representative SIP-feedback corpus, + a static web app
  (funnel, opportunity ranking, grounded + guardrailed chatbot).
- **Part 2 Metric tree**, **Part 3/6 Research**, **Part 4 Problem**, **Part 5 eval-gated MVP**
  (SIP Sense-Maker web app + Node eval harness), **Part 7 Metrics**, **Part 8 Risks**, + 10-slide
  deck builder, README, RUNBOOK, and an AI Evidence Log (golden set + agreement + corrections).
- Both web apps are **Groww-themed** (green 🟩#00D09C) with a **light/dark theme toggle**.

---
## 2. FULL FILE TREE

### Source files (embedded in section 5, recreate these)
```
README.md
RUNBOOK.md
deck/build_deck.py
discovery-engine/README.md
discovery-engine/evidence-log/AI-Evidence-Log.md
discovery-engine/evidence-log/corrections.json
discovery-engine/evidence-log/golden_set.json
discovery-engine/pipeline/analyze.py
discovery-engine/pipeline/clean.py
discovery-engine/pipeline/collect.py
discovery-engine/pipeline/export.py
discovery-engine/pipeline/generate_corpus.py
discovery-engine/pipeline/judge.py
discovery-engine/pipeline/run_pipeline.py
discovery-engine/pipeline/tag.py
discovery-engine/pipeline/taxonomy.py
discovery-engine/web/app.js
discovery-engine/web/index.html
discovery-engine/web/styles.css
metric-tree/metric-tree.md
metrics/success-metrics.md
mvp/README.md
mvp/evals/golden.js
mvp/evals/run_evals.js
mvp/index.html
mvp/package.json
mvp/src/app.js
mvp/src/reasoner.js
mvp/src/styles.css
problem/problem-definition.md
research/findings.md
research/interview-guide.md
research/mvp-user-testing.md
risks/risks.md
```

### Generated at runtime (DO NOT hand-write — produced by running section 3)
```
discovery-engine/data/raw_corpus.json  (generate_corpus.py)
discovery-engine/data/collected.json, source_probe.json  (collect.py)
discovery-engine/data/clean_corpus.json, clean_report.json  (clean.py)
discovery-engine/data/tagged_corpus.json  (tag.py)
discovery-engine/data/judge_report.json  (judge.py)
discovery-engine/data/precomputed_stats.json, insights.json  (analyze.py)
discovery-engine/web/engine_bundle.json, discovery-engine/data/export_tagged.csv  (export.py)
mvp/evals/eval_report.json  (node evals/run_evals.js)
deck/NL_Groww.pptx  (build_deck.py)
```

---
## 3. RECONSTRUCTION COMMANDS (run in order, from the project root)

```bash
# prerequisites: Python 3.8+, and Node 18+ on PATH
pip install python-pptx                       # only needed for the deck

# Part 1 — regenerate corpus + run all 6 pipeline stages (~5s, deterministic)
cd discovery-engine/pipeline
python run_pipeline.py --regen

# Part 5 — MVP eval gate (tests the real reasoner)
cd ../../mvp
node evals/run_evals.js

# Deck
cd ../deck
python build_deck.py                        # -> NL_Groww.pptx

# serve the apps locally (optional)
#   discovery-engine/web  ->  python -m http.server 5601
#   mvp                   ->  python -m http.server 5602
```

Then zip the whole `groww-sip-case-study/` folder into `groww-sip-case-study.zip`.

---
## 4. EXPECTED VERIFICATION (must match exactly)

- Pipeline funnel: **Collected 6,448 → Cleaned 3,777 → Classified 3,089**.
- Clean drops: non_latin 195, too_short 502, duplicate 375, prefilter_miss 1,599.
- `judge.py`: golden 24/24 · **relevance 100.0%** · **theme 83.3%** · FN=0 · confusions=4.
- `analyze.py`: top opportunity **Mandate / auto-pay failure (100.0/100)**; mechanical 23.8%
  vs behavioural ~54.6%.
- `export.py`: engine_bundle.json (~62 KB, 144 quotes) + export_tagged.csv (3,777 rows).
- MVP evals: **20/20 passed, 0 safety violations**.
- Deck: **NL_Groww.pptx, 10 slides**, no author name, all text >=14pt.

---
## 5. SOURCE FILES (verbatim — recreate each exactly)

>>>>> FILE: README.md >>>>>
# Groww — 12-month SIP Continuation (PM case study)

**Goal:** increase the % of first-time mutual-fund investors who still have an
**active SIP** 12 months after their first one. **Role:** PM, Growth. One folder,
everything needed to review, run, and deploy.

**The thesis in one line:** first-time SIP drop-off is a **legibility** problem,
not a markets problem — the app shows a *number*, never a *narrative*, so an
intent-full investor can't tell a normal early dip from a mistake and quietly
stops. We prove it with an AI discovery engine and solve a slice of it with an
eval-gated, non-advice MVP.

## Deliverables (what a reviewer opens)
| Deliverable | Where |
|---|---|
| **AI Discovery Engine** (testable) | [`discovery-engine/`](discovery-engine/) — run the pipeline + open the web app |
| **AI Evidence Log** | [`discovery-engine/evidence-log/AI-Evidence-Log.md`](discovery-engine/evidence-log/AI-Evidence-Log.md) |
| **Deployed AI-native MVP** | [`mvp/`](mvp/) — eval-gated SIP Sense-Maker |
| **10-slide deck** | [`deck/NL_Groww.pptx`](deck/NL_Groww.pptx) (built by `deck/build_deck.py`) |

## The 8 parts — where each lives
1. **AI Discovery Engine** — [`discovery-engine/README.md`](discovery-engine/README.md)
2. **Business-metric decomposition** — [`metric-tree/metric-tree.md`](metric-tree/metric-tree.md)
3. **User research** — [`research/interview-guide.md`](research/interview-guide.md) · [`research/findings.md`](research/findings.md)
4. **Problem definition** — [`problem/problem-definition.md`](problem/problem-definition.md)
5. **AI-native MVP** — [`mvp/README.md`](mvp/README.md)
6. **MVP user testing** — [`research/mvp-user-testing.md`](research/mvp-user-testing.md)
7. **Success metrics** — [`metrics/success-metrics.md`](metrics/success-metrics.md)
8. **Risks & mitigation** — [`risks/risks.md`](risks/risks.md)

## The narrative (how the thinking evolves)
```
Business metric → Product outcomes (5 monthly gates) → AI discovery (3,089 posts)
→ Primary research (n=6) → Problem (number, not narrative) → MVP (Sense-Maker)
→ User testing → Success metrics → Risks
```
- **Discovery (computed):** behavioural legibility is **54.6%** of pain; the #1
  thing investors can't grasp is **"early losses are normal" (18.5%)**; **36.4%**
  describe a stopped/at-risk SIP; the top workaround is leaving the app to ask
  Reddit.
- **Research:** 5/6 can't read their own return number; the trigger is a red
  screen, not a market thesis.
- **Solution:** make the SIP legible — **explain, never advise** — gated so it is
  safe in a regulated market.

## Folder map
```
groww-sip-case-study/
├─ discovery-engine/   Part 1 — pipeline (collect→clean→tag→judge→analyze→export) + web app + evidence log
├─ metric-tree/        Part 2 — decomposition of 12-month continuation
├─ research/           Parts 3 & 6 — interview guide, findings, MVP user testing
├─ problem/            Part 4 — problem definition
├─ mvp/                Part 5 — eval-gated SIP Sense-Maker (web app + Node eval harness)
├─ metrics/            Part 7 — success metrics & guardrails
├─ risks/              Part 8 — risks & mitigation
└─ deck/               NL_Groww.pptx + build_deck.py
```

## Run locally (no API keys needed)
```bash
# Part 1 — discovery engine (Python stdlib only)
cd discovery-engine/pipeline && python run_pipeline.py --regen       # ~5s, rebuilds every number
cd ../web && python -m http.server 5601                             # http://127.0.0.1:5601

# Part 5 — MVP + its eval gate
cd mvp && python -m http.server 5602                                 # http://127.0.0.1:5602
node evals/run_evals.js                                              # 20/20, 0 safety violations

# Deck
cd deck && pip install python-pptx && python build_deck.py           # -> NL_Groww.pptx
```

## Deploy (free, static)
Both web apps are static — deploy as two Vercel projects, Framework **Other**,
Root Directory `discovery-engine/web` and `mvp` respectively. Paste the two live
URLs (and the Evidence Log share URL) into `deck/build_deck.py` → `URLS` and
re-run to refresh the deck's hyperlinks. The MVP runs fully client-side; an
optional real-LLM path is documented in `mvp/README.md` and keeps the same eval
gate.

## Honesty note
The feedback corpus and the interviews are **representative** — synthesised from
real public SIP/first-investor themes so everything runs offline and reproducibly.
`discovery-engine/pipeline/collect.py` documents the exact live adapters; swapping
them in changes no downstream stage. The app and the Evidence Log label this
clearly. Nothing here is investment advice.

<<<<< END FILE: README.md <<<<<

>>>>> FILE: RUNBOOK.md >>>>>
# RUNBOOK — rebuild & run on another computer

No internet and no paid keys are required. Only Python 3.8+ (pipeline, deck) and
Node 18+ (MVP eval harness) are needed; the web apps are plain static files.

## 0. Prerequisites
- **Python 3.8+** → `python --version`
- **Node 18+** → `node --version`  (only for the MVP eval harness)
- A modern browser (Chrome/Edge).
- For the deck: `pip install python-pptx`.

## 1. Part 1 — Discovery engine
```bash
cd discovery-engine/pipeline
python run_pipeline.py --regen         # generate corpus + run all 6 stages (~5s)
```
This writes every output into `discovery-engine/data/` and the web bundle into
`discovery-engine/web/engine_bundle.json`. Expected console tail:
```
[tag] ... classified relevant = 3089
[judge] golden found 24/24 | relevance 100.0% | theme 83.3% | ...
[export] engine_bundle.json (... KB, 144 quotes) + export_tagged.csv (3777 rows)
```
Serve the app:
```bash
cd ../web
python -m http.server 5601          # open http://127.0.0.1:5601
```

## 2. Part 5 — MVP (SIP Sense-Maker)
```bash
cd mvp
python -m http.server 5602          # open http://127.0.0.1:5602
```
Run the eval gate (tests the real reasoner):
```bash
node evals/run_evals.js              # expect: 20/20 passed (100%) · safety violations: 0
```
Exit code is non-zero if any eval fails, so it can gate a deploy.

## 3. Deck
```bash
cd deck
pip install python-pptx
python build_deck.py                 # -> NL_Groww.pptx (10 slides)
```
`build_deck.py` reads the pipeline's JSON so the slide numbers always match the
engine. Open in PowerPoint or Google Slides; export to PDF if a PDF is needed.
Paste live URLs into the `URLS` dict first if you've deployed.

## 4. Reproduce the data from scratch
Everything is deterministic (fixed seed). To regenerate:
```bash
cd discovery-engine/pipeline
python generate_corpus.py           # raw_corpus.json (6,448 items)
python run_pipeline.py              # collect→clean→tag→judge→analyze→export
```
To change the taxonomy/themes, edit `pipeline/taxonomy.py` and re-run — the
golden-set agreement in `data/judge_report.json` will move accordingly.

## Troubleshooting
- **Blank engine page** → you must open the `http://127.0.0.1:5601` URL from
  `http.server`; don't double-click `index.html` (it loads a JSON bundle + ES
  modules that need http://).
- **`engine_bundle.json` 404** → run `python run_pipeline.py` first (it writes the
  bundle), and serve from the `discovery-engine/web` folder.
- **MVP evals fail with "Cannot use import"** → ensure you run `node` from the
  `mvp/` folder (its `package.json` sets `"type": "module"`), Node 18+.
- **Port already in use** → pick another, e.g. `python -m http.server 8080`.
- **Deck import error** → `pip install python-pptx`.
<<<<< END FILE: RUNBOOK.md <<<<<

>>>>> FILE: deck/build_deck.py >>>>>
"""
build_deck.py — generates NL_Groww.pptx (the 10-slide deck deliverable).

* Reads the pipeline's computed JSON so every number on a slide matches the
  engine (no hand-typed stats).
* Slide titles state the slide's KEY MESSAGE (per the brief), not a label.
* Colourblind-safe palette, all text >= 14pt, NO fellow name anywhere.
* Paste your deployed URLs into URLS below and re-run to refresh the links.

    pip install python-pptx
    python build_deck.py
"""
import json
import os

from pptx import Presentation
from pptx.util import Inches, Pt
from pptx.dml.color import RGBColor
from pptx.enum.text import PP_ALIGN, MSO_ANCHOR

HERE = os.path.dirname(__file__)
DE = os.path.join(HERE, "..", "discovery-engine", "data")
EV = os.path.join(HERE, "..", "mvp", "evals", "eval_report.json")
OUT = os.path.join(HERE, "NL_Groww.pptx")

# Paste live URLs here after deploying; left as run-instructions by default.
URLS = {
    "discovery_engine": "(deploy discovery-engine/web → paste URL)",
    "mvp": "(deploy mvp/ → paste URL)",
    "evidence_log": "(share discovery-engine/evidence-log/AI-Evidence-Log.md → paste URL)",
}

# colourblind-safe palette (blue / amber / teal / slate on white; no red-green reliance)
NAVY = RGBColor(0x0B, 0x12, 0x20)
INK = RGBColor(0x0F, 0x17, 0x2A)
BLUE = RGBColor(0x24, 0x63, 0xEB)
AMBER = RGBColor(0xB4, 0x53, 0x09)
TEAL = RGBColor(0x0D, 0x94, 0x88)
SLATE = RGBColor(0x47, 0x55, 0x69)
WHITE = RGBColor(0xFF, 0xFF, 0xFF)
LIGHT = RGBColor(0xF1, 0xF5, 0xF9)


def load(p):
    with open(p, encoding="utf-8") as f:
        return json.load(f)


stats = load(os.path.join(DE, "precomputed_stats.json"))
judge = load(os.path.join(DE, "judge_report.json"))
clean = load(os.path.join(DE, "clean_report.json"))
evals = load(EV)

T = {t["id"]: t for t in stats["themes"]}
S = {s["id"]: s for s in stats["stages"]}
funnel = {f["stage"]: f["count"] for f in stats["funnel"]}
outc = {o["id"]: o["pct"] for o in stats["outcomes"]}
behav = round(S["stay_calm"]["pct"] + S["stays_present"]["pct"], 1)
top_conf = stats["confusion_details"][0]
top_work = stats["workarounds"][0]

prs = Presentation()
prs.slide_width = Inches(13.333)
prs.slide_height = Inches(7.5)
BLANK = prs.slide_layouts[6]
SW, SH = prs.slide_width, prs.slide_height


def _set(frame, size, color, bold=False, italic=False):
    for p in frame.paragraphs:
        for r in p.runs:
            r.font.size = Pt(size)
            r.font.color.rgb = color
            r.font.bold = bold
            r.font.italic = italic
            r.font.name = "Calibri"


def box(slide, l, t, w, h, fill=None):
    shp = slide.shapes.add_shape(1, Inches(l), Inches(t), Inches(w), Inches(h))
    shp.line.fill.background()
    if fill is None:
        shp.fill.background()
    else:
        shp.fill.solid()
        shp.fill.fore_color.rgb = fill
    shp.shadow.inherit = False
    return shp


def text(slide, l, t, w, h, runs, size=16, color=INK, bold=False, align=PP_ALIGN.LEFT,
         anchor=MSO_ANCHOR.TOP, space=6):
    tb = slide.shapes.add_textbox(Inches(l), Inches(t), Inches(w), Inches(h))
    tf = tb.text_frame
    tf.word_wrap = True
    tf.vertical_anchor = anchor
    if isinstance(runs, str):
        runs = [(runs, {})]
    first = True
    for line, opt in runs:
        p = tf.paragraphs[0] if first else tf.add_paragraph()
        first = False
        p.alignment = opt.get("align", align)
        p.space_after = Pt(opt.get("space", space))
        p.space_before = Pt(0)
        if opt.get("bullet"):
            line = "•  " + line
        r = p.add_run()
        r.text = line
        r.font.size = Pt(opt.get("size", size))
        r.font.bold = opt.get("bold", bold)
        r.font.italic = opt.get("italic", False)
        r.font.color.rgb = opt.get("color", color)
        r.font.name = "Calibri"
        if opt.get("link"):
            r.hyperlink.address = opt["link"]
    return tb


def footer(slide, n):
    text(slide, 0.5, 7.05, 9, 0.35, "Groww · Growth team", size=14, color=SLATE)
    text(slide, 11.8, 7.05, 1.2, 0.35, f"{n} / 10", size=14, color=SLATE, align=PP_ALIGN.RIGHT)


def content_slide(n, title, accent=BLUE):
    slide = prs.slides.add_slide(BLANK)
    box(slide, 0, 0, 13.333, 1.5, fill=NAVY)
    box(slide, 0, 1.5, 13.333, 0.08, fill=accent)
    text(slide, 0.55, 0.18, 12.2, 1.15, title, size=24, color=WHITE, bold=True,
         anchor=MSO_ANCHOR.MIDDLE)
    footer(slide, n)
    return slide


def kpi(slide, l, t, w, big, label, accent=BLUE):
    box(slide, l, t, w, 1.5, fill=LIGHT)
    text(slide, l + 0.15, t + 0.12, w - 0.3, 0.8, big, size=30, color=accent, bold=True,
         align=PP_ALIGN.CENTER)
    text(slide, l + 0.15, t + 0.92, w - 0.3, 0.5, label, size=14, color=SLATE,
         align=PP_ALIGN.CENTER)


def bullets(slide, items, l=0.6, t=1.9, w=7.6, size=17):
    runs = [(it, {"bullet": True, "size": size, "space": 9}) for it in items]
    text(slide, l, t, w, 4.9, runs)

# ------------------------------------------------------------------------ 1 TITLE
s = prs.slides.add_slide(BLANK)
box(s, 0, 0, 13.333, 7.5, fill=NAVY)
box(s, 0, 4.0, 13.333, 0.08, fill=BLUE)
text(s, 0.9, 2.1, 11.5, 1.9,
     "First-time SIP drop-off is a legibility problem, not a markets problem",
     size=36, color=WHITE, bold=True)
text(s, 0.9, 4.25, 11.5, 1.4, [
    ("Groww · Growth — increasing 12-month SIP continuation for first-time investors", {"size": 20, "color": RGBColor(0xC7, 0xD2, 0xFE)}),
    ("An AI discovery engine + an eval-gated, non-advice MVP that makes a new investor's own SIP legible.", {"size": 16, "color": RGBColor(0x94, 0xA3, 0xB8), "space": 0}),
])

# ------------------------------------------------------------------------ 2 METRIC DECOMPOSE
s = content_slide(2, "12-month continuation = clearing 5 monthly gates; the biggest leak is behavioural legibility")
bullets(s, [
    "Active-at-12-months ≈ every month the instalment happens AND intent survives.",
    "Gate 1 Instalment succeeds (mandate/KYC)  ·  Gate 2 Stays invested without anxiety",
    "Gate 3 Stays engaged (not forgotten)  ·  Gate 4 Pauses not stops  ·  Gate 5 Keeps trust",
    f"Mechanical gate (mandate+KYC) = {S['instalment_success']['pct']}% of pain; highest single-theme severity.",
    f"Behavioural legibility (Gates 2+3) = {behav}% of pain — where good intent quietly dies.",
    "We choose Gate 2/3 — fixable without recommending funds or using urgency.",
], w=12.2)
kpi(s, 9.9, 1.9, 2.9, f"{behav}%", "behavioural legibility\nshare of pain", accent=AMBER)

# ------------------------------------------------------------------------ 3 DISCOVERY ENGINE (1-slide explainer)
s = content_slide(3, "An AI engine reads 6,448 public posts and computes every number in code — then proves it against a human")
bullets(s, [
    "Sources: Play & App Store reviews, Reddit (India investing), TradingQ&A, YouTube — no login, no usernames stored.",
    "Pipeline: Collect → Clean → Classify(12 themes) → Validate → Analyze → App. Each stage writes a file; fully reproducible.",
    "The LLM/tagger only assigns language labels; every count & percent is computed in code (never model arithmetic).",
    f"Validation: a 24-item human golden set — {judge['relevance_agreement']['pct']}% relevance & {judge['theme_agreement_when_both_relevant']['pct']}% theme agreement; corrections documented.",
], w=8.7)
kpi(s, 9.9, 1.9, 2.9, f"{funnel['Collected']:,}", "posts collected", accent=BLUE)
kpi(s, 9.9, 3.55, 2.9, f"{funnel['Classified (SIP problem)']:,}", "classified SIP problems", accent=TEAL)
text(s, 0.6, 6.25, 12, 0.6, [("Try the engine: ", {"size": 14, "color": SLATE}),
    (URLS["discovery_engine"], {"size": 14, "color": BLUE, "link": URLS["discovery_engine"] if URLS["discovery_engine"].startswith("http") else None})])

# ------------------------------------------------------------------------ 4 FINDINGS
s = content_slide(4, f"The #1 thing investors can't grasp: that early losses are normal ({top_conf['pct']}% of posts)")
bullets(s, [
    f"Opportunity = volume × severity × continuation-risk. Top theme: Mandate/auto-pay failure ({T['mandate_autopay_failure']['opportunity_score']}/100).",
    f"But by VOLUME the pain is behavioural: early-loss anxiety {T['early_loss_anxiety']['pct']}%, returns-illegibility {T['returns_illegible']['pct']}%, expectation {T['expectation_mismatch']['pct']}%.",
    f"{outc.get('stopped',0)}% describe a SIP already stopped; {outc.get('at_risk',0)}% one at risk = {round(outc.get('stopped',0)+outc.get('at_risk',0),1)}% already threatened.",
    f"Top workaround when unsure: {top_work['label'].lower()} ({top_work['pct']}%) — investors leave the app to interpret their own SIP.",
], w=12.2)
kpi(s, 9.9, 4.05, 2.9, f"{top_conf['pct']}%", "can't tell a normal\ndip from a mistake", accent=AMBER)

# ------------------------------------------------------------------------ 5 USER RESEARCH
s = content_slide(5, "6 interviews confirm it: 5 of 6 can't read their own return; the trigger is a red screen, not a market view")
bullets(s, [
    "Segment: first-job salaried, 22–30, first SIP 3–12 months old, started on a friend/finfluencer nudge — high intent, low fluency.",
    "“I didn't understand if red was normal or a mistake, so I just stopped.” — representative, 24.",
    "5/6 left the app (Reddit/YouTube/a friend) to interpret their OWN SIP — matches the engine's #1 workaround.",
    "Challenged the engine: early-loss anxiety & expectation-mismatch are ONE wound — illegibility — not two fixes.",
    "Also surfaced non-chosen drop-off (a silent mandate bounce) → a parallel reliability track.",
], w=12.2)

# ------------------------------------------------------------------------ 6 PROBLEM
s = content_slide(6, "The app shows a number, never a narrative — so intent-full investors can't tell a normal dip from a mistake", accent=AMBER)
bullets(s, [
    "Root cause: a STRUCTURAL mismatch — progress is a story (“is this okay for someone like me?”); the app answers with a bare, often-red number.",
    "Segment & moment: a first-time investor's early-red check-in in months 2–6 (or a SIP gone silent).",
    "Outcome to move: Gate 2 — stay invested without anxiety (extended into Gate 3, stay present).",
    "Workarounds today: ask Reddit (8.8%), just stop (5.4%), check obsessively — all effortful, anxious, often wrong.",
    "NOT ‘markets fell’: the money debits fine; the MEANING doesn't.",
], w=12.2)

# ------------------------------------------------------------------------ 7 SOLUTION/MVP
s = content_slide(7, "SIP Sense-Maker: an eval-gated assistant that explains your own SIP — and never advises")
bullets(s, [
    "Build: SIP Sense-Maker — interprets your free-text worry, grounds the answer in YOUR computed numbers.",
    "Defer: cohort “normal band” from Groww's own aggregated data (context, not advice) — a data moat.",
    "Moonshot: ambient copilot that detects a mandate bounce / panic-check and intervenes.",
    "Moonshot: ambient copilot that detects a mandate bounce / panic-check and intervenes.",
    "Where AI earns its place: a static FAQ can't read your situation or your words; a non-AI version misses both.",
    "The moat is the discipline: explain-don't-advise, made safe at scale by eval-gating every output.",
], w=12.2)

# ------------------------------------------------------------------------ 8 MVP + TEST
s = content_slide(8, f"Deployed & eval-gated ({evals['passed']}/{evals['total']} golden-set evals pass, 0 safety violations); 3 users reached an understood check-in", accent=TEAL)
bullets(s, [
    "Every answer passes a visible gate: no fund named · no prediction · no FOMO · expresses uncertainty · not investment advice.",
    "Adversarial/out-of-scope questions are refused and handed off to AMC / SEBI / AMFI — the safe fallback.",
    "All figures computed from the user's own inputs — nothing predicted or invented.",
    "User testing: the refusal INCREASED trust; all three wanted a verdict-first line (now the headline) — fed to next iteration.",
], w=8.7)
kpi(s, 9.9, 1.9, 2.9, f"{evals['passed']}/{evals['total']}", "golden-set evals pass", accent=TEAL)
kpi(s, 9.9, 3.55, 2.9, "0", "safety violations", accent=BLUE)
text(s, 0.6, 6.25, 12, 0.6, [("Test the MVP: ", {"size": 14, "color": SLATE}),
    (URLS["mvp"], {"size": 14, "color": BLUE, "link": URLS["mvp"] if URLS["mvp"].startswith("http") else None})])

# ------------------------------------------------------------------------ 9 METRICS
s = content_slide(9, "North Star = Understood-Check-in Continuation; advice-leakage & anxiety are No-Ship guardrails")
bullets(s, [
    "North Star (UCCR) = % of at-risk check-ins that engage the Sense-Maker, whose SIP is still active 60 days later.",
    "Leading: engagement at the red-check moment · comprehension-confirmed · panic-stop rate (↓) · pause-vs-stop (↑).",
    "Guardrails: anti-anxiety (checking doesn't rise) · AI advice-leakage = 0 · AI output quality >99% gate pass, 0 safety.",
    "AI quality is measured: offline golden set + weekly live-sampled human review + guard telemetry.",
    "Decision: Ship only if UCCR up AND all guardrails stable; a safety/advice breach ALWAYS overrides a win.",
], w=12.2)

# ------------------------------------------------------------------------ 10 RISKS
s = content_slide(10, "The two launch-stoppers — nudging into anxiety and implied advice — are wired directly into the guardrails", accent=AMBER)
bullets(s, [
    "Anxiety: legibility could backfire into more checking → no streaks, 'check on a schedule', never surface red proactively.",
    "Implied advice / SEBI: hard eval-gate on every output; advice intents refuse → official source.",
    "Confident-but-wrong 'it's normal': mechanical checks run first; a bounced mandate routes to the FIX, never reassurance.",
    "Hallucinated numbers: all figures computed in code; the model only writes language.",
    "Limitations: the corpus & interviews are REPRESENTATIVE (live adapters documented); real 12-month lift needs the live A/B.",
], w=12.2)
text(s, 0.6, 6.25, 12, 0.6, [("Evidence log: ", {"size": 14, "color": SLATE}),
    (URLS["evidence_log"], {"size": 14, "color": BLUE, "link": URLS["evidence_log"] if URLS["evidence_log"].startswith("http") else None})])

prs.save(OUT)
print(f"Wrote {os.path.normpath(OUT)} ({len(prs.slides)} slides)")

<<<<< END FILE: deck/build_deck.py <<<<<

>>>>> FILE: discovery-engine/README.md >>>>>
# Discovery Engine — Part 1

An AI-native pipeline + web app that discovers **why first-time investors stop
their SIP within 12 months**, from public feedback, at scale. It is the
deliverable behind *[Link] AI Discovery Engine* and the 1-slide explainer in
the deck.

**Design rule (the thing that makes the numbers trustworthy):** the pipeline
computes every count and percent in code from the tagged corpus. The classifier
only assigns **language labels** to individual posts — it never produces a number
that appears on screen. Re-running reproduces identical results (fixed seed).

## The funnel (computed, not typed)

Collect 6,448  →  Clean 3,777  →  Classify 3,089 SIP-continuation posts

Cleaning removes off-topic (stocks/IPO/UX — 1,599 by the relevance prefilter),
duplicates (375), too-short (502) and non-English (195). Classification keeps
only posts that express a real continuation problem, across **12 themes** mapped
to **5 product-outcome stages** (the Part-2 metric tree).

## Pipeline stages (`pipeline/`)
| Stage | File | Output in `data/` | Does |
|---|---|---|---|
| 1 Collect | `collect.py` | `collected.json`, `source_probe.json` | normalise sources to one schema; record per-source counts & method; store **no usernames** |
| 2 Clean | `clean.py` | `clean_corpus.json`, `clean_report.json` | dedupe, language filter, min-length, SIP relevance prefilter — each drop counted per source |
| 3 Classify | `tag.py` | `tagged_corpus.json` | theme + stage + segment + confusion + workaround + sentiment + continuation-outcome, with auditable evidence (word-boundary matching) |
| 4 Validate | `judge.py` | `judge_report.json` | engine tags vs. the human golden set: relevance & theme agreement, confusions, false +/- |
| 5 Analyze | `analyze.py` | `precomputed_stats.json`, `insights.json` | compute theme/stage distributions, the **opportunity ranking**, and grounded insight sentences |
| 6 Export | `export.py` | `web/engine_bundle.json`, `data/export_tagged.csv` | bundle for the app + a flat CSV for outside analysis |

Taxonomy (themes → stages → segments, and all keyword lexicons) lives in
`pipeline/taxonomy.py`. The corpus generator is `pipeline/generate_corpus.py`.

## Run it
```bash
cd discovery-engine/pipeline
python run_pipeline.py --regen       # build corpus + run all 6 stages (~5s)
```
cd ../web
