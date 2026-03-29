# ZORA Landing Site — Copy Refresh Design

**Goal:** Update landing page copy to accurately reflect the app's capabilities, address visitor confusion, and add a personal origin story to the Why section.

**Architecture:** Pure copy changes to `index.html`. No structural HTML or CSS changes. No new sections.

**Scope:** `index.html` only. `privacy.html`, `terms.html`, `styles.css` untouched.

---

## 1. Hero Section

**File:** `index.html`

**Current lead (line 36):**
> ZORA helps you understand your medication routine so you can feel your best — and actually communicate what's working to the people helping you.

**New lead:**
> ZORA is a daily log for your medications and how they make you feel — so you can finally know if they're working, and communicate the full picture to the people helping you.

**Rationale:** The old copy implied ZORA helps you "understand your routine" — vague and slightly off-mission. The new copy makes clear it's a daily log, frames the core value as knowing whether meds are working, and preserves the "communicate" angle the user wanted to keep.

No changes to the headline (`Track your meds. Find what works.`) or buttons.

---

## 2. How It Works — Cards

**File:** `index.html`

Three cards. Title and description changes only — icons and structure unchanged.

| Card | Current title | New title | Current desc | New desc |
|---|---|---|---|---|
| 1 | Log your meds | Log your meds | "Add your medications and dosages in seconds." | "Add your medications, dosages, and when you took them." |
| 2 | Track patterns | Log how you feel | "See how you feel over days, weeks, and months." | "Each day, record your mood, energy, sleep, and other symptoms that matter to you." |
| 3 | Share with your doctor | Share with your doctor | "Walk into every appointment with the full picture." | "Walk into every appointment with weeks of real data instead of trying to remember." |

**Rationale:**
- Card 2 rename from "Track patterns" to "Log how you feel" directly answers the visitor question "do I have to tag things?" — yes, it's manual daily logging, and here's what you log.
- Card 1 adds "when you took them" to clarify this is a time-stamped daily log, not a one-time medication list.
- Card 3 replaces the vague "full picture" with "weeks of real data" — concrete and emotionally resonant.

---

## 3. Why We Built ZORA

**File:** `index.html`

**Current copy (lines 206–207):**
> Built to help you discover medications that actually help. Even on the worst days.
>
> Finding the right treatment can take years of trial, adjustment, and appointments where you struggle to explain what you've been feeling. ZORA gives you a simple way to track what you're taking, how you feel, and what changes — so when it matters most, you have the full picture.

**New copy (two paragraphs, replace both existing `<p class="body-text">` elements):**

> Someone we love spent years cycling through medications, talking to psychiatrists, trying to understand whether each new prescription was helping, hurting, or making no difference at all.

> ZORA was born from that experience. We wanted to create a simple way for those struggling with the same thing to stay consistent and to keep an honest record of which days were hard and how the easier days felt. So much of better care comes down to information, and too often that gets lost between visits. ZORA helps keep it in view.

**Rationale:** The previous copy was generic. The new copy grounds ZORA in a real personal experience, names the core problem (years of trial, inability to track what's helping), and ends with a clear value statement. The `h2` ("Finding the right medication shouldn't take years.") stays unchanged — it pairs well with the new body copy.

---

## 4. CTA Section

**File:** `index.html`

**Current headline (line 239):** "Coming soon to the App Store."
**New headline:** "Launching Spring 2026 on the App Store."

**Rationale:** Addresses the top visitor question ("when?") with a concrete timeframe. The app is already in App Store review. The subtext ("Be the first to know when ZORA launches.") and form are unchanged.

---

## 5. Out of Scope

- No structural HTML changes
- No CSS changes
- No new sections
- No changes to nav, footer, phone mockup, or legal pages
- No changes to hero headline or buttons
