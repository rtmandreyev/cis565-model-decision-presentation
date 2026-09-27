# Predict · Explain · Intervene

**Model choice for business decisions**

Prediction, explanation, and causal intervention answer different questions. A model can rank customers accurately and still be the wrong instrument for the decision in front of you. This presentation develops that argument through a single case — personalized promotions — and closes on a practical rule: match the model to the decision, not the reverse.

**View the live presentation:** <https://rtmandreyev.github.io/predict-explain-intervene/>

**Repository:** <https://github.com/rtmandreyev/predict-explain-intervene>

---

## Overview

A twelve-slide Reveal.js deck built with Quarto, with a custom SCSS theme — a title slide and eleven content slides. It stays on one running example from the first slide to the last.

It opens with a single scene: a household scored at an 82% probability of purchase, and the question that follows — should we send the coupon? The deck's answer is that the score cannot settle it, because the score answers a different question.

From there the talk separates three questions that are often conflated:

| Business question | Analytical task |
| --- | --- |
| Will they buy? | **Prediction** — judged out of sample, on customers the model never saw |
| Why this score? | **Explanation** — different audiences need different accounts of the same output |
| Will the coupon change behavior? | **Intervention** — needs a credible counterfactual, not a good forecast |

The deck then works through each in turn. Prediction asks who is most likely to redeem next cycle and argues the real test is unseen data. Explanation traces one model output to three audiences — an analyst, a manager, an auditor — and asks when opacity actually matters, placing a grocery recommendation and a high-stakes decision at different points on a consequence spectrum, which is the ground for Rudin's case for inherently interpretable models. Intervention returns to the coupon and shows why forecast quality cannot answer it.

The discussion is then grounded in a real retail dataset: dunnhumby's *The Complete Journey*, 2,500 frequent-shopper households over two years of transactions, campaigns, coupons, and marketing exposure — enough to observe marketing exposure, not enough to assume causality. The deck's framework follows: start from the decision (forecast → predict, understand → explain, change → intervene). Its conclusion is that no single model wins that competition, because the three roles are complementary tools, and the question worth asking is not "which model is best?" but "best for what decision?"

## The example: likely to buy ≠ likely to be persuaded

The central illustration is a two-customer comparison. Customer A carries a 90% predicted purchase probability and buys anyway — the coupon made no difference, even though the prediction was correct. Customer B carries a 35% predicted probability, and the coupon changes the decision. Ranked by purchase probability, an offer goes to A and skips B; only the estimated effect of the action identifies the customer worth persuading. Predicting behavior is not the same as estimating the effect of an action.

None of these numbers is an empirical result. The opening slide labels its 82% score "ILLUSTRATIVE SCORE" and carries the disclaimer that the illustrative customer and probability are not an empirical result; the 90% and 35% figures on the intervention slide belong to the same hypothetical example. The dataset characteristics come from the dunnhumby documentation. The presentation does not fit, train, or evaluate a model; it is an argument about which kind of model a decision requires.

## Design and implementation

The deck is a dark 1600×900 layout with fixed color semantics carried across every slide: cyan for prediction, violet for explanation, magenta for intervention. Slides are authored as hand-written HTML blocks inside the Quarto source rather than plain Markdown, so each slide's layout can be controlled individually, with fragment-based reveals and hash-addressable slides.

- **Quarto** (1.10.18) with the `revealjs` format
- **Reveal.js** 5.1.0, bundled by Quarto's `revealjs` format
- **Custom SCSS theme** — `theme.scss`, providing the palette, typography, and all per-slide layout rules
- No JavaScript frameworks and no external runtime dependencies

## Running it locally

Requires [Quarto](https://quarto.org). This output was rendered with Quarto 1.10.18.

```bash
git clone https://github.com/rtmandreyev/predict-explain-intervene.git
cd predict-explain-intervene

quarto preview presentation.qmd   # live preview while editing
quarto render presentation.qmd    # writes presentation.html
```

`presentation_files/` is Quarto's generated asset directory and is gitignored, so a fresh clone must be rendered before `presentation.html` will display correctly on its own. To view an already-rendered copy without Quarto, serve the directory over a local server (for example `python3 -m http.server`) and open the HTML — the deck loads its assets relatively.

GitHub Pages publishes the presentation itself at <https://rtmandreyev.github.io/predict-explain-intervene/>. The site is built by a GitHub Actions workflow (`.github/workflows/publish.yml`), which renders `presentation.qmd` with Quarto and deploys the result as the site root; the `presentation_files/` assets are generated during the build and are not committed.

## Sources

Every substantive slide carries an inline citation to the specific source and the page or section supporting the claim. The deck's closing slide holds the full bibliography and is the authoritative reference — Mullainathan & Spiess, *Journal of Economic Perspectives* (2017); Kleinberg, Ludwig, Mullainathan & Obermeyer, *American Economic Review* (2015); NIST AI RMF 1.0 (2023) and NISTIR 8312 (2021); Rudin, *Nature Machine Intelligence* (2019); and the dunnhumby *Complete Journey User Guide*. Each entry on that slide includes its DOI or documentation reference.

## Main files

| File | Role |
| --- | --- |
| `presentation.qmd` | Presentation source — front matter, slide content, inline citations |
| `theme.scss` | Custom SCSS theme: palette, typography, per-slide layout |
| `presentation.html` | Rendered deck (generated by `quarto render`) |

## Context

This is coursework — built for CIS 565 and kept here as a standalone presentation artifact. It presents no original research and fits no models; the arguments are drawn from the cited literature.

