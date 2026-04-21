# Hawkeye Website Test Cases (Current Scope)

Use this sheet to validate what is already implemented in:

- `/`
- `/about/`
- `/faq/`

Status values:

- `Pass`
- `Fail`
- `Blocked`

---

## 1) Global Smoke Checks

### TC-G01: Pages load successfully

- **Precondition:** Local server is running.
- **Steps:**
  1. Open `/`
  2. Open `/about/`
  3. Open `/faq/`
- **Expected:** All pages render without blank screen or browser error.

### TC-G02: Shared stylesheet loads

- **Steps:**
  1. Open each route (`/`, `/about/`, `/faq/`)
  2. Visually verify brand colors, typography, spacing are styled (not plain HTML)
- **Expected:** `styles.css` is applied on all pages.

### TC-G03: Skip link works on keyboard

- **Steps:**
  1. Open each page
  2. Press `Tab` once
  3. Activate "Skip to content"
- **Expected:** Focus jumps to the main content region (`#main`).

### TC-G04: Brand link returns to home

- **Steps:**
  1. From `/about/`, click brand in nav
  2. From `/faq/`, click brand in nav
- **Expected:** Navigates to `/`.

### TC-G05: WhatsApp CTA URL consistency

- **Steps:**
  1. Check "Get started" and/or "Start a conversation" links on all pages
- **Expected:** Every WhatsApp CTA points to `https://wa.me/919540134700`.

---

## 2) Home Page (`/`) Test Cases

### TC-H01: Hero renders key trust copy

- **Steps:**
  1. Open `/`
  2. Locate hero heading and subcopy
- **Expected:** Hero includes mutual fund positioning and primary headline ("Financial freedom, personally delivered.").

### TC-H02: Hero CTA and secondary anchor behavior

- **Steps:**
  1. Click "Start a conversation"
  2. Return to `/`
  3. Click "See how it works"
- **Expected:** Primary CTA opens WhatsApp link; secondary CTA scrolls to `#how-it-works`.

### TC-H03: Desktop nav links

- **Precondition:** Viewport width >= 1100px.
- **Steps:**
  1. Click "How it works"
  2. Click "FAQ"
  3. Click "About"
- **Expected:** Links resolve to `/#how-it-works`, `/faq/`, `/about/` respectively.

### TC-H04: Mobile nav drawer links

- **Precondition:** Viewport width < 1100px.
- **Steps:**
  1. Open burger menu
  2. Click each drawer link
- **Expected:** Drawer links navigate correctly (same destinations as desktop nav).

### TC-H05: Landing sections render in expected order

- **Steps:**
  1. Scroll top to bottom on `/`
- **Expected:** Sections appear in this sequence:
  1. Hero
  2. Credentials
  3. Who we work with
  4. Philosophy + How it works
  5. Testimonial
  6. Final CTA

### TC-H06: Footer disclaimer visible

- **Steps:**
  1. Scroll to final CTA block
- **Expected:** Regulatory/disclaimer copy is present and readable.

---

## 3) About Page (`/about/`) Test Cases

### TC-A01: About hero identity block

- **Steps:**
  1. Open `/about/`
  2. Verify name, role subtitle, and portrait block
- **Expected:** "Rajesh Sahu" and Founder/CIO context is visible.

### TC-A02: At-a-glance credentials section

- **Steps:**
  1. Find "At a glance" section
- **Expected:** Credentials text includes CFP, market experience, ARN, and AMFI references.

### TC-A03: About narrative sections

- **Steps:**
  1. Verify "Experience"
  2. Verify "How Hawkeye works with you"
  3. Verify quote block
- **Expected:** All sections render with body text intact and readable.

### TC-A04: About CTA and disclaimer

- **Steps:**
  1. Click "Start a conversation"
  2. Inspect disclaimer text below CTA
- **Expected:** CTA opens WhatsApp; disclaimer copy is shown.

### TC-A05: About mobile content variant

- **Precondition:** Viewport width < 1100px.
- **Steps:**
  1. Open `/about/`
  2. Check mobile intro, compressed credentials line, mobile quote
- **Expected:** Mobile-specific copy/layout appears (not desktop block).

---

## 4) FAQ Page (`/faq/`) Test Cases

### TC-F01: FAQ hero renders

- **Steps:**
  1. Open `/faq/`
  2. Verify eyebrow + H1 title
- **Expected:** Intro header appears with "Common questions" and the FAQ headline.

### TC-F02: FAQ accordion interaction

- **Steps:**
  1. Expand a closed question
  2. Collapse the same question
- **Expected:** `<details>` toggles content correctly without layout breaking.

### TC-F03: Default expanded FAQ items

- **Steps:**
  1. Open `/faq/`
  2. Identify items expanded on initial load
- **Expected:** Exactly these are open by default:
  - "How is Hawkeye Capital different from Groww or Zerodha?"
  - "How do I start investing in mutual funds in India?"
  - "Is my money safe with a mutual fund distributor?"

### TC-F04: All FAQ items contain answer body

- **Steps:**
  1. Expand each FAQ one by one
- **Expected:** Each question has non-empty answer text and no truncation/cutoff.

### TC-F05: Keyboard accessibility on FAQ summary

- **Steps:**
  1. Tab to a FAQ question summary
  2. Press `Enter` (or `Space`) to toggle
- **Expected:** Question toggles and focus remains visible (focus ring present).

### TC-F06: FAQ mobile wording variant

- **Precondition:** Viewport width < 1100px.
- **Steps:**
  1. Find robo-advisor question
- **Expected:** Mobile-specific shorter question variant is shown.

---

## 5) Responsive and Visual Regression Checks

Run the following at minimum viewports:

- Mobile: `390 x 844`
- Tablet: `768 x 1024`
- Desktop: `1440 x 900`

### TC-R01: No horizontal overflow

- **Steps:**
  1. Check each page at all viewports
  2. Scroll horizontally
- **Expected:** No unintended horizontal scrolling.

### TC-R02: Navigation mode switch

- **Steps:**
  1. Test around `1099px` and `1100px`
- **Expected:** Mobile nav is visible below breakpoint; desktop nav above breakpoint.

### TC-R03: Desktop-only/mobile-only content behavior

- **Steps:**
  1. Compare home hero text variants and quote marks
  2. Compare About content blocks
  3. Compare FAQ mobile-specific question label
- **Expected:** Correct variant appears per breakpoint; hidden variant does not overlap.

### TC-R04: Image assets load

- **Steps:**
  1. Validate hero background
  2. Validate hawk graphic (desktop only on home)
  3. Validate about portrait background
- **Expected:** No broken image placeholders.

---

## 6) Suggested Bug Report Template

When a case fails, log:

- **Test case ID:** (e.g., `TC-F03`)
- **Environment:** Browser + viewport + local/prod URL
- **Actual result:** What happened
- **Expected result:** What should have happened
- **Screenshot:** Attach visual proof
- **Severity:** Critical / High / Medium / Low