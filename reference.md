# Reference — template-creation-prompt

Supporting material for `SKILL.md`. The verbatim prompt below can be pasted directly; the example records what it produced for re-animators.net.

## The prompt (verbatim)

> You are creating a **reusable website template** from an existing **website analysis** document.
>
> **Input:** a markdown analysis of one website describing its artistic decisions (typography, color, layout, imagery, motion, iconography, naming) and philosophical decisions (mission, voice, theory of commerce, posture toward imperfection/community/the internet), plus a named "one move" — the single structural idea that defines the site.
>
> **Output:** a self-contained template package, modelled on the conventions of the existing `jvscholz-website-template`:
>
> - Every page is a **markdown file** wrapping **one complete HTML document inside a single fenced ` ```html ` block**.
> - All variable content is expressed as `{{PLACEHOLDER}}` keys, never hard-coded.
> - A shared `:root` block carries the palette and font stack as CSS custom properties; a shared `<header>`/`<nav>` shell is copied into every page.
> - No build step, no CSS framework, no JS framework. One inline `<style>` per page; JS only if the design genuinely needs it.
>
> Produce: `README.md`, `config.md`, `style-guide.md`, `extract.md`, `pages/*.md` (one per page in the site map), and `example/config.filled.md`. (See `SKILL.md` for the required contents of each.)
>
> **Rules:**
> - Match the existing `jvscholz-website-template` packaging conventions exactly.
> - Capture the *system*, not a clone: describe the look precisely enough that someone can reproduce it with their own original art and copy.
> - Build a page for the site's "one move" and make it the centerpiece.
> - Reproduce every layout grammar and honor every voice register the analysis names.
> - Fix the source's genuine defects; keep its intentional posture.
> - Flag any network-exposed or transactional surface and its security implication, even if not asked.
> - Output only markdown files. Verify each `pages/*.md` has exactly one ` ```html ` fence opening with `<!DOCTYPE html>` and closing with `</html>`.

## Worked example — re-animators.net

- **Texture captured:** *"Photocopied metal reliquary."*
- **One move:** the **Lore** collage page that smuggles two products inside the décor as clickable cut-outs.
- **Files produced:** `README.md`, `config.md`, `style-guide.md`, `extract.md`, `pages/{index,shop,lore,product-page,faq,404}.md`, `example/config.filled.md`.
- **Conventions applied:** two-tone paper/ink/blood palette as `:root` vars; a kit-bash of five display faces used simultaneously; flat product grid vs. disordered collage as two coexisting layout grammars; clinical PDP spec sheet (with the source's repeated `LENGHT` typo fixed); all-caps FAQ; voice-slip 404. Three voice registers honored (cult-brochure / clinical-archivist / shitposter), each kept to its page.
- **Verification:** every `pages/*.md` extracted to one clean HTML document (`<!DOCTYPE html>` → `</html>`).

## Companion: input format

This skill expects an analysis shaped like the vault's `Δ/ART/*-analysis.md` notes — sections for each artistic decision, each philosophical decision, tensions/negative space, and an explicit "the one move" section. The richer the analysis, the more faithful the template.
