# Alt Text Skill

An [Agent Skill](https://agentskills.io/) that teaches AI agents to write standards-compliant alt text for images in HTML and Markdown.

## What it does

When an agent with this skill adds images to content, reviews a page, or is asked to write image descriptions, it follows the decision procedure that accessibility standards actually prescribe — rather than defaulting to "describe the pixels":

- **Replacement, not description.** The governing principle from the [WHATWG HTML Living Standard §4.8.4.4](https://html.spec.whatwg.org/multipage/images.html#alt): alt text should let you replace the image without changing the page's meaning.
- **Category first, prose second.** Following the [W3C WAI alt decision tree](https://www.w3.org/WAI/tutorials/images/decision-tree/), the agent decides whether an image is functional, decorative, text-bearing, complex, or informative before writing anything — because the right answer is often `alt=""` or a link destination, not a description.
- **Short alt + long description for charts.** Complex images get a brief identifying alt plus a separate description carrying the statistics and trends — the content blind readers most value, per [Lundgard & Satyanarayan's research](https://doi.org/10.1109/TVCG.2021.3114770) ([PDF](https://vis.csail.mit.edu/pubs/vis-text-model/)).
- **Guardrails against the known failure modes** of AI-generated alt text: hallucinated detail, context-free descriptions, filenames, "image of…" prefixes, asserting people's identity from appearance, and duplicating captions.

## Why

Missing and poor alt text is consistently the most common accessibility failure on the web — the [WebAIM Million](https://webaim.org/projects/million/) survey finds roughly one in five home-page images has no text alternative at all. Multimodal agents now write a lot of the web's content, and their default behavior (fluent, context-free image descriptions) reproduces the exact anti-patterns that accessibility guidance warns about. This skill encodes the guidance from [WCAG 2.2](https://www.w3.org/WAI/WCAG22/Understanding/non-text-content.html), the HTML spec, [WebAIM](https://webaim.org/techniques/alttext/), and [Section508.gov](https://www.section508.gov/create/alternative-text/) into the compact form an agent needs at write time.

Accessibility practitioners broadly agree that automated alt text works best as a **reviewed draft**, and the skill is designed for that: it tells the agent to flag low-confidence output and surface assumptions rather than assert them.

## Installation

### Claude Code

Clone into your personal skills directory:

```bash
git clone https://github.com/brendanlong/alt-text-skill.git ~/.claude/skills/alt-text
```

Or add it to a single project (checked into the repo, shared with your team):

```bash
git clone https://github.com/brendanlong/alt-text-skill.git .claude/skills/alt-text
```

That's it — Claude Code discovers skills automatically. The skill activates when Claude works with images in Markdown or HTML, or you can invoke it explicitly by mentioning alt text. See the [Claude Code skills documentation](https://code.claude.com/docs/en/skills) for more on how skills are loaded.

### Other agents

Any tool that supports the [Agent Skills format](https://agentskills.io/) (a `SKILL.md` with YAML frontmatter) can use this skill — point it at the cloned directory.

## Sources

The skill distills:

- [WHATWG HTML Living Standard §4.8.4.4](https://html.spec.whatwg.org/multipage/images.html#alt) — the most detailed prescriptive spec, including guidance for markup generators
- [W3C WAI Images Tutorial](https://www.w3.org/WAI/tutorials/images/) and [alt decision tree](https://www.w3.org/WAI/tutorials/images/decision-tree/)
- [WCAG 2.2 SC 1.1.1 Non-text Content](https://www.w3.org/WAI/WCAG22/Understanding/non-text-content.html)
- [WebAIM: Alternative Text](https://webaim.org/techniques/alttext/)
- [Section508.gov: Authoring Meaningful Alternative Text](https://www.section508.gov/create/alternative-text/)
- Lundgard & Satyanarayan, [*Accessible Visualization via Natural Language Descriptions*](https://doi.org/10.1109/TVCG.2021.3114770) (IEEE TVCG 2022) — the four-level model of chart descriptions
- Bennett et al., [*"It's Complicated": Negotiating Accessibility and (Mis)Representation in Image Descriptions of Race, Gender, and Disability*](https://dl.acm.org/doi/10.1145/3411764.3445498) (CHI 2021)
- Eric Eggert, [*There is no character limit for "alt text"*](https://yatil.net/blog/there-is-no-character-limit-for-alt-text) — why the 125-character "rule" is folklore

## License

[MIT](LICENSE)
