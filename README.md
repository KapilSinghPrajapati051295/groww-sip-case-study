# Groww — First-time SIP 12-Month Continuation

**Product selected:** Groww (independent product-management case study; no affiliation). **Goal:** improve the share of first-time SIP investors with an active SIP 12 months after starting. **Hypothesis:** returns legibility and early-screen anxiety can create avoidable continuation loss, separate from failed payments.

## Submission items

| Requirement | Deliverable | How to use |
| --- | --- | --- |
| Choose any ONE product | **Groww** | Select Groww in the form |
| AI Discovery Engine + 1-slide workflow explanation | [`discovery-engine/web/`](discovery-engine/web/) + **slide 3** of the deck | Test dashboard and grounded question flow; publish with GitHub Pages |
| 10-slide PDF deck | [`deck/NL_Groww_10_Slides.pdf`](deck/NL_Groww_10_Slides.pdf) | Upload this **PDF**, not the PPTX |
| Deployed AI-native MVP | [`mvp/`](mvp/) | Interactive, eval-gated **offline demo**; must publish to claim publicly deployed |
| AI Evidence Log, viewable document | [`discovery-engine/evidence-log/AI-Evidence-Log.md`](discovery-engine/evidence-log/AI-Evidence-Log.md) | Link to the public repo or GitHub Pages `/evidence-log/` |

The full editable presentation is [`deck/NL_Groww.pptx`](deck/NL_Groww.pptx). The public-ready combined site is in [`docs/`](docs/) and contains an entry page, Discovery Engine, MVP, and HTML Evidence Log. `SUBMISSION_CHECKLIST.md` gives the final paste/upload order; `DEPLOYMENT.md` gives git and GitHub Pages steps.

## The 8 case-study parts

1. **AI Discovery Engine:** [`discovery-engine/README.md`](discovery-engine/README.md), six-stage Python pipeline, 12 themes, grounded Q&A and visible evidence.
2. **Metric decomposition:** [`metric-tree/metric-tree.md`](metric-tree/metric-tree.md).
3. **Research design:** [`research/interview-guide.md`](research/interview-guide.md) and [`research/findings.md`](research/findings.md).
4. **Problem definition:** [`problem/problem-definition.md`](problem/problem-definition.md).
5. **SIP Sense-Maker MVP:** [`mvp/README.md`](mvp/README.md) and `src/reasoner.js`.
6. **Testing plan:** [`research/mvp-user-testing.md`](research/mvp-user-testing.md).
7. **Success metrics:** [`metrics/success-metrics.md`](metrics/success-metrics.md).
8. **Risks & mitigation:** [`risks/risks.md`](risks/risks.md).

## Local run (no API keys)

```bash
cd discovery-engine/pipeline
python run_pipeline.py --regen
cd ../web
python -m http.server 5601
# in a separate terminal:
cd mvp
python -m http.server 5602
# in another terminal:
cd mvp
node evals/run_evals.js
```

Visit **http://localhost:5601** (discovery) and **http://localhost:5602** (MVP). From root, run `python -m http.server 5600 --directory docs` to preview the full submission site at **http://localhost:5600**. Building the deck requires `python-pptx`; `python deck/build_deck.py` regenerates the 10-slide PPTX, then export PDF with LibreOffice/PowerPoint.

## Reproducible demonstration numbers (not empirical findings)

- Generated fixture 6,448 → clean 3,777 → topic-tagged 3,089.
- Illustration: calm/present gates together 54.6%, early-loss confusion 18.5%, stopped/at-risk labels 36.4%, Ask Reddit workaround 8.8%.
- Hand-authored reference comparison: 24/24 relevance and 20/24 theme label matches, not independent human validation.
- MVP local functional test: 20/20 developer-authored cases pass, with 0 violations of the five implemented output rules.

**Important integrity note:** The corpus, source labels, six interviews and three usability-test stories are **synthetic/representative**. No original real customer interviews, live scraped feedback or production retention experiment were provided. The two applications use deterministic rule-based logic to demonstrate an AI-native *design workflow*; **neither makes live LLM calls**. No claims of real impact, regulator-approved advice safety or public deployment should be inferred. Read the Evidence Log for what was and was not verified.

## GitHub Pages

1. Upload this project to a **public** GitHub repository.
2. Settings → Pages → Deploy from a branch: `main`, folder `/docs`; Save.
3. Confirm your real live site first. If the site base is `https://USERNAME.github.io/REPO/`, submit:
   - Discovery Engine: `https://USERNAME.github.io/REPO/engine/`
   - MVP: `https://USERNAME.github.io/REPO/mvp/`
   - Evidence Log: `https://USERNAME.github.io/REPO/evidence-log/`
4. Put the verified URLs into `deck/build_deck.py` (the `URLS` mapping) and rebuild/export the PDF **before uploading it**.

No user credentials or paid API keys are required to run these demos. Avoid putting any real investor data into a public repository.
"# groww-sip-case-study" 
