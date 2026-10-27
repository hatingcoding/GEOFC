# GEO Phase 2 Prototype

Static site for the GEO Phase 2 prototype (IFN736, Group 22). Deployed on GitHub Pages at
**https://elllllllle.github.io/ifn736-geo-project/**

- `/` — findings dashboard, grouped into three parts: **Part 1 — The Results** (headline mention
  rates, journey stage & competitors), **Part 2 — The Evidence** (pooled significance, run-by-run
  consistency across 4 team members, and a follow-up test on whether rewording the P2 FAQ-only
  page moves the needle further), **Part 3 — What It Means** (key takeaways, recommendations,
  limitations & caveats)
- `/chat/` — interactive chat demo — ask a travel question, compare Baseline vs Optimised
  (content-injected) responses from Gemini, with live Inclusion Rate / Ranking Position /
  rubric-score metrics per turn
- `/mockups/` — the 10 Flight Centre GEO mockup site variants used for V3 testing: an Incremental
  Comparison Ladder (Site A → V1 → V2 → Site B → V4) plus Isolated Technique Variants (P2, the
  restructured P2.1, P3, P4, P5), with a directory page linking to each
- `/queries/` — the 19 multi-turn test conversations run against every page variant, grounded in
  Flight Centre's Customer Persona Book and mapped to the Dream → Plan → Engage → Book (→ Pre-trip)
  journey

## User guide

This site presents the findings of a QUT student research project with Flight Centre on generative AI optimisation (GEO): how the design of a product page affects whether AI assistants name and recommend Flight Centre. The full findings and recommendations are in the *GEO Guide: What Actually Helps*, supplied separately.

### The four pages

| Page | Address | What it shows |
|---|---|---|
| Findings | https://elllllllle.github.io/ifn736-geo-project/ | The results: how often Gemini named Flight Centre with no help, with live search and after reading each mock-up page; results by journey stage and by test run; recommendations and limitations |
| Chat Demo | https://elllllllle.github.io/ifn736-geo-project/chat/ | A live chat with Gemini that shows, for each answer, whether Flight Centre was named |
| Mockup Sites | https://elllllllle.github.io/ifn736-geo-project/mockups/ | The 10 mock-up Flight Centre pages used in testing |
| Query Set | https://elllllllle.github.io/ifn736-geo-project/queries/ | The 19 traveller conversations used in every test |

All four pages are linked from the menu at the top of each page.

### Using the chat demo

1. **Get a free Gemini API key** at https://aistudio.google.com/app/apikey and paste it into box 1. The key stays in your browser and goes only to Google. It isn't saved, so you'll need to paste it again if you reload the page.
2. **Choose a mode:**
   - **Baseline:** Gemini answers with nothing added, the way most people use it today.
   - **Optimised:** Gemini first reads Flight Centre's Full composite mock-up page (`mockups/04_site_b_full.html`), as an AI assistant reading that page would. Click *View the actual page Gemini reads in Optimised mode* to open it, or *Show what was given to the AI* to see the exact text.
3. **Type a travel question** and press Send. Follow-up questions continue the same conversation.
4. **Read the scores under each answer:**
   - **Inclusion:** whether "Flight Centre" appears in the answer. Checked directly against the text.
   - **Ranking position:** where Flight Centre appears among the brands named (1st = named before any competitor).
   - **Relevance to Trustworthiness (0 to 3):** quality scores given by Gemini judging its own answer. These haven't been checked by people, so treat them as a guide only.
5. **Compare the two modes:** click *New conversation*, switch mode and ask the same question. The mode can't be changed partway through a conversation.
6. *Copy transcript* copies the whole conversation so you can save or share it.

Each question uses two requests on your key (the answer, then the scoring), so free-tier limits are reached sooner than in a normal chat. If you see a "try again" message, wait a minute and resend.

### The mock-up pages

Each page carries the same 39 Flight Centre products from the ProCat export. Each one starts from the same plain page and changes only what's listed.

| Page | File | What it adds to the plain page |
|---|---|---|
| Baseline | `01_site_a_baseline.html` | Nothing: products as plain text cards |
| Schema only | `02_v1_schema_only.html` | Schema markup (hidden labels in the page code describing the agency, products and offers) |
| Schema + FAQ | `03_v2_schema_faq.html` | Schema and an FAQ section |
| Full composite | `04_site_b_full.html` | Schema and FAQ, plus a summary, a one-line quick answer per product, a trust bar, star class, review scores, promotion tags, and an SEO title and description |
| Full composite + tables | `05_v4_full_tables.html` | Everything in Full composite, plus comparison and policy tables |
| FAQ only | `06_p2_faq_only.html` | An FAQ section on package types, the loyalty program, why to book with Flight Centre, stopovers, guided tours, ski and snow, cruises and expeditions, and how to book |
| Reworded FAQ | `06_p2_faq_only_v3_restructured.html` | The FAQ only page rewritten in customers' own words, with the same topics and facts |
| Statistics only | `07_p3_stats_only.html` | A statistics bar: 40+ years, 2,000+ tours a month, 200+ countries, ATAS accredited |
| Tables only | `08_p4_tables_only.html` | Comparison tables |
| Citations only | `09_p5_citations_only.html` | Quotes credited to named outside sources |

### Please note

- These are **research prototypes, not official Flight Centre pages**. Product details come from a ProCat sample. Review scores and counts are randomly generated, and the $299 deposit and cancellation terms are illustrative. None of these figures should be published.
- The pages are hidden from search engines and carry a notice saying they are research prototypes.
- **The test scripts and full result files are not in this repository.** They are supplied separately in the testing results ZIP, which has its own README explaining how to run them.
- This site will be made private after the QUT assessment period ends.

## Updating the live site

The repo is already set up and deployed — from this folder, committing and pushing to `main`
updates the live site within a minute or two:

```bash
git add -A
git commit -m "..."
git push origin main
```

GitHub Pages is configured under **Settings → Pages → Build and deployment → Source: Deploy from
a branch → Branch: main / (root)**.

<details>
<summary>First-time setup (already done for this repo — kept for reference)</summary>

```bash
git init
git add .
git commit -m "GEO Phase 2 prototype: dashboard, chat demo, mockup sites"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```

Then on GitHub: **Settings → Pages → Build and deployment → Source: Deploy from a branch →
Branch: main / (root)**. The site goes live at `https://<your-username>.github.io/<repo-name>/`
within a minute or two — dashboard at the root URL, chat demo at `/chat/`, mockup sites at
`/mockups/`, query set at `/queries/`.

</details>

## About the chat demo's API key

The chat page calls the Gemini API directly from browser JavaScript, so each visitor pastes in
their own Gemini API key rather than the site shipping a shared one. The key lives only in that
browser tab for the session (sent straight to Google with each request, never stored or sent
anywhere else) and has to be re-entered on reload. This keeps things simple for a static,
GitHub-Pages-hosted demo, but it does mean each visitor needs their own key and is on the free
tier's rate limits.

If this ever needs to run with one shared key instead (e.g. so visitors don't need their own),
the options are:

1. Keep the repo private (needs a paid GitHub plan for Pages on a private repo).
2. Use a separate, rate-limited key you're fine with someone eventually finding.
3. Put a small server-side proxy in front of it (e.g. a Cloudflare Worker) so the browser never sees the real key.