# ZORA Landing Site — Visual Polish Design

**Goal:** Upgrade the landing page hero and icon system to feel bold and premium while keeping the existing blue/gold color scheme and page structure.

**Architecture:** Pure static HTML/CSS changes to `index.html` and `styles.css`. No new sections, no new pages, no build step. Tabler Icons loaded via CDN.

**Scope:** `index.html`, `styles.css` only. `privacy.html` and `terms.html` are untouched.

---

## 1. Hero Section Redesign

**Current state:** Full-width gradient section with `<div class="section-inner">` centered content — badge, h1, lead, two buttons. No visual of the app.

**New layout:** The `<section>` keeps its `style="background: var(--hero-gradient);"` inline style. Inside, replace the single `section-inner` div with a `hero-inner` div that uses flexbox to split into two columns.

**HTML skeleton** (replaces the existing hero section interior):

```html
<section style="background: var(--hero-gradient);">
  <div class="hero-inner">

    <!-- Left: copy -->
    <div class="hero-copy">
      <div class="hero-badge">
        <i class="ti ti-device-mobile"></i> Coming to App Store
      </div>
      <h1>Track your meds.<br/><span style="color: #fff3cc;">Find what works.</span></h1>
      <p class="lead">ZORA helps you understand your medication routine so you can feel your best — and actually communicate what's working to the people helping you.</p>
      <div class="hero-actions">
        <a href="#notify"><button class="btn-primary">Notify Me at Launch</button></a>
        <a href="#how-it-works"><button class="btn-ghost">Learn More</button></a>
      </div>
    </div>

    <!-- Right: phone mockup -->
    <div class="hero-phone">
      <!-- phone mockup HTML here — see Section 1b -->
    </div>

  </div>
</section>
```

The existing anonymous `<div style="display: flex; gap: 12px; justify-content: center; flex-wrap: wrap;">` wrapping the buttons is replaced by `<div class="hero-actions">` — remove the inline style div entirely.

**CSS for hero layout** (add to `styles.css`):

```css
.hero-inner {
  max-width: 900px;
  margin: 0 auto;
  padding: 56px 24px;
  display: flex;
  gap: 48px;
  align-items: center;
}
.hero-copy {
  flex: 1;
  text-align: left; /* intentional — hero copy is left-aligned in the two-column layout, unlike the centered single-column sections elsewhere on the page */
}
.hero-actions {
  display: flex;
  gap: 12px;
  flex-wrap: wrap;
}
.hero-phone {
  flex-shrink: 0;
}
```

**Typography changes** (update in `styles.css`):
- `h1`: font-size `52px` (up from `44px`), add `letter-spacing: -2px`

**Responsive** (in the existing `@media (max-width: 640px)` block in `styles.css`):
- Add `.hero-inner { flex-direction: column; }` and `.hero-phone { display: none; }`
- The existing `h1 { font-size: 32px; }` rule is already there — update it in-place to add `letter-spacing: -0.5px;`, do not add a duplicate rule.

---

## 1b. Phone Mockup

Built entirely in HTML/CSS inside `.hero-phone` — no images. All CSS for the phone mockup is written as **inline styles** directly on the elements (not in `styles.css`), since this is a self-contained decorative component. Font sizes are intentionally small (7–11px). Slight clipping at the bottom of the sheet is acceptable and expected.

**Outer shell:** `width: 200px; height: 410px; overflow: hidden;` (overflow hidden produces the natural bottom-sheet clipping), `border-radius: 36px`, white background (`#ffffff`), `border: 5px solid rgba(255,255,255,0.4)`, large drop shadow. All set as inline styles on the outer div. The `.hero-phone` CSS class only needs `flex-shrink: 0` — the phone dimensions are self-contained via inline styles.

**Layers top to bottom:**

1. **Status bar** — `9:41` left, battery/signal right. Dark text on white.
2. **Nav bar** — `ZORA` in `#5DABFE` bold, gear icon right: `<i class="ti ti-settings" style="color:#8e8e93;font-size:14px;"></i>`
3. **Month nav** — `<i class="ti ti-chevron-left"></i> March 2026 <i class="ti ti-chevron-right"></i>` (icons in `#8e8e93`).
4. **Weekday bar** — S M T W T F S in `#8e8e93`, 7-column grid.
5. **Thin separator** — `0.5px`, `#e5e5ea`.
6. **Calendar grid** — 7-column CSS grid, March 2026 (starts Sunday, 5 rows):
   - **Logged day (has check-in):** `20px` circle, background color from `overallColor @ 18% opacity`. Use: green `rgba(52,199,89,0.18)`, yellow `rgba(255,204,0,0.22)`, red `rgba(255,59,48,0.15)`. Semibold number.
   - **Selected day (28 — today):** solid `#5DABFE` circle, white bold number.
   - **Unlogged day:** plain number, no circle.
   - Specific day coloring (implementer must use exactly these): green on 8,9,12,15,16,18,20,21,23,24,26,27 — yellow on 11,19,25 — red on 14,22 — unlogged on 1–7,10,13,17. Days 29–31 are future/unlogged.
7. **Bottom sheet** — `border-radius: 18px 18px 0 0`, `background: #fefcfe`, drag handle bar at top.
   - Date label: "Today, March 28" + "Edit" in `#5DABFE`
   - Overall score: `4.2` in `#34c759` (large bold) + `/ 5` in `#c7c7cc`
   - Thin separator
   - Two medication rows: Tabler pill icon in `#5DABFE` + "Sertraline • 50mg • Morning" and "Wellbutrin • 150mg • Morning"
   - Thin separator
   - Three metric bars (Mood 5, Energy 4, Sleep 3): label + score + `red→yellow→green` gradient bar + white thumb dot

---

## 2. Icon System — Tabler Icons

**CDN link** — add to `<head>` of `index.html`, pinned to major version 3 (resolves to latest 3.x at fetch time — acceptable for a pre-launch static site):
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@3/dist/tabler-icons.min.css" />
```

**Replacements in `index.html`:**

| Location | Current HTML | New HTML |
|---|---|---|
| Hero badge | `📱 Coming to App Store` | `<i class="ti ti-device-mobile"></i> Coming to App Store` |
| How it Works — Log meds | `💊` | `<i class="ti ti-pill"></i>` |
| How it Works — Track patterns | `📈` | `<i class="ti ti-activity"></i>` |
| How it Works — Share with doctor | `🗣️` | `<i class="ti ti-clipboard-heart"></i>` |

Update the existing `.hero-badge` rule in-place — replace `display: inline-block` with `display: inline-flex` and add `align-items: center; gap: 6px;`. All other properties (padding, border-radius, color) stay as-is.

**Icon sizing** inside `.how-icon` gradient containers (add to `styles.css`):
```css
.how-icon i {
  font-size: 22px;
  color: white;
}
```

---

## 3. Files Changed

| File | What changes |
|---|---|
| `index.html` | Hero interior replaced with `.hero-inner` two-column layout + phone mockup; Tabler CDN `<link>` in `<head>`; 4 emoji replacements |
| `styles.css` | Add `.hero-inner`, `.hero-copy`, `.hero-actions`, `.hero-phone`; update `h1` size + letter-spacing; add `.how-icon i` rule; update mobile breakpoint |

**Unchanged:** `privacy.html`, `terms.html`, `assets/`, `vercel.json`

---

## 4. Out of Scope

- No new sections (social proof, waitlist counter, FAQ)
- No dark mode
- No animations or scroll effects
- No changes to copy
- No changes to the email capture form behavior
- No changes to the "Why We Built ZORA" or CTA sections
