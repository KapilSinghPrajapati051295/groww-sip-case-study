# RUNBOOK — Rebuild, verify and publish

**Requirements:** Python 3.8+, Node 18+, modern browser; `pip install python-pptx` for slides; LibreOffice or PowerPoint for PDF export. No API keys needed.

## 1. Rebuild data

```bash
cd discovery-engine/pipeline
python run_pipeline.py --regen
```

Expected: generated 6,448; clean 3,777 after exact drops 195 non-Latin, 502 too-short, 375 duplicates and 1,599 irrelevant; tagged 3,089; reference agreement 24/24 relevance, 20/24 theme. **All data is synthetic.**

## 2. Test the MVP

```bash
cd ../../mvp
node evals/run_evals.js
```

Expected: `20/20 passed · safety rule violations: 0`. Reads and scores the real `src/reasoner.js` used by the UI. Not a safety certification.

## 3. Preview

```bash
# from the project root:
python -m http.server 5600 --directory docs
```

Open `http://localhost:5600`, then try the two demos. Check advice refusal with `which fund should I buy?` and a failed mandate with the dedicated demo case.

## 4. Rebuild the 10-slide editable deck, export PDF

```bash
pip install python-pptx
python deck/build_deck.py
libreoffice -env:UserInstallation=file:///tmp/lo_groww_case --headless --convert-to pdf --outdir deck deck/NL_Groww.pptx
```

The deck PDF can be renamed to `NL_Groww_10_Slides.pdf`. It should have exactly 10 pages; inspect all pages for text clipping. Always paste verified public URLs into `URLS` inside the deck builder before rebuilding for final submission.

## 5. GitHub Pages publication

Use `DEPLOYMENT.md`. The `/docs` folder is the GitHub Pages site source, holding `engine`, `mvp`, and `evidence-log`. GitHub requires repository creation and publishing access; local generation alone cannot produce real public links.

## 6. Known limitations

Author-authored fixture and golden references, not live sourcing or independent annotation; scripted rather than live interviews; deterministic classifier and controlled response templates, not a live LLM; no production A/B measurement or regulatory approval. Keep these limitations visible when presenting the case study.
