# Hawkeye Capital — Agent Instructions

This document is the **source of truth for AI and human agents** working on the Hawkeye Capital website and related deliverables. Read it before making architectural, copy, or compliance decisions. Prefer **simple, shippable** choices over framework churn unless the user explicitly expands scope.

---

## Recommendations vs implementation (do not skip)

The user often asks for **thinking**, not **shipping**. Treat these differently:


| User intent                   | Examples of phrasing                                                                                                                                                               | What you do                                                                                                                                                                                         |
| ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Recommendation / critique** | “What do you think?”, “Recommendation?”, “Suggestion”, “Should we…?”, “What can we do about…?”, “Options”, “Feedback”, “I don’t like how X looks” (without “fix it” / “change it”) | **Answer only:** trade-offs, 2–3 concrete options, risks, and what you’d pick and why. **No edits** to this repo, **no Paper MCP mutations**, no drive-by file changes. They may still be deciding. |
| **Build / apply**             | “Implement”, “Apply that”, “Change Paper”, “Update the file”, “Do it now”, “Ship”, “Go ahead”, “Make it so”, “Patch”, explicit task to alter assets or code                        | **Execute:** code changes, Paper `update_styles` / `write_html`, etc., as appropriate.                                                                                                              |


**If a message is ambiguous** (sounds like a question but could imply work), default to **recommendation-only** and offer a one-line ask: *Want me to apply this in Paper / the repo?*

This applies especially to **Paper** (`hawkeyecapital.in`): design critique ≠ permission to restyle the canvas.

---

## Project snapshot

- **Client:** Hawkeye Capital — SEBI-registered **mutual fund distributor** (India), human-led advice.
- **Live domain:** [https://hawkeyecapital.in](https://hawkeyecapital.in) (revamp in progress).
- **Operator:** Rajesh Sahu (Founder & CIO) — credentials and story live in copy briefs, not as a “celebrity hero” treatment on v1.
- **Studio:** Masala Dew (project owner: see Linear **Hawkeye Capital**).

---

## Non-negotiables

1. **Numbers policy (DEW-58):** Do **not** publish **AUM** or **client count** on the public site. Credibility = tenure, certifications, process, testimonials — not disclosed financials.
2. **Scope of business:** Hawkeye is **mutual fund distribution** only for this site. Do not imply stock-picking RIA breadth unless copy is legally accurate.
3. **Primary CTA:** WhatsApp **+91 9540134700** — prefer `wa.me` links; no mandatory web forms on v1 unless the user adds them.
4. **Regulatory accuracy:** Distributor **ARN-156467** is confirmed from Rajesh. SEBI / AMFI claims on the site must match **approved legal copy** — never invent numbers or registration text beyond what is confirmed.

---

## Engineering principles

- **Minimize JavaScript.** Marketing site first: **HTML + CSS**; static or SSG output is ideal.
- **Prefer platform primitives:** `<details>` / `<summary>` for FAQ if behavior matches UX; native links for navigation.
- **No SPA requirement** — no client-side router for v1.
- **Performance:** subset fonts, lazy non-critical images, avoid heavy carousels; respect `prefers-reduced-motion`.
- **Conflict check:** If a Linear issue or old doc suggests putting AUM/client counts in HTML for “GEO,” **override with the numbers policy** above unless the user explicitly changes policy.

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

- **North-star aesthetic:** **[Sapient Wealth](https://sapientwealth.in)** — structured trust, multi-segment clarity, polished “wealth firm” feel. **Do not** copy their full service breadth, public AUM style, or page count; steal **layout discipline, trust framing, and footer/legal patterns**.
- **Hawkeye differentiation:** Old-book / editorial warmth (forest, bark, parchment — see design brief), **human** over “platform,” **MF distribution** clarity.
- **Design source of truth:** Paper file `**hawkeyecapital.in`** — artboards for landing (desktop/mobile) and FAQ (desktop/mobile). Prefer **get_jsx / get_computed_styles** when translating to code, not screenshots alone.
- **Nav masthead:** Paper reserves a **square logo slot** (layer `**Logo placeholder — asset TBD`**, dashed gold outline) **before** the wordmark; **no SEBI/ARN line** in the top bar — use credentials, CTA footer, and legal pages for registration text. Replace the placeholder with the final client logo asset in build (see `references/hawkeye-design.md` → Global navigation).
- **References folder:** `references/` — `hawkeye-capital-master.md`, `hawkeye-design.md`, `hawkeye-dew58-working-notes.md` — **copy and locked decisions** live here; reconcile with Linear if anything conflicts.

---

## GEO, search, and agent readability

- **Real content in HTML** — no critical copy injected only by JS.
- **One clear `<h1>`** per page; logical heading order for sections and FAQ.
- **FAQ answers** should work as **standalone paragraphs** (already drafted in DEW-58 notes) so LLMs can quote them cleanly.
- **FAQPage JSON-LD** is optional until the domain is live and indexed — can be v1.1; do not block launch on schema alone.

---

## Compliance & “paperwork” checklist

Minimum credible cluster for a regulated Indian site (iterate with legal/compliance as needed):

- Correct **distributor registration / ARN** display where applicable
- **Disclaimer** (scope: MF distribution; not personalised advice unless true; standard MF risk language)
- **Privacy policy** and **terms** when you collect data or run analytics
- Optional: **disclosure** page or link to **SEBI** mutual fund resources (peers often link SID/SAI/KAM hubs — only if maintained)

Never invent SEBI numbers or registration text.

---

## Competitor reviews (ongoing)

Use the **panel** in `references/hawkeye-design.md` (Dezerv, Stash Wealth, Artemis, Falcon, Sapient) plus optional **small Indian peers** if needed.

When proposing a change, tag:

- **Benchmark:** which site inspired it  
- **Hawkeye constraint:** numbers policy, MF-only, WhatsApp-first  
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
5. **Paper:** confirm against latest artboards before pixel-perfect implementation.

If instructions in chat **conflict** with this file, **ask the user** unless the conflict is an obvious error (e.g. outdated placeholder ARN).

---

*Last updated: 2026-04-20 — added “Recommendations vs implementation” for agents (Paper + repo).*