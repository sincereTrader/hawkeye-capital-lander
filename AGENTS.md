# Hawkeye Capital — Agent Instructions

This document is the **source of truth for AI and human agents** working on the Hawkeye Capital website and related deliverables. Read it before making architectural, copy, or compliance decisions. Prefer **simple, shippable** choices over framework churn unless the user explicitly expands scope.

---

## Paper overrides everything (read first)

The **Paper design system** at [app.paper.design/file/01KPJN44ARS3W2E809KQFHAWE3/2-0/185-0](https://app.paper.design/file/01KPJN44ARS3W2E809KQFHAWE3/2-0/185-0) (including linked artboards and exploration frames) is the **highest-priority** instruction set for this project.

**If anything conflicts with Paper — including sections below, Linear issues, `references/` notes, DEW-58 copy policy, GEO or marketing heuristics, or prior agent assumptions — follow Paper.** Implement layouts, typography, colours, spacing, **and on-canvas copy** (headlines, body, metrics, credentials, CTAs) exactly as specified in Paper. Use `**get_jsx` / `get_computed_styles`** (and related Paper MCP tools) to translate to code; do not “fix” or replace Paper content to satisfy another rule.

This override applies to **all designed screens**. For routes or components **not yet represented in Paper**, use the rest of this document and references until designs exist.

While doing any tool calls, ensure that there is exact alignment with the brand tokens. If they are not given, ensure that the user puts the brand tokens on the same Paper page so that you can read from it.

---

## Recommendations vs implementation (do not skip)

The user often asks for **thinking**, not **shipping**. Treat these differently:


| User intent                   | Examples of phrasing                                                                                                                                                               | What you do                                                                                                                                                                                         |
| ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Recommendation / critique** | “What do you think?”, “Recommendation?”, “Suggestion”, “Should we…?”, “What can we do about…?”, “Options”, “Feedback”, “I don’t like how X looks” (without “fix it” / “change it”) | **Answer only:** trade-offs, 2–3 concrete options, risks, and what you’d pick and why. **No edits** to this repo, **no Paper MCP mutations**, no drive-by file changes. They may still be deciding. |
| **Build / apply**             | “Implement”, “Apply that”, “Change Paper”, “Update the file”, “Do it now”, “Ship”, “Go ahead”, “Make it so”, “Patch”, explicit task to alter assets or code                        | **Execute:** code changes, Paper `update_styles` / `write_html`, etc., as appropriate.                                                                                                              |


**If a message is ambiguous** (sounds like a question but could imply work), default to **recommendation-only** and offer a one-line ask: *Want me to apply this in Paper / the repo?*

This applies especially to **Paper** ([design system link](https://app.paper.design/file/01KPJN44ARS3W2E809KQFHAWE3/2-0/185-0)): design critique ≠ permission to restyle the canvas.

---

## Project snapshot

- **Client:** Hawkeye Capital — SEBI-registered **mutual fund distributor** (India), human-led advice.
- **Live domain:** [https://hawkeyecapital.in](https://hawkeyecapital.in) (revamp in progress).
- **Operator:** Rajesh Sahu (Founder & CIO) — credentials and story live in copy briefs, not as a “celebrity hero” treatment on v1.
- **Studio:** Masala Dew (project owner: see Linear **Hawkeye Capital**).

---

## Non-negotiables

These apply **except where Paper specifies otherwise** (see [Paper overrides everything](#paper-overrides-everything-read-first)). On designed pages, **Paper is the approval** for visible copy and numbers.

1. **Published numbers and claims:** Whatever **Paper** shows on a shipped artboard (including **AUM**, **client counts**, tenure lines, or other metrics) **must be implemented as designed.** Do not strip or substitute metrics to match older written policies.
2. **Scope of business:** Default: Hawkeye is **mutual fund distribution** for this site. If Paper copy implies a broader or narrower scope, **match Paper** and flag a product/legal review separately — do not unilaterally rewrite the canvas.
3. **Primary CTA:** WhatsApp **+91 9540134700** — prefer `wa.me` links; no mandatory web forms on v1 unless Paper or the user adds them.
4. **Regulatory strings:** Use the **exact registration / disclaimer / footer text from Paper** where it appears. Do not invent SEBI or AMFI numbers; if Paper and an old brief disagree, **Paper wins** for the build.

---

## Engineering principles

- **Minimize JavaScript.** Marketing site first: **HTML + CSS**; static or SSG output is ideal.
- **Prefer platform primitives:** `<details>` / `<summary>` for FAQ if behavior matches UX; native links for navigation.
- **No SPA requirement** — no client-side router for v1.
- **Performance:** subset fonts, lazy non-critical images, avoid heavy carousels; respect `prefers-reduced-motion`.
- **Conflict check:** If a Linear issue or old doc conflicts with **Paper** on copy or metrics, **follow Paper** (see [Paper overrides everything](#paper-overrides-everything-read-first)).

---

## Information architecture

### Launch routes (target)


| Route    | Purpose                                                                                               |
| -------- | ----------------------------------------------------------------------------------------------------- |
| `/`      | Landing: hero → credentials → who we work with → philosophy + how it works → testimonial → CTA        |
| `/faq`   | Full FAQ (long-form, quotable answers)                                                                |
| `/about` | Founder / CIO profile (trust layer; copy in Paper artboards **About — Desktop** / **About — Mobile**) |


Use **stable section IDs** on `/` for anchors (e.g. `#credentials`, `#who-we-work-with`, `#how-it-works`, `#testimonials`, `#cta`) — align with nav and Paper.

### Recommended alongside launch (trust / compliance)


| Route                           | Purpose                                                                   |
| ------------------------------- | ------------------------------------------------------------------------- |
| `/privacy-policy`               | Data, cookies, contact — especially if analytics or forms are added later |
| `/terms` or `/terms-conditions` | Site terms                                                                |
| `/disclaimer`                   | Investment / MF / non-advice disclaimers                                  |


Thin static pages are fine; legal review can follow.

### Deferred (explicitly out of v1 unless user reopens)

- Social media links in header/footer; social “header” assets (OG/Twitter) — can track as **post–design system** polish.
- Smallcase or other products until live and approved.
- Blog / resources until there is a real publishing cadence.

---

## Design direction

- **North-star aesthetic:** **[Sapient Wealth](https://sapientwealth.in)** — structured trust, multi-segment clarity, polished “wealth firm” feel. **Do not** copy their full service breadth, public AUM style, or page count; steal **layout discipline, trust framing, and footer/legal patterns** (benchmark only — **Paper** defines what ships).
- **Hawkeye differentiation:** As expressed in **Paper** and the brief: old-book / editorial warmth (forest, bark, parchment), **human** over “platform,” **MF distribution** clarity.
- **Design source of truth:** Paper design system at [app.paper.design/file/01KPJN44ARS3W2E809KQFHAWE3/2-0/185-0](https://app.paper.design/file/01KPJN44ARS3W2E809KQFHAWE3/2-0/185-0). Prefer **get_jsx / get_computed_styles** when translating to code, not screenshots alone. **Do not deviate** from Paper for pixel implementation or copy.
- **Nav masthead:** As in Paper — **square logo slot** (e.g. layer **Logo placeholder — asset TBD**, dashed gold outline) **before** the wordmark; registration lines live where Paper places them (e.g. credentials block, footer). Replace the placeholder with the final client logo asset in build when provided.
- **References folder:** `references/` — `hawkeye-capital-master.md`, `hawkeye-design.md`, `hawkeye-dew58-working-notes.md` — background context only. **If a reference conflicts with Paper, ignore the reference for implementation.**

---

## GEO, search, and agent readability

- **Real content in HTML** — no critical copy injected only by JS.
- **One clear `<h1>`** per page; logical heading order for sections and FAQ.
- **FAQ answers** should work as **standalone paragraphs** so LLMs can quote them cleanly. **Copy on the FAQ pages must match Paper** (`Hawkeye Capital — Mobile FAQ` / `Desktop FAQ`); DEW-58 notes are fallback only where Paper is silent.
- **FAQPage JSON-LD** is optional until the domain is live and indexed — can be v1.1; do not block launch on schema alone.

---

## Compliance & “paperwork” checklist

Minimum credible cluster for a regulated Indian site (iterate with legal/compliance as needed):

- Correct **distributor registration / ARN** display where applicable
- **Disclaimer** (scope: MF distribution; not personalised advice unless true; standard MF risk language)
- **Privacy policy** and **terms** when you collect data or run analytics
- Optional: **disclosure** page or link to **SEBI** mutual fund resources (peers often link SID/SAI/KAM hubs — only if maintained)

Do not invent SEBI numbers or registration text **except** by transcribing **exactly** what Paper specifies.

---

## Competitor reviews (ongoing)

Use the **panel** in `references/hawkeye-design.md` (Dezerv, Stash Wealth, Artemis, Falcon, Sapient) plus optional **small Indian peers** if needed.

When proposing a change, tag:

- **Benchmark:** which site inspired it  
- **Hawkeye constraint:** match **Paper**; MF distribution positioning unless Paper says otherwise; WhatsApp CTA as in Paper  
- **Verdict:** adopt / adapt / reject

Same rubric for trust, IA, FAQ depth, CTA friction, mobile, performance, footer/legal.

---

## Linear

- **Project:** [Hawkeye Capital](https://linear.app/masala-dew/project/hawkeye-capital-69b828f25a91) (team **DEW**).
- **Done:** DEW-58 — positioning, sitemap, copy brief  
- **Open (high level):** DEW-59 design pass · DEW-60 build · DEW-61 presentation deck

Agents should **align implementation tickets** with this file and **update Linear** when scope shifts (routes, compliance pages, deferred social).

---

## Testimonials & consent

- Only use testimonials **explicitly cleared** in the brief (e.g. Sanjay Sathu confirmed; others pending).
- No fake names; no stock headshots passed off as clients.

---

## How to use this file

1. **Start here** for stack, routes, policy, and design north star.
2. **Deep copy / FAQ:** `references/hawkeye-dew58-working-notes.md`.
3. **Visual system & sections:** `references/hawkeye-design.md`.
4. **Business context:** `references/hawkeye-capital-master.md`.
5. **Paper:** confirm against latest artboards; implementation must **match Paper**, not this file’s older constraints.

If instructions in chat **conflict** with **Paper**, **follow Paper**. If instructions in chat conflict with this file but **not** with Paper, follow this file. If **Paper** appears internally inconsistent, **ask the user** or use the latest edited artboard.

---

*Last updated: 2026-04-21 — Paper is the supreme override; non-negotiables reframed to defer to Paper; credentials copy restored to match designs.*