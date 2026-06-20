---
name: template-creation-prompt
description: Turn a website-analysis note into a reusable, copy-pasteable website template package (markdown files that wrap HTML, a config of placeholders, a style guide, and an extractor). Use when the user has an analysis of a website's artistic + philosophical decisions and wants a buildable template that reproduces the *design system* (not a clone) for their own brand.
---

# Template Creation Prompt

Convert a **website-analysis document** into a **reusable website template package**. Scope is template creation only — this skill does **not** scrape live sites, download assets, or build demos/mirrors.

## When to use

- The user points at a website-analysis note (artistic decisions: typography, color, layout, imagery, motion, iconography, naming; philosophical decisions: mission, voice, theory of commerce, posture; plus a named **"one move"**).
- They want a template they can fill in for their own brand and deploy as plain static HTML.

If no analysis exists yet, ask for one (or for the URL + permission to analyze) before proceeding.

## Conventions to match

Mirror the `jvscholz-website-template` packaging exactly:

- Each page is a **markdown file** wrapping **one complete HTML document** in a single fenced ` ```html ` block.
- All variable content is a `{{PLACEHOLDER}}` key — never hard-coded.
- A shared `:root` block holds palette + font stack as CSS custom properties; a shared `<header>`/`<nav>` shell is copied into every page.
- No build step, no CSS framework, no JS framework. One inline `<style>` per page; JS only if the design truly needs it.
- Output **markdown files only**.

## Procedure

1. **Read the analysis end to end.** Extract: the one-line texture/verdict, the named **one move**, the palette, the font system, every layout grammar, the voice registers (and where each appears), the naming system, and the commerce posture.

2. **Produce these files:**
   - **`README.md`** — what it's for, who uses it, a `Contents` tree, numbered `Quick start`, the `Site map produced`, and a `Philosophy` paragraph naming the texture + one move.
   - **`config.md`** — every `{{PLACEHOLDER}}` grouped by section (Identity, Palette, Fonts, Brand marks & props, then one block per content type). Each value gets an inline comment encoding the design intent and constraints (e.g. "two-tone only, no third hue"; "load all faces, use simultaneously"). Keep any source copy that has deliberate quirks.
   - **`style-guide.md`** — translate the analysis into **rules**: one section per artistic decision and per philosophical decision, each stating the decision then the do/don't. Include a **"What to keep vs. what to fix"** table separating intentional *posture* from real *neglect*. Surface judgement calls the source dodged (contested content, voice fatigue) and tell the implementer to decide deliberately. End with a **Commerce & security** note if the site transacts.
   - **`extract.md`** — a one-shot `awk` snippet ripping the inner HTML from each `pages/*.md` into `*.html`, a per-item loop for repeated page types (one product/post per file), and post-extraction deploy steps.
   - **`pages/*.md`** — one file per page in the site map (see "Page rules" below).
   - **`example/config.filled.md`** — a worked example filling every key for a *fictional* brand that keeps the source's posture without copying its actual (or sensitive/contested) inventory.

3. **Page rules** (each `pages/*.md` must implement the analysis faithfully):
   - Build a dedicated page for the **"one move"** and make it the centerpiece. Do not water it down.
   - Reproduce **every layout grammar** the site uses, even contradictory ones on the same site.
   - Honor the **voice registers** exactly, including which register appears on which page.
   - Accessibility for free: `alt` on images, `aria-hidden` on pure ornament, keyboard-reachable links with focus outlines, empty `alt` on decorative props.
   - **Fix** genuine defects (typos repeated site-wide, legal links to unfinished URLs). **Keep** intentional posture (loose taunts, mismatched prop scales).

4. **Verify before finishing:** each `pages/*.md` has exactly **one** ` ```html ` fence that opens with `<!DOCTYPE html>` and closes with `</html>`. Report the check.

## Rules

- Capture the **system**, not a clone — describe the look precisely enough to reproduce with original art and copy.
- Flag any network-exposed or transactional surface and its security implication, even if unasked (never capture cards on a static page; use a hosted checkout; escape user-echoed values).
- Pick reasonable defaults for minor choices and note them rather than stalling.

## Reference

See `reference.md` for the full prompt text and the worked re-animators.net result (texture "Photocopied metal reliquary"; one move = the Lore collage page that smuggles products inside the décor).
