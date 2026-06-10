# Bayes Demos — agent playbook

You (Claude) build **Bayes Impact demos and presentations** in this repo, from a content brief a
teammate gives you (a meeting note, a pitch outline, "make a deck for hospital X", a use case to
show). You produce **one self-contained HTML page**, on the shared Bayes design system, **bilingual
FR/EN**, mobile-readable, PDF-exportable — then publish it. **This file is the contract.** Read it
fully before you start.

The golden rule: **a teammate should be able to point you at a brief and get a beautiful, on-brand,
working demo without touching code.** You do the work. Don't ask them to fill in templates.

---

## 1 · What Bayes is, and how we talk about it

Get this right — every word of copy you write must sound like Bayes. (Sources: www.bayesimpact.org
and www.bayesimpact.org/about/.)

**Who we are.** Bayes Impact is a **nonprofit**, founded in **Silicon Valley in 2014**, now working
across **three continents** (Europe, North America, Africa). We've served **10M+ people**. Funders &
partners include **Google.org, the Gates Foundation, Y Combinator, France Travail, and the U.S.
Department of Veterans Affairs**. We are **open-source** and build **for the public good** — not a
vendor.

**Our mission, the one line everything ladders up to:**
> *L'IA pour aider celles et ceux qui en ont besoin — et celles et ceux qui les accompagnent.*
> *AI to empower people in need — and those who serve them.*

**The Bayes Platform** is our product: an **open-source platform of AI agents for public services**.
What makes it ours, and what you should foreground:
- **Sovereign** — open-source, **hostable locally; your data stays in-house**. No vendor lock-in.
- **No-code** — partner teams **build and deploy agents themselves**, then take over (skills transfer).
- **Trustworthy** — answers are **grounded in your documents (RAG)**: **zero hallucination, sources
  cited**, traceable.
- **A platform, not a patchwork** of point tools — one foundation many services run on.
- For a **government** audience, the platform is positioned as the **"DPI of the agentic government"**
  (Digital Public Infrastructure). Elsewhere: "own your AI / a sovereign AI platform".

**Tone.** Mission-driven, calm, concrete, humble. Be **honest about maturity** — say "à terme",
"future portal", "pilot" when something isn't live. Treat all demo data as **illustrative** (names,
figures, citations are placeholders that need an expert check before a real audience).

**Banned phrasings** (we've moved past these — never use them): ~~"GouvAI"~~, ~~"le service public en
un coup de fil"~~, ~~"digitalisation 360"~~ (Togo-specific), ~~"renforcer"~~ (use *aider* /
*accompagner*). Prefer "digitalisation du pays / IA-natif" over "360".

---

## 2 · The design system (keep it; don't reinvent)

Everything lives in **`lib/bayes.css`** (tokens + components) and **`lib/bayes.js`** (the engine).
**You almost never edit these.** You write **one deck file** that uses the classes below.

**Tokens** (CSS variables, already defined):
| | |
|---|---|
| `--bg` `#F2EFE9` (warm beige) · `--ink` `#000` | page / text |
| `--accent-orange` `#FF8400` | primary accent, highlights, the active state |
| `--accent-blue` `#1067FE` | secondary accent (data / DB) |
| `--gold-bg` `#EBE092` | the `<em class="hl">…</em>` highlighter |
| `--card` `#FFF` · `--border-soft` `#DBCCAF` | cards & borders |
| `--ok` `#1F7A3F` · `--wa-green` `#075E54` | success · WhatsApp chrome |
| `--radius` `14px` · `--shadow` | rounding · elevation |

**Type:** Inter (UI/headings) + JetBrains Mono (labels, code, counters). Loaded in the page `<head>`.

**To re-theme a single deck** (rare), override a token in an inline `<style>` in that deck's `<head>`,
e.g. `:root{ --accent-orange:#0A7E5A; }`. Never edit the shared CSS for one deck.

**Core building blocks** (all styled already — compose them):
`.slide` (a full-screen section; add `data-dark` for a dark slide) · `.slide-inner` (the content
column) · `.reveal` (fades up on scroll) · `.eyebrow` · `.title` / `.big` (headings) · `.lead`
(intro paragraph) · `<em class="hl">` (gold highlight) · `.cards.c3` + `.card` (+ `.kicker`) ·
`.chips`/`.chip` · `.partners-grid` (funder logos) · `.brand-corner` (top-left logo + section label)
· `.cover` (title/closing slide) · the **earth hero** (§5) · the **two demos** (§6).

The slide **chrome** (progress bar, dots, counter, hint, the **FR/EN toggle**, the **PDF button**)
is injected automatically by `bayes.js`. You don't add it.

---

## 3 · Repo layout & the two kinds of content

```
bayes-demos/
├── index.html         splash gate — visitor types a code → /demos/<slug>/
├── lib/  bayes.css · bayes.js          (shared engine — don't edit)
├── assets/  logos/ · planet.webp · partners/   (shared brand assets)
├── demos/
│   ├── _template/index.html   ← copy this to start
│   └── <slug>/index.html      ← each demo / deck
├── CLAUDE.md   (this file)
└── README.md
```

Two content types live side by side — same system, same file shape:
1. **Website-linkable demo pages** — a focused interactive showcase you could embed or link from
   bayesimpact.org (e.g. an employment assistant, a civil-status service on WhatsApp).
2. **Partner decks** — a presentation shown or shared to a partner (a ministry, a hospital, a
   foundation): intro → vision → use cases → demos → team → thanks.

Pick the emphasis from the brief; the components are the same.

---

## 4 · How to make a variant (the workflow)

1. **Read the brief.** Identify: audience (ministry / hospital / foundation / board), the message,
   the **1–2 use cases to demo**, the partner/org name, and any domain facts (services, languages,
   payment provider, sectors). Handle **any** domain — government, healthcare, nonprofit, education.
2. **Copy the template** to a new slug folder:
   ```bash
   cp -r demos/_template demos/<slug>     # slug = kebab-case, e.g. benin-platform, charite-health
   ```
3. **Edit only `demos/<slug>/index.html`.** Set the `<title>`, rewrite the slides for the brief, and
   rewrite the demo JSON (§6). Keep the slide structure in §5 as your spine; the use-case middle is
   yours to shape.
4. **Verify** (§7): run a preview, walk every slide at desktop **and** mobile, confirm both demos
   animate, the FR/EN toggle works, and the PDF export shows demos finished. Console must be clean.
5. **Publish** (§8) and give the teammate the URL + the access code (the slug).

---

## 5 · The canonical slide structure

This is the Bayes narrative spine. Keep the bookends; **the use-case middle varies a lot — that's
intentional, don't templatize it.** A deck runs ~8–14 slides, one idea each, generous whitespace.

1. **Cover** (`.slide.dark.cover`) — title, one-line pitch, partner/org name.
2. **Earth hero** (`.slide.dark.earth`) — *the* Bayes vision slide (§5). "We believe in a world
   where __" over the living planet. This is our signature; keep it second.
3. **Who we are** — the mission line + the credibility (10+ yrs, 3 continents, 10M+) + funder logos.
4. **Arguments & use cases** — *the bespoke middle.* As many slides as the story needs: the problem,
   the vision (3 pillars in `.cards.c3`), one slide per sector/use case, the trust/sovereignty story.
   **Shape this freely to the brief** — a hospital deck looks nothing like a ministry deck here.
5. **Interactive demos** — the proof. At least one of the two engines (§6), often both: the
   conversational service (chat) and the back-office copilot. **Demo-forward: this is what sells.**
6. **Team / sponsors / how we work** — the partnership (open-source, skills transfer, advisory).
7. **Thank-you** (`.slide.dark.cover`) — a clean visual close + the tagline.

The `_template/index.html` is exactly this skeleton, filled with a generic Bayes Platform pitch and
both demos wired up. Start there.

---

## 6 · The earth hero (our signature — match the website)

The vision slide mirrors the bayesimpact.org homepage: a **living Earth in dark space** with a
**starfield** and a faint **orbiting dot-cloud**, beside the headline **"We believe in a world
where …"** whose tail **fade-cycles** through statements.

In the deck file it's just:
```html
<section class="slide dark earth" id="earth" data-dark>
  <div class="brand-corner">…</div>
  <div class="slide-inner"><div class="hero believe-box" id="believeBox">
    <div class="hero-txt">
      <h1 class="believe"><span data-lang="fr">Nous croyons en un monde où</span><span data-lang="en">We believe in a world where</span><span class="believe-cycle" id="believeCycle"></span></h1>
      <p class="lead">…the mission line…</p>
    </div>
    <div class="hero-planet"><div class="planet-wrap"><img src="../../assets/planet.webp" alt="Earth"/><div class="planet-orbit" id="planetOrbit"></div></div></div>
  </div></div>
  <script type="application/json" class="believe-data">
  {"fr":["…","…"],"en":["…","…"]}
  </script>
</section>
```
`bayes.js` builds the stars, the orbit, and runs the fade-cycle from `.believe-data`. **Rewrite the
phrases to the audience** (e.g. for health: "chaque patient est compris", "les soignants gardent du
temps pour soigner"). Keep `id`s and class names exactly.

---

## 7 · The demos (the part that makes it real)

Each demo lives on its own slide, marked `data-demo="chat"` or `data-demo="copilot"`, and is driven
by an **inline JSON script** inside that slide: `<script type="application/json"
class="demo-data">…</script>`. `bayes.js` auto-plays it when the slide scrolls into view, and renders
its **finished state** for the PDF. **You adapt the demo by editing the JSON — not the engine.**

### Chat (`data-demo="chat"`) — any conversational service
A WhatsApp-style thread: a citizen requesting a document, a patient's family asking pre-op questions,
a donor onboarding, a beneficiary getting support. The JSON:
```json
{ "pay": {"provider":"Mobile Money","host":"pay.gov/"},
  "fr": [ {steps…} ], "en": [ {steps…} ] }
```
Each step is one of:
- `{"type":"in","text":"…","bp":1}` — assistant message (`bp:0–N` lights the left journey strip)
- `{"type":"out","text":"…","digits":true}` — user message (`digits` = monospace for IDs/codes)
- `{"type":"tool","name":"…","arg":"k: \"v\"","result":"…"}` — a tool/API call card
- `{"type":"fill","src":"…","rows":[["Label","Value"],…]}` — auto-filled form from a record
- `{"type":"voice","dur":"0:05","transcript":"…"}` — a voice note + its transcription
- `{"type":"dossier","num":"…","rows":[…]}` — a compiled request/case
- `{"type":"paylink","amount":"…","ref":"…","code":"…"}` — a payment link (flips to ✓ Paid)
- `{"type":"notif","tag":"N04","text":"…"}` — an external callback / status notification

The left panel (the service card + BPMN journey strip with `.bpmn-node`s) and the header service
name are plain HTML in the slide — relabel them for the use case. The **voice note + local-language**
angle is a strong inclusion point; keep it where it fits.

### Copilot (`data-demo="copilot"`) — any NL query over a corpus/DB
A back-office agent answering in natural language with cited sources, over a scan→agent→DB pipeline:
case-law for a magistrate, clinical/wearable analytics for a clinician, an internal knowledge base.
```json
{ "meta": {"who":{"fr":"Agent","en":"Officer"},"search":{"fr":"Recherche","en":"Search"},"name":{"fr":"Copilote","en":"Copilot"}},
  "fr": [ {"q":"…question…","arg":"…query…","res":"3 résultats","a":"…streamed answer…","s":["source 1","source 2"]} ],
  "en": [ … ] }
```
Relabel the pipeline stages (Documents → Bayes agent → Structured DB) in the slide HTML to the domain
(e.g. *wearable data → agent → time-series query*).

**Both demos must have FR and EN arrays with matching steps.** Demo data is illustrative — say so.

---

## 8 · Bilingual (inline FR/EN) — non-negotiable

Every deck ships **FR + EN** from the start. The approach is **inline `data-lang` spans** — no central
dictionary. For any piece of text, write both:
```html
<span data-lang="fr">Texte français</span><span data-lang="en">English text</span>
```
`bayes.js` detects which languages are present, shows the **FR/EN toggle** automatically, and hides
the inactive language with CSS. The demo JSON carries `fr` and `en` arrays; the earth carries
`fr`/`en` phrase lists. **Rule: if you write a French string, write its English twin in the same
place, and vice-versa.** No orphans.

---

## 9 · Hard requirements (every deck, every time)

- **Mobile-readable.** The layout stacks and scrolls naturally on phones (≤700px). Walk every slide
  at **375×812** — nothing clipped, demos still animate, taps work. Desktop is the **first-class**
  surface for *presenting* the demos, but mobile must always be browsable.
- **PDF-exportable, as a rule.** The **PDF button** (and Cmd/Ctrl-P) must produce a clean export with
  the **desktop layout** and **every demo in its finished state** (full chat thread, copilot answer
  shown). This is wired in `bayes.js` (`beforeprint`) + the `@media print` block — keep your custom
  slides inside `.slide > .slide-inner` so they inherit it. Verify it before shipping.
- **Dependency-free, zero-build.** Plain HTML/CSS/JS. Must work opened as a file and on GitHub Pages.
  Relative asset paths (`../../assets/…`, `../../lib/…`).
- **Console clean.** No errors on load or while the demos run.

---

## 10 · Wording library (reuse — keep the voice consistent)

Adapt, don't translate. Pull from these so every deck sounds like one Bayes.

| Use | FR | EN |
|---|---|---|
| Mission | L'IA pour aider celles et ceux qui en ont besoin et celles et ceux qui les accompagnent. | AI to empower people in need and those who serve them. |
| Vision (earth) | Nous croyons en un monde où chacun reçoit l'aide dont il a besoin. | We believe in a world where everyone receives the help they need. |
| Sovereignty | Open-source, souveraine — vos données restent chez vous. | Open-source, sovereign — your data stays in-house. |
| Trust | Fiabilisé par vos documents (RAG) : zéro hallucination, sources citées. | Grounded in your documents (RAG): zero hallucination, sources cited. |
| No-code | Vos équipes créent et déploient des agents, sans coder. | Your teams build and deploy agents, no code. |
| Partnership | Un partenariat, pas un fournisseur : Bayes accompagne, ne verrouille pas. | A partnership, not a vendor: Bayes supports, doesn't lock you in. |
| Gov positioning | La Bayes Platform, DPI du gouvernement agentique. | The Bayes Platform, the DPI of the agentic government. |
| Maturity caveat | À titre illustratif — à confirmer avant diffusion. | Illustrative — to be confirmed before any real audience. |

---

## 11 · Publish

The repo auto-deploys to GitHub Pages. Commit the new `demos/<slug>/` folder and push; the demo is
live at:
```
https://bayesimpact.github.io/bayes-demos/demos/<slug>/
```
Give the teammate that URL **and** the splash access code (the slug) — the splash at the repo root
(`/`) is a soft gate: a visitor types the code and is sent to the demo. The repo is public, so this
is security-by-obscurity only; mark genuinely confidential pitches as such and don't rely on the gate.

---

### TL;DR
Copy `demos/_template/`, rewrite **one HTML file** to the brief (slides + the two demo JSON blocks),
keep every string **FR+EN**, keep the earth hero + the design tokens, verify **desktop + mobile +
PDF**, push, share the URL. Sound like Bayes. Be honest about what's a demo.
