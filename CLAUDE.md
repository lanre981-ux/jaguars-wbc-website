# CLAUDE.md — Web Design Standards

## Prime directive
Every site must look **deliberately designed**, not generated. If a stranger could guess it was AI-built in under three seconds, it has failed. Start from a stated design point of view and defend every choice.

## Hard bans — the "vibe-coded" tells
Never ship any of these:

- **Purple.** No violet, indigo, or lavender as a primary or accent. No `#6366f1`, `#8b5cf6`, `#a855f7`.
- **Purple/blue gradients.** No `linear-gradient(to right, #667eea, #764ba2)` or any relative of it. No gradient text headlines.
- Glowing/blurred blobs behind hero sections.
- Glassmorphism cards floating on a dark mesh background.
- Default Tailwind palette used raw (`bg-blue-500`, `text-gray-600`) with no custom tokens.
- Emoji as feature icons.
- A rounded-`2xl` card grid of three "features" with identical icon + heading + two lines of filler.
- Centered everything, 800px column, nothing else.
- Rocket ships, sparkles, "Supercharge your workflow" copy.
- Drop shadows on every element.

If the design brief genuinely calls for purple (client brand, provided reference), it's allowed — but only when explicitly justified by the user's material.

## Color
- Build a palette of 2–4 real colors plus neutrals. Commit to one dominant hue.
- Neutrals should be tinted, not pure grey. Warm off-whites (`#faf8f5`) and true blacks beat `#f9fafb`.
- Contrast must pass WCAG AA (4.5:1 body, 3:1 large text). Verify, don't assume.
- Use color sparingly for emphasis, not decoration.

## Typography — always beautiful, never default
- **Never** ship system-ui, Arial, Helvetica, or Inter-by-default as the display face.
- Pick a real typeface with character. Reliable choices:
  - Serif display: Fraunces, Instrument Serif, Playfair Display, GT Sectra, Newsreader
  - Sans display: Satoshi, General Sans, Space Grotesk, Söhne, Neue Haas
  - Body: Söhne, Inter (body only), Source Serif, Literata, IBM Plex
  - Mono: Berkeley Mono, JetBrains Mono, IBM Plex Mono
- Maximum two families. Pair by contrast: serif display + clean sans body, or one family across weights.
- Set a real type scale (1.25 or 1.333 ratio). No arbitrary sizes.
- Body copy 16–20px, line-height 1.5–1.7, measure 60–75 characters.
- Headlines: tighten tracking (`-0.02em` to `-0.03em`), line-height 1.0–1.15.
- Load fonts properly: `font-display: swap`, preload the display face, subset if self-hosting.

## Layout
- Use an 8px spacing scale. Nothing off-grid.
- Whitespace is the design. Sections need room to breathe — generous vertical rhythm.
- Break the single-column default: asymmetry, editorial grids, offset images, full-bleed moments.
- Give the page a visual hierarchy that survives squinting at it from six feet away.

## Motion
- Subtle and purposeful. 150–300ms, `cubic-bezier(0.4, 0, 0.2, 1)` or similar.
- Animate opacity and transform only. Never layout properties.
- Respect `prefers-reduced-motion`.
- No parallax unless specifically requested.

## Responsive — non-negotiable
Every build must work on both. This is not an afterthought.

- Mobile-first CSS. Base styles are mobile; media queries add up.
- Test breakpoints: **375px, 768px, 1280px, 1920px**.
- Tap targets ≥44×44px.
- No horizontal scroll at any width. Ever.
- Type scales down on mobile — a 72px desktop headline is not a 72px mobile headline. Use `clamp()`.
- Navigation, tables, and multi-column layouts need real mobile treatments, not squashed desktop ones.
- Images: responsive `srcset`, correct aspect ratios, no layout shift.
- Check landscape phone and tablet portrait too.

## Design references
When the user provides a reference site, screenshot, Figma, or brand:

1. **Study it before writing code.** Name what makes it work: the palette, the type pairing, the spacing rhythm, the layout structure, the tone.
2. **Extract concrete tokens** — actual hex values, font families, spacing units, border radii, shadow treatments.
3. **Match the design language**, don't clone the layout. The goal is "clearly from the same world."
4. **State the interpretation** back to the user before building, so they can correct course early.
5. The reference **overrides** the defaults in this file, including the purple ban if the reference uses purple.

If no reference is given, ask for one or propose a specific direction ("editorial, warm neutrals, serif display") before building.

## Self-review — always, before saying it's done
After building, review the work. Do not skip this.

1. **Render and look at it.** Screenshot desktop and mobile. Actually inspect the output.
2. Run this checklist:
   - [ ] Zero purple/purple-gradient unless justified by the brief
   - [ ] Custom typeface loaded and rendering (not falling back)
   - [ ] Type scale consistent; no arbitrary font sizes
   - [ ] Contrast passes AA on every text/background pair
   - [ ] 375px: no overflow, no cramped text, tap targets adequate
   - [ ] 768px: layout transition is intentional, not broken
   - [ ] 1280px+: content doesn't stretch into unreadable measures
   - [ ] Spacing follows the scale — no one-off margins
   - [ ] Interactive states present: hover, focus-visible, active, disabled
   - [ ] Keyboard navigable; focus rings visible
   - [ ] Images have alt text and dimensions
   - [ ] No console errors
   - [ ] `prefers-reduced-motion` honored
   - [ ] Matches the provided reference's design language
3. **Fix what fails, then re-check.** Iterate until clean.
4. Report what was verified and anything left as a known limitation.

## Tone of the work
Restraint over decoration. One strong idea executed precisely beats five competing effects. If an element can be removed and the page still communicates, remove it.
