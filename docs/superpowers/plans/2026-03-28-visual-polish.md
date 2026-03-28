# Visual Polish Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Upgrade the ZORA landing page with a bold two-column hero (including a real app phone mockup) and replace all emojis with Tabler Icons.

**Architecture:** Pure static HTML/CSS edits to two files — `index.html` and `styles.css`. No build step. Tabler Icons loaded via CDN. Phone mockup is self-contained HTML with inline styles inside a `.hero-phone` div.

**Tech Stack:** Plain HTML5, CSS3, Tabler Icons v3 (CDN webfont)

**Spec:** `docs/superpowers/specs/2026-03-28-visual-polish-design.md`

---

## File Map

| File | What changes |
|---|---|
| `index.html` | Add Tabler CDN link in `<head>`; replace 4 emojis; replace hero section interior with two-column layout + phone mockup |
| `styles.css` | Add `.hero-inner / .hero-copy / .hero-actions / .hero-phone`; update `h1` size + letter-spacing; update `.hero-badge` to `inline-flex`; add `.how-icon i`; update mobile breakpoint |

**Unchanged:** `privacy.html`, `terms.html`, `assets/`, `vercel.json`

---

## Task 1: Tabler Icons CDN + emoji replacements + CSS tweaks

**Files:**
- Modify: `index.html` (head + 4 emoji swap locations)
- Modify: `styles.css` (`.hero-badge`, `.how-icon i`)

This task is self-contained and verifiable on its own before touching the hero layout.

- [ ] **Step 1: Add Tabler Icons CDN link to `index.html` `<head>`**

In `index.html`, after the existing `<link rel="stylesheet" href="styles.css" />` line, add:

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@3/dist/tabler-icons.min.css" />
```

- [ ] **Step 2: Replace emoji in hero badge**

Find this in `index.html` (inside the hero section):
```html
<div class="hero-badge">📱 Coming to App Store</div>
```

Replace with:
```html
<div class="hero-badge"><i class="ti ti-device-mobile"></i> Coming to App Store</div>
```

- [ ] **Step 3: Replace emojis in How It Works cards**

Find and replace these three lines in `index.html`:

```html
<div class="how-icon how-icon-blue">💊</div>
```
→
```html
<div class="how-icon how-icon-blue"><i class="ti ti-pill"></i></div>
```

```html
<div class="how-icon how-icon-mid">📈</div>
```
→
```html
<div class="how-icon how-icon-mid"><i class="ti ti-activity"></i></div>
```

```html
<div class="how-icon how-icon-gold">🗣️</div>
```
→
```html
<div class="how-icon how-icon-gold"><i class="ti ti-clipboard-heart"></i></div>
```

- [ ] **Step 4: Update `.hero-badge` in `styles.css`**

Find the existing rule (line 170–180):
```css
.hero-badge {
  display: inline-block;
  background: rgba(255,255,255,0.25);
  border: 1px solid rgba(255,255,255,0.5);
  border-radius: 20px;
  padding: 5px 14px;
  margin-bottom: 20px;
  color: white;
  font-size: 12px;
  font-weight: 600;
}
```

Replace `display: inline-block` with `display: inline-flex` and add `align-items: center; gap: 6px;`:
```css
.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  background: rgba(255,255,255,0.25);
  border: 1px solid rgba(255,255,255,0.5);
  border-radius: 20px;
  padding: 5px 14px;
  margin-bottom: 20px;
  color: white;
  font-size: 12px;
  font-weight: 600;
}
```

- [ ] **Step 5: Add `.how-icon i` rule to `styles.css`**

After the `.how-icon-gold` line (line 207), add:
```css
.how-icon i    { font-size: 22px; color: white; }
```

- [ ] **Step 6: Verify in browser**

Open `index.html` in a browser (or run a local server). Confirm:
- No emojis visible anywhere on the page
- Hero badge shows phone icon + "Coming to App Store" with proper spacing
- How It Works cards show pill, activity, clipboard-heart icons centered in their gradient squares
- Icons are white and correctly sized

- [ ] **Step 7: Commit**

```bash
git add index.html styles.css
git commit -m "feat: replace emojis with Tabler Icons, add CDN"
```

---

## Task 2: Hero layout CSS

**Files:**
- Modify: `styles.css` (new hero classes, h1 update, mobile breakpoint)

- [ ] **Step 1: Update `h1` rule in `styles.css`**

Find line 163:
```css
h1 { font-size: 44px; font-weight: 800; color: white; line-height: 1.15; margin-bottom: 16px; text-shadow: 0 2px 10px rgba(0,0,0,0.1); }
```

Replace with:
```css
h1 { font-size: 52px; font-weight: 800; color: white; line-height: 1.1; letter-spacing: -2px; margin-bottom: 16px; text-shadow: 0 2px 10px rgba(0,0,0,0.1); }
```

- [ ] **Step 2: Add hero layout classes to `styles.css`**

After the `/* ─── Hero badge pill ─── */` block (after line 180), add a new section:

```css
/* ─── Hero layout ────────────────────────────────────────── */
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
  text-align: left;
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

