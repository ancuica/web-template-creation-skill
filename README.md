# web-template-creation-skill

> [!NOTE]
> This skill is now part of a combined project — the full **analyze → template → audit** loop lives at **[ancuica/web-design-pipeline](https://github.com/ancuica/web-design-pipeline)** (see `skills/web-template-creator`). This standalone repo remains available, but new work happens in the combined project.

An [agent skill](https://docs.anthropic.com/en/docs/agents-and-tools/agent-skills/overview) that turns a **website-analysis note** into a **reusable website template package** — markdown files that wrap HTML, a config of `{{PLACEHOLDER}}` keys, a style guide, and a one-shot extractor. It captures a site's *design system* so you can reproduce the look for your own brand with your own art and copy — not a clone.

## What it does

Given an analysis describing a website's **artistic decisions** (typography, color, layout, imagery, motion, iconography, naming) and **philosophical decisions** (mission, voice, theory of commerce, posture), plus the site's defining **"one move"**, the skill produces:

```
your-template/
├── README.md              ← what it's for, quick start, site map, philosophy
├── config.md              ← every {{PLACEHOLDER}}, grouped + commented
├── style-guide.md         ← the analysis turned into do/don't rules
├── extract.md             ← awk snippet: pages/*.md → *.html
├── pages/*.md             ← one HTML doc per page, wrapped in a ```html fence
└── example/config.filled.md
```

Every page is a markdown file wrapping one complete HTML document; no build step, no framework, one inline `<style>` per page.

## Files

| File | Purpose |
| ---- | ------- |
| [`SKILL.md`](./SKILL.md) | The skill: frontmatter (`name`, `description`) + when-to-use, procedure, page rules, verification. |
| [`reference.md`](./reference.md) | The verbatim paste-ready prompt and a worked example. |

## Install

Drop the folder into your agent's skills directory, e.g.:

```shell
git clone https://github.com/ancuica/web-template-creation-skill.git
cp -r web-template-creation-skill ~/.pi/agent/skills/web-template-creation
# then restart your agent or run /reload
```

(Path varies by agent — adjust to wherever your tool loads skills.)

## Use

1. Have (or write) a website-analysis note covering the artistic + philosophical decisions and the "one move."
2. Invoke the skill with that analysis as input.
3. Fill in the generated `config.md`, run the `extract.md` snippet, drop in your own art, and deploy the static HTML anywhere.

## Scope

Template creation **only**. The skill does not scrape live sites, download assets, or build local demos/mirrors — by design, so it stays a clean authoring step you can point at any analysis.

## Provenance

Distilled from building a template out of a real teardown (texture *"Photocopied metal reliquary"*; one move = an editorial collage page that smuggles products inside the décor). See [`reference.md`](./reference.md) for the worked example.

## License

[MIT](./LICENSE).
