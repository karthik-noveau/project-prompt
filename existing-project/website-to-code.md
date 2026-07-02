# Live URL → code: ready-to-paste CLI prompts

Fill in `[URL]`, `[SCREEN/FLOW NAME]`, `[PATH]`. Paste one step at a time, reviewing between each.

---

## Step 1 — Extract ground truth

```
Fetch the live reference at [URL]. If it's client-rendered, a plain fetch only returns an empty
shell — drive it with a real/headless browser, or download its built JS/CSS bundles (fetch the
HTML, find linked script/stylesheet URLs, pull them) and grep for the real copy, class names,
exact colors/spacing, and animation logic (@keyframes, animateTransform, timing).

Summarize: literal copy, the flow's screens/states in order, and exact style values for anything
visual. Flag anything needing live data/backend behavior we don't have — before building.
```

---

## Step 2 — Implement with this codebase's own conventions

```
Using the extraction above, implement [SCREEN/FLOW NAME] in [PATH] with this codebase's existing
components/tokens — never copy the reference's raw framework output (its CSS classes, arbitrary
px values, its component library). Map each extracted value to the nearest equivalent we already
have; add something new only if nothing close exists. Pass this repo's lint/type-check before
calling it done.
```

---

## Step 3 — Verify both directions

```
Verify [SCREEN/FLOW NAME] against [URL]:
1. Drive our implementation through the real flow in a browser and screenshot each state.
2. Drive the live reference through the same flow and screenshot the same states.
3. Compare side by side; list concrete mismatches (proportions, color, spacing, shape, animation)
   — not impressions. For animation, prove motion with computed styles or two time-separated
   screenshots, not one still frame.
Report the mismatch list before changing anything.
```

---

## Step 4 — Fix and re-verify

```
Fix only the mismatches found above — no unrequested "improvements" beyond what the reference
shows. Re-screenshot both sides and re-compare. Repeat fix → re-verify until they match, or state
explicitly why a remaining difference is intentional.
```

---

## Technique notes

- **Static fetch ≠ real UI.** Client-rendered apps need a real browser or their compiled bundles —
  source is more precise than eyeballing a screenshot anyway.
- **Login-gated live app:** headless = no cookies = login wall. Launch a real browser with remote
  debugging on a throwaway profile, log in manually once, then connect programmatically (CDP /
  puppeteer / playwright) and drive it — you never touch the actual credentials.
- **Stale tabs.** Repeated runs leave old tabs open. Match the exact target/page id you just
  created before driving it, or you'll silently screenshot the wrong (blank/outdated) tab.
- **Animation proof needs two samples.** One screenshot can't show motion. Also confirm it's
  actually *visible* (a correct rotation between two similar-lightness shades of one hue can be
  imperceptible at small sizes) — running ≠ perceptible.
- **Don't substitute your own values** when copying an effect — an unannounced "improvement"
  reintroduces the mismatch you were asked to fix.
- **Scope discipline.** Small CSS/token fixes: just do them. Layout restructuring, new visual
  patterns, or anything needing backend data that doesn't exist: ask first.
