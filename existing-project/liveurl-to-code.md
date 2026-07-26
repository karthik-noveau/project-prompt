# Live URL → code

Fill `[URL]`, `[SCREEN]`, `[PATH]`. Paste one step at a time; review between each.

---

## 1 — Extract

```
Extract ground truth from [URL]. A plain fetch returns an empty shell on client-rendered pages —
drive a real browser, or pull the linked JS/CSS bundles and grep them.
Report: literal copy, every screen/state in order, exact colors, spacing, animation timing.
Flag anything needing data or backend we don't have. Write no code yet.
```

## 2 — Implement

```
Implement [SCREEN] in [PATH] from that extraction, using this repo's existing components and
tokens. Never copy the reference's CSS classes, arbitrary px values, or component library — map
each value to the nearest thing we already have; add something new only if nothing is close.
Pass lint and type-check before calling it done.
```

## 3 — Verify

```
Drive our [SCREEN] and [URL] through the same flow in a browser; screenshot every state on both
sides. List concrete mismatches — proportion, color, spacing, shape, motion — not impressions.
Prove animation with computed styles or two time-separated shots, never one still frame.
Report the list before changing anything.
```

## 4 — Fix

```
Fix only the listed mismatches. No unrequested improvements. Re-screenshot, re-compare, repeat
until they match — or state why a remaining difference is intentional.
```