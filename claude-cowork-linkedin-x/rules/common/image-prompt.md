# Image Prompt Rules

Image prompts are text descriptions only. They are passed to an image generation pipeline (e.g. Nano Banana via n8n). Claude does not generate the image.

---

## Spec

- Style: hand-written note / infographic feel
- Background: light grid or off-white paper — no coffee stains, not always cream
- Headline: hand-lettered, bold, states the achievement or core insight
- Chart: one required — bar, pie, timeline, or flow — hand-drawn style
- Icons: hand-drawn for any tools, concepts, or steps mentioned
- Colours: multi-colour ink — navy, rust, teal, amber, yellow accents
- Feel: smart founder's notebook — not Canva, not corporate, not sketch
- Rule: image alone must tell the full story without reading the post
- Ratio: 4:5

---

## What Every Prompt Must Include

1. What the headline text says (exact wording)
2. What the chart shows — type (bar/pie/timeline/flow) AND actual data points
3. What icons appear and where on the page
4. Layout (top / centre-left / centre-right / bottom)
5. Colour for each element

---

## Bad Prompt (too vague)

"Smart founders notebook page, light grid background, navy headline, bar chart, hand-drawn icons, 4:5 ratio"

This tells the image model nothing specific. It will hallucinate generic content.

---

## Good Prompt (tells the full story)

"Hand-written infographic, 4:5 ratio, off-white grid paper background.

TOP: Bold hand-lettered headline in navy ink reads 'She Closed a $3M Brand. Built a $30M One in 24 Hours.'

CENTRE-LEFT: Hand-drawn timeline with 4 steps in rust ink — Instagram post (7am), The Cut article (8am), Harper's Bazaar (noon), Essence interview (3pm) — small clock icons next to each step in amber

CENTRE-RIGHT: Hand-drawn bar chart comparing 'Old Company Value $3M' (short teal bar) vs 'Personal Brand Value $30M' (tall navy bar) with rust annotation arrow pointing up

BOTTOM: 4 hand-drawn icons in a row — megaphone (PR), shield (data as armor), person at podium (protagonist), lightbulb (failure as insight) — each labelled in small rust handwriting

Colour palette: navy headlines, rust annotations and arrows, teal and amber chart bars, yellow highlight boxes, black hand-drawn outlines. No Canva gradients. No corporate feel."

---

## Self-Check Before Writing a Prompt

- Did I state the exact headline text?
- Did I describe the chart type AND data?
- Did I name every icon and its position?
- Did I specify a colour for each element?
- Does this image tell the full story without the post?
