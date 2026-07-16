---
name: alt-text
description: Write, review, or fix alt text for images in HTML, Markdown, or other documents. Use when adding images to content, generating image descriptions, auditing accessibility, or when asked about alt text, image descriptions, or text alternatives for screen reader users.
---

# Writing alt text

Alt text is a **replacement** for the image, not a description of it. The test: imagine reading the page aloud over the phone without mentioning that an image is present — the alt text is what you say in the image's place. If swapping every image for its alt text would leave the page's meaning unchanged, the alt text is right.

There is no single correct alt text for an image. The same logo needs `alt="The XYZ company"` as a page heading, `alt=""` next to the company's name, and a visual description in an article about the logo's design. Determine the image's purpose in context first; only then write.

## Decision procedure

Work through these in order; the first match decides the approach.

1. **Functional — is the image inside a link or button?** Alt conveys the action or destination, not the picture: a printer icon that prints gets `Print`, not `Printer icon`. If adjacent text already states the function, alt carries only the image's added information (`PDF`) or is empty. An image that is a link's *only* content must never have empty alt — derive the alt from the link's destination if nothing else is available.
2. **Decorative or redundant?** If removing the image loses no information, or its content is already in adjacent text or a caption, use `alt=""`. Describing decorative images adds noise, and duplicating a caption makes screen reader users hear it twice.
3. **Contains text?** Reproduce it verbatim — for memes and screenshots of text this is the single most important rule. Then, if useful, add the visual context (for memes: the base image or character and the action). If the identical text appears as real text nearby, the image is redundant → `alt=""`.
4. **Logo?** Alt is the entity's name (`Acme Corporation`), never the word "logo" — the logo conveys the entity, not its own logo-ness.
5. **Complex — chart, graph, diagram, map, infographic?** Use the two-part pattern in the next section. Don't try to fit it all in alt.
6. **Informative photo or illustration?** Brief description of what matters *for this context*: a bird photo on a parks site needs only a passing mention; the same photo on a birding site needs plumage detail. Detail that doesn't serve the page's purpose is noise.
7. **Key content — gallery, comic, artwork, a screenshot being discussed?** Full replacement text conveying everything the image contributes.
8. **Purpose genuinely undeterminable** (no surrounding context available)? Write a purpose-neutral factual description, transcribe any visible text, and flag low confidence for human review. Never invent a purpose or context to justify richer detail.

Context to gather before deciding, in priority order: the parent element (link? button?) and any link target; caption or `figcaption`; nearest heading and surrounding paragraphs; the page's topic; sibling images' alt (for consistency across a set); text visible inside the image.

## Writing rules

- Front-load the most important information — alt text can't be skimmed or re-read piecemeal; listeners hear it start to finish or start over.
- Write full, punctuated phrases and end with a period so the screen reader pauses before the next element. Avoid ALL-CAPS (may be spelled letter-by-letter) and runs of special characters.
- No "image of…" / "photo of…" prefix — screen readers already announce the role. Name the medium only when it's itself meaningful (a painting vs. a photograph of the same scene).
- The 125/150/250-character "limits" are folklore (no modern screen reader truncates alt), but brevity is still right: if the purpose needs more than a sentence or two, treat it as a complex image instead of writing longer alt.
- Mention color only when it carries meaning ("the error state is marked with a red border" — yes; a subject's shirt color — usually no). If the image uses color alone to distinguish things, the alt must convey that distinction without relying on color.
- Match the language of the surrounding content.
- Never output: filenames, `alt="image"`/`"photo"`/`"spacer"`, SEO keyword lists, a verbatim copy of the adjacent caption, or any detail you can't verify from the image itself — names of people or places, dates, emotions or intent not visibly evident. Transcribing text you can read is high-confidence; identifying who someone is from their face is not.

## Complex images (charts, diagrams, maps, infographics)

Use two parts:

1. **Short alt** identifying the image and pointing to the description: chart type, title, what's plotted — `alt="Bar chart showing monthly and total visitors for the first quarter for sites 1 to 3. Details in the following table."`
2. **Long description** carrying the content: the statistics (extrema, outliers, key comparisons) and the trends in plain language ("site 1 declines steadily while site 3 grows"). Research with blind readers (Lundgard & Satyanarayan 2022) found they most value exactly this middle level — stats and trends — over both design-element inventories and high-level editorial conclusions. Leave causal interpretation ("the spike was caused by…") out unless the source material states it.

Put the long description in visible adjacent text when possible (it helps everyone); otherwise `aria-describedby` pointing to on-page text, or a `<details>` disclosure. Never use `longdesc` — it's obsolete. Exhaustive data points belong in an adjacent or linked data table, not in prose.

For maps: describe the purpose and the spatial relationships relevant to the task (the route, the affected region), not the geography pixel-by-pixel.

## Describing people

Don't assert race, gender, age, or disability from appearance — screen reader users' preferences here vary and misidentification is harmful. When appearance is relevant, prefer concrete observable features ("a person with dark skin tone and long braids", "a person using a wheelchair") over identity categories. Use identity terms only when the surrounding context already establishes them (a caption naming the person, an article about them) or when identity is central to the image's meaning — a photo of Elizabeth Eckford and the Little Rock Nine is *about* race, and omitting it would erase the point. When identity seems salient but unestablished, describe observably and flag for human review.

## Mechanics: HTML and Markdown

- `alt=""` and a *missing* alt attribute are different: empty alt tells assistive technology to skip the image; missing alt makes screen readers fall back to announcing the filename or URL. Decorative → always `alt=""`. Truly-unknown → omitting alt is the spec's honest-failure path, but flag it rather than filling in phony text.
- Markdown `![](image.png)` renders as empty alt — that's the decorative form. For anything needing a caption, `aria-describedby`, or `<details>`, drop to inline HTML.
- Inline SVG and other non-`img` images: `role="img"` with `aria-label` on the outer element. Decorative icons inside an already-labeled control: `aria-hidden="true"`.
- `figcaption` is a visible complement to alt, not a substitute — the two must not duplicate each other, and pairing a `figcaption` with `alt=""` sends contradictory signals.
- Don't put descriptions in the `title` attribute (inconsistently read, hover-only). Don't write "AI-generated" inside the alt string — surface provenance and confidence in your response to the user, outside the alt text itself.