- [ ] **Step 3: Update mobile breakpoint in `styles.css`**

Find the existing `@media (max-width: 640px)` block (line 257–266). Update `h1` in-place and add the two hero rules:

```css
@media (max-width: 640px) {
  nav { padding: 0 20px; }
  .nav-links .hide-mobile { display: none; }
  h1 { font-size: 32px; letter-spacing: -0.5px; }
  h2 { font-size: 24px; }
  .section-inner { padding: 48px 20px; }
  .hero-inner { flex-direction: column; }
  .hero-phone { display: none; }
  .email-form { flex-direction: column; }
  footer { padding: 24px 20px; flex-direction: column; align-items: flex-start; }
  .prose { padding: 40px 20px; }
}
```

- [ ] **Step 4: Verify in browser**

Open `index.html`. The hero section still looks like the old single-column layout (hero HTML hasn't changed yet), but:
- Headline text should be noticeably larger (52px vs 44px)
- No visual regressions on other sections

- [ ] **Step 5: Commit**

```bash
git add styles.css
git commit -m "feat: add hero layout CSS and update h1 typography"
```

---

## Task 3: Hero HTML restructure (copy column only)

**Files:**
- Modify: `index.html` (hero section — replace `section-inner` with `hero-inner` two-column skeleton, copy column only, empty phone column)

- [ ] **Step 1: Replace the hero section interior in `index.html`**

Find the hero section as it exists after Task 1 (emoji already replaced with `<i>` tag):
```html
  <!-- HERO -->
  <section style="background: var(--hero-gradient);">
    <div class="section-inner">
      <div class="hero-badge"><i class="ti ti-device-mobile"></i> Coming to App Store</div>
      <h1>Track your meds.<br/><span style="color: #fff3cc;">Find what works.</span></h1>
      <p class="lead">ZORA helps you understand your medication routine so you can feel your best — and actually communicate what's working to the people helping you.</p>
      <div style="display: flex; gap: 12px; justify-content: center; flex-wrap: wrap;">
        <a href="#notify"><button class="btn-primary">Notify Me at Launch</button></a>
        <a href="#how-it-works"><button class="btn-ghost">Learn More</button></a>
      </div>
    </div>
  </section>
```

Replace with:
```html
  <!-- HERO -->
  <section style="background: var(--hero-gradient);">
    <div class="hero-inner">

      <!-- Left: copy -->
      <div class="hero-copy">
        <div class="hero-badge"><i class="ti ti-device-mobile"></i> Coming to App Store</div>
        <h1>Track your meds.<br/><span style="color: #fff3cc;">Find what works.</span></h1>
        <p class="lead">ZORA helps you understand your medication routine so you can feel your best — and actually communicate what's working to the people helping you.</p>
        <div class="hero-actions">
          <a href="#notify"><button class="btn-primary">Notify Me at Launch</button></a>
          <a href="#how-it-works"><button class="btn-ghost">Learn More</button></a>
        </div>
      </div>

      <!-- Right: phone mockup (added in Task 4) -->
      <div class="hero-phone"></div>

    </div>
  </section>
```

- [ ] **Step 2: Verify in browser**

Open `index.html`. Confirm:
- Hero text is left-aligned (not centered)
- Badge, headline, lead paragraph, and two buttons all display correctly
- The right column is empty (phone comes next task)
- No visual regressions on other sections
- On mobile (resize to < 640px): hero stacks vertically, content is readable

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: restructure hero to two-column layout"
```

---

## Task 4: Phone mockup HTML

**Files:**
- Modify: `index.html` — fill in the `.hero-phone` div with the complete phone mockup

This is the most complex task. The entire mockup uses inline styles — nothing added to `styles.css`. Tabler icon classes are already available from Task 1's CDN link.

- [ ] **Step 1: Replace the empty `.hero-phone` div with the full mockup**

Find:
```html
      <!-- Right: phone mockup (added in Task 4) -->
      <div class="hero-phone"></div>
```

Replace with:
```html
      <!-- Right: phone mockup -->
      <div class="hero-phone">
        <div style="width:200px;height:410px;overflow:hidden;background:#ffffff;border-radius:36px;border:5px solid rgba(255,255,255,0.4);box-shadow:0 30px 60px rgba(0,0,0,0.3),0 0 0 1px rgba(0,0,0,0.06);display:flex;flex-direction:column;">

          <!-- Status bar -->
          <div style="background:white;padding:10px 16px 4px;display:flex;justify-content:space-between;align-items:center;flex-shrink:0;">
            <span style="color:#1c1c1e;font-size:9px;font-weight:600;">9:41</span>
            <div style="display:flex;gap:4px;align-items:center;">
              <svg width="12" height="8" viewBox="0 0 12 8" fill="#1c1c1e"><rect x="0" y="5" width="2" height="3" rx="0.5"/><rect x="3" y="3" width="2" height="5" rx="0.5"/><rect x="6" y="1" width="2" height="7" rx="0.5"/><rect x="9" y="0" width="2" height="8" rx="0.5"/></svg>
              <svg width="16" height="8" viewBox="0 0 16 8" fill="none"><rect x="0" y="1" width="13" height="6" rx="1.5" stroke="#1c1c1e" stroke-width="0.8"/><rect x="1" y="2" width="9" height="4" rx="0.8" fill="#1c1c1e"/><path d="M14 3v2" stroke="#1c1c1e" stroke-width="1" stroke-linecap="round"/></svg>
            </div>
          </div>

          <!-- Nav bar -->
          <div style="background:white;padding:2px 14px 8px;display:flex;justify-content:space-between;align-items:center;flex-shrink:0;">
            <span style="font-size:14px;font-weight:900;color:#5DABFE;letter-spacing:1.5px;">ZORA</span>
            <i class="ti ti-settings" style="color:#8e8e93;font-size:14px;"></i>
          </div>

          <!-- Month nav -->
          <div style="background:white;padding:0 14px 6px;display:flex;justify-content:space-between;align-items:center;flex-shrink:0;">
            <i class="ti ti-chevron-left" style="color:#8e8e93;font-size:12px;"></i>
            <span style="color:#1c1c1e;font-size:11px;font-weight:600;">March 2026</span>
            <i class="ti ti-chevron-right" style="color:#8e8e93;font-size:12px;"></i>
          </div>

          <!-- Weekday bar -->
          <div style="background:white;display:grid;grid-template-columns:repeat(7,1fr);padding:0 6px 4px;flex-shrink:0;">
            <div style="text-align:center;font-size:7px;font-weight:600;color:#8e8e93;">S</div>
            <div style="text-align:center;font-size:7px;font-weight:600;color:#8e8e93;">M</div>
            <div style="text-align:center;font-size:7px;font-weight:600;color:#8e8e93;">T</div>
            <div style="text-align:center;font-size:7px;font-weight:600;color:#8e8e93;">W</div>
            <div style="text-align:center;font-size:7px;font-weight:600;color:#8e8e93;">T</div>
            <div style="text-align:center;font-size:7px;font-weight:600;color:#8e8e93;">F</div>
            <div style="text-align:center;font-size:7px;font-weight:600;color:#8e8e93;">S</div>
          </div>

          <!-- Divider -->
          <div style="height:0.5px;background:#e5e5ea;flex-shrink:0;margin:0 10px 2px;"></div>

          <!-- Calendar grid: March 2026 starts Sunday -->
          <!-- Green=rgba(52,199,89,0.18) Yellow=rgba(255,204,0,0.22) Red=rgba(255,59,48,0.15) -->
          <!-- Logged: green 8,9,12,15,16,18,20,21,23,24,26,27 | yellow 11,19,25 | red 14,22 | selected(blue) 28 | plain 1-7,10,13,17,29-31 -->
          <div style="background:white;display:grid;grid-template-columns:repeat(7,1fr);padding:2px 4px;flex-shrink:0;">
            <!-- Row 1: 1-7 unlogged -->
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><span style="font-size:9px;color:#1c1c1e;">1</span></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><span style="font-size:9px;color:#1c1c1e;">2</span></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><span style="font-size:9px;color:#1c1c1e;">3</span></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><span style="font-size:9px;color:#1c1c1e;">4</span></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><span style="font-size:9px;color:#1c1c1e;">5</span></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><span style="font-size:9px;color:#1c1c1e;">6</span></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><span style="font-size:9px;color:#1c1c1e;">7</span></div>
            <!-- Row 2: 8 green, 9 green, 10 plain, 11 yellow, 12 green, 13 plain, 14 red -->
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><div style="width:20px;height:20px;background:rgba(52,199,89,0.18);border-radius:50%;display:flex;align-items:center;justify-content:center;"><span style="font-size:9px;font-weight:600;color:#1c1c1e;">8</span></div></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><div style="width:20px;height:20px;background:rgba(52,199,89,0.18);border-radius:50%;display:flex;align-items:center;justify-content:center;"><span style="font-size:9px;font-weight:600;color:#1c1c1e;">9</span></div></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><span style="font-size:9px;color:#1c1c1e;">10</span></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><div style="width:20px;height:20px;background:rgba(255,204,0,0.22);border-radius:50%;display:flex;align-items:center;justify-content:center;"><span style="font-size:9px;font-weight:600;color:#1c1c1e;">11</span></div></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><div style="width:20px;height:20px;background:rgba(52,199,89,0.18);border-radius:50%;display:flex;align-items:center;justify-content:center;"><span style="font-size:9px;font-weight:600;color:#1c1c1e;">12</span></div></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><span style="font-size:9px;color:#1c1c1e;">13</span></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><div style="width:20px;height:20px;background:rgba(255,59,48,0.15);border-radius:50%;display:flex;align-items:center;justify-content:center;"><span style="font-size:9px;font-weight:600;color:#1c1c1e;">14</span></div></div>
            <!-- Row 3: 15 green, 16 green, 17 plain, 18 green, 19 yellow, 20 green, 21 green -->
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><div style="width:20px;height:20px;background:rgba(52,199,89,0.18);border-radius:50%;display:flex;align-items:center;justify-content:center;"><span style="font-size:9px;font-weight:600;color:#1c1c1e;">15</span></div></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><div style="width:20px;height:20px;background:rgba(52,199,89,0.18);border-radius:50%;display:flex;align-items:center;justify-content:center;"><span style="font-size:9px;font-weight:600;color:#1c1c1e;">16</span></div></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><span style="font-size:9px;color:#1c1c1e;">17</span></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><div style="width:20px;height:20px;background:rgba(52,199,89,0.18);border-radius:50%;display:flex;align-items:center;justify-content:center;"><span style="font-size:9px;font-weight:600;color:#1c1c1e;">18</span></div></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><div style="width:20px;height:20px;background:rgba(255,204,0,0.22);border-radius:50%;display:flex;align-items:center;justify-content:center;"><span style="font-size:9px;font-weight:600;color:#1c1c1e;">19</span></div></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><div style="width:20px;height:20px;background:rgba(52,199,89,0.18);border-radius:50%;display:flex;align-items:center;justify-content:center;"><span style="font-size:9px;font-weight:600;color:#1c1c1e;">20</span></div></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><div style="width:20px;height:20px;background:rgba(52,199,89,0.18);border-radius:50%;display:flex;align-items:center;justify-content:center;"><span style="font-size:9px;font-weight:600;color:#1c1c1e;">21</span></div></div>
            <!-- Row 4: 22 red, 23 green, 24 green, 25 yellow, 26 green, 27 green, 28 selected(blue) -->
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><div style="width:20px;height:20px;background:rgba(255,59,48,0.15);border-radius:50%;display:flex;align-items:center;justify-content:center;"><span style="font-size:9px;font-weight:600;color:#1c1c1e;">22</span></div></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><div style="width:20px;height:20px;background:rgba(52,199,89,0.18);border-radius:50%;display:flex;align-items:center;justify-content:center;"><span style="font-size:9px;font-weight:600;color:#1c1c1e;">23</span></div></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><div style="width:20px;height:20px;background:rgba(52,199,89,0.18);border-radius:50%;display:flex;align-items:center;justify-content:center;"><span style="font-size:9px;font-weight:600;color:#1c1c1e;">24</span></div></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><div style="width:20px;height:20px;background:rgba(255,204,0,0.22);border-radius:50%;display:flex;align-items:center;justify-content:center;"><span style="font-size:9px;font-weight:600;color:#1c1c1e;">25</span></div></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><div style="width:20px;height:20px;background:rgba(52,199,89,0.18);border-radius:50%;display:flex;align-items:center;justify-content:center;"><span style="font-size:9px;font-weight:600;color:#1c1c1e;">26</span></div></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><div style="width:20px;height:20px;background:rgba(52,199,89,0.18);border-radius:50%;display:flex;align-items:center;justify-content:center;"><span style="font-size:9px;font-weight:600;color:#1c1c1e;">27</span></div></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><div style="width:20px;height:20px;background:#5DABFE;border-radius:50%;display:flex;align-items:center;justify-content:center;"><span style="font-size:9px;font-weight:700;color:white;">28</span></div></div>
            <!-- Row 5: 29-31 future/unlogged -->
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><span style="font-size:9px;color:#1c1c1e;">29</span></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><span style="font-size:9px;color:#1c1c1e;">30</span></div>
            <div style="display:flex;align-items:center;justify-content:center;height:24px;"><span style="font-size:9px;color:#1c1c1e;">31</span></div>
            <div></div><div></div><div></div><div></div>
          </div>

          <!-- Bottom sheet -->
          <div style="background:#fefcfe;border-radius:18px 18px 0 0;flex:1;padding:8px 14px 0;box-shadow:0 -4px 20px rgba(0,0,0,0.1);overflow:hidden;">
            <!-- Drag handle -->
            <div style="width:28px;height:3px;background:#d1d1d6;border-radius:2px;margin:0 auto 8px;"></div>
            <!-- Date + Edit -->
            <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:8px;">
              <span style="font-size:10px;font-weight:600;color:#1c1c1e;">Today, March 28</span>
              <span style="font-size:9px;color:#5DABFE;font-weight:500;">Edit</span>
            </div>
            <!-- Overall score -->
            <div style="margin-bottom:6px;">
              <div style="font-size:7px;font-weight:500;color:#8e8e93;text-transform:uppercase;letter-spacing:0.5px;margin-bottom:1px;">Overall</div>
              <div style="display:flex;align-items:baseline;gap:3px;">
                <span style="font-size:20px;font-weight:700;color:#34c759;line-height:1;">4.2</span>
                <span style="font-size:8px;color:#c7c7cc;">/ 5</span>
              </div>
            </div>
            <!-- Divider -->
            <div style="height:0.5px;background:#e5e5ea;margin-bottom:6px;"></div>
            <!-- Medication rows -->
            <div style="display:flex;align-items:center;gap:5px;margin-bottom:5px;">
              <i class="ti ti-pill" style="font-size:11px;color:#5DABFE;flex-shrink:0;"></i>
              <span style="font-size:8px;font-weight:500;color:#1c1c1e;">Sertraline  •  50mg  •  Morning</span>
            </div>
            <div style="display:flex;align-items:center;gap:5px;margin-bottom:8px;">
              <i class="ti ti-pill" style="font-size:11px;color:#5DABFE;flex-shrink:0;"></i>
              <span style="font-size:8px;font-weight:500;color:#1c1c1e;">Wellbutrin  •  150mg  •  Morning</span>
            </div>
            <!-- Divider -->
            <div style="height:0.5px;background:#e5e5ea;margin-bottom:6px;"></div>
            <!-- Metric bars -->
            <div style="display:flex;flex-direction:column;gap:5px;">
              <!-- Mood: 5/5 -->
              <div>
                <div style="display:flex;justify-content:space-between;margin-bottom:2px;">
                  <span style="font-size:7px;font-weight:500;color:#8e8e93;">Mood</span>
                  <span style="font-size:8px;font-weight:700;color:#34c759;">5</span>
                </div>
                <div style="height:5px;background:#f2f2f7;border-radius:3px;position:relative;">
                  <div style="width:100%;height:100%;background:linear-gradient(to right,#ff3b30,#ffcc00,#34c759);border-radius:3px;"></div>
                  <div style="position:absolute;right:-3px;top:-2px;width:9px;height:9px;background:white;border-radius:50%;box-shadow:0 1px 3px rgba(0,0,0,0.25);"></div>
                </div>
              </div>
              <!-- Energy: 4/5 -->
              <div>
                <div style="display:flex;justify-content:space-between;margin-bottom:2px;">
                  <span style="font-size:7px;font-weight:500;color:#8e8e93;">Energy</span>
                  <span style="font-size:8px;font-weight:700;color:#34c759;">4</span>
                </div>
                <div style="height:5px;background:#f2f2f7;border-radius:3px;position:relative;">
                  <div style="width:75%;height:100%;background:linear-gradient(to right,#ff3b30,#ffcc00,#34c759);border-radius:3px;"></div>
                  <div style="position:absolute;left:calc(75% - 4px);top:-2px;width:9px;height:9px;background:white;border-radius:50%;box-shadow:0 1px 3px rgba(0,0,0,0.25);"></div>
                </div>
              </div>
              <!-- Sleep: 3/5 -->
              <div>
                <div style="display:flex;justify-content:space-between;margin-bottom:2px;">
                  <span style="font-size:7px;font-weight:500;color:#8e8e93;">Sleep</span>
                  <span style="font-size:8px;font-weight:700;color:#ffcc00;">3</span>
                </div>
                <div style="height:5px;background:#f2f2f7;border-radius:3px;position:relative;">
                  <div style="width:50%;height:100%;background:linear-gradient(to right,#ff3b30,#ffcc00,#34c759);border-radius:3px;"></div>
                  <div style="position:absolute;left:calc(50% - 4px);top:-2px;width:9px;height:9px;background:white;border-radius:50%;box-shadow:0 1px 3px rgba(0,0,0,0.25);"></div>
                </div>
              </div>
            </div>
          </div><!-- /bottom sheet -->

        </div><!-- /phone outer shell -->
      </div><!-- /hero-phone -->
```

- [ ] **Step 2: Verify in browser**

Open `index.html`. Confirm:
- Phone mockup appears to the right of the hero copy
- White background, rounded corners, drop shadow
- Blue "ZORA" wordmark in the phone nav bar
- Calendar shows green/yellow/red tinted circles on logged days, solid blue on day 28
- Bottom sheet shows overall score 4.2, two medication rows with pill icons, three metric bars
- On mobile (< 640px): phone is hidden, copy stacks full-width

- [ ] **Step 3: Commit and push**

```bash
git add index.html
git commit -m "feat: add phone app mockup to hero section"
git push origin main
```
