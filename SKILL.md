---
name: visual-image-director
description: Plan, preview, generate, code-render, and revise single-image raster visual designs such as posters, social posts, banners, covers, product visuals, ads, thumbnails, and edited images. Use when the user wants a disciplined workflow with design.md, prompt.md, style-used.md, thumbnail-board.png approval, final high-resolution PNG delivery, localized revisions that preserve visual continuity, or complex visuals that may use SVG, HTML, CSS, canvas, browser rendering, or other code as intermediate production assets.
---

# Visual Image Director

## Core Idea

Use this skill as a visual director for single-image design and image editing. Do not jump directly from a vague request to final generation. Convert the user's request into a reviewable design framework, a production prompt, a thumbnail preview, and only then a final image.

Default to the user's language for support documents and visible text. If the user writes in Chinese, write `design.md`, `prompt.md`, `style-used.md`, review notes, and visible image text in Chinese unless they request another language.

## Highest Priority Rules

- Always create or update `design.md` before generating any thumbnail or final image.
- Always create or update `prompt.md` before generating any thumbnail or final image.
- Always create or update `style-used.md` before final generation, unless the task is a simple one-off factual edit with no visual style choices.
- Ask the user to confirm `design.md` and `prompt.md` before generating `thumbnail-board.png`, unless the user explicitly says to skip confirmation.
- Ask the user to confirm the thumbnail direction before generating the final image, unless the user explicitly says to skip confirmation.
- After every document, thumbnail, final image, or revision, run a self-check against the user's requirements. If something is off, revise the artifact before asking for approval.
- Before final delivery, run an aesthetic calibration pass against the approved thumbnail: keep the thumbnail's composition, visual direction, and style DNA consistent while improving finish, detail, balance, and visual appeal.
- Do not over-simplify the final image into an amateur, generic, childish, or template-like result. The final image must look intentionally designed and aesthetically polished.
- For local revisions, first restate the requested change and the locked areas. Then change only the requested local region or issue.
- Preserve visual continuity across the same chat: palette, materials, lighting, typography mood, layout logic, camera language, and decorative system must stay consistent unless the user requests a new visual direction.
- Never perform a full redesign when the user asks for a local fix.

## Output Folder

For each task, create a compact working folder in the current workspace unless the user gives another destination:

```text
output/visual-image-director/<short-project-name>/
```

Expected artifacts:

- `design.md`: image design framework, composition, layout, text hierarchy, visual constraints.
- `prompt.md`: thumbnail prompt, final prompt, edit prompts, negative constraints, invariants.
- `style-used.md`: style lock for the current image or image series.
- `thumbnail-board.png`: preview of composition, rhythm, and approximate visual direction.
- `final.png`: final approved image, or a clearly named format variant.
- `revision-log.md`: record of requested local edits, locked areas, and resulting versions.
- `render/` or clearly named source files: optional code-assisted production assets such as SVG, HTML, CSS, canvas scripts, browser screenshots, masks, or compositing notes when they are used to create the final PNG.

Do not overwrite final files unless the user explicitly asks. Use versioned names such as `final-v2.png`, `poster-edited-v3.png`, or `thumbnail-board-v2.png`.

## Request Classification

Classify the request before writing files:

- New design: poster, ad, social post, cover, banner, product visual, thumbnail, key visual.
- Design from reference: use provided images for style, layout, mood, product, character, or composition.
- Image edit: modify an existing image while preserving unchanged areas.
- Local revision: change one element, text area, color, object, face expression, crop, lighting issue, or layout detail in a generated result.
- Full redesign: rebuild the whole image, style, composition, or art direction.

If an input image is provided, label each image's role:

- Edit target: the image to change.
- Style reference: visual DNA only.
- Content reference: object, person, product, logo, layout, or scene to include.
- Comparison reference: used to diagnose what should change.

## Missing Inputs

Ask one concise question when missing information would materially affect the result. Continue after the user answers.

Important missing inputs may include:

- Final use: poster, Instagram post, ad, cover, banner, marketplace image.
- Aspect ratio or size: default to the most likely format only when safe.
- Exact visible text: ask for verbatim text if text accuracy matters.
- Brand constraints: colors, logo behavior, fonts, forbidden styles.
- Required preservation: which parts of an existing image must not change.
- Target audience and mood.

Do not ask about details that can be reasonably chosen from the brief.

## `design.md` Requirements

Write `design.md` as the design blueprint. Include only sections that help the task.

Recommended structure:

```markdown
# Design

## Goal
## Output Format
## Production Method
## Audience And Mood
## Visual Concept
## Layout Framework
## Text Hierarchy
## Subject And Image Treatment
## Color, Lighting, And Materials
## Style Lock Summary
## Must Keep
## Must Avoid
## Self-Check
```

For posters and marketing images, specify the placement of:

- Main title or hook.
- Subtitle or supporting line.
- Product, person, scene, or key object.
- Call to action, price, date, or badge only if provided or required.
- Empty breathing space and safe margins.

For edits, specify:

- Exact edit target.
- Locked elements.
- What may change.
- What must remain visually identical.

When a code-assisted raster workflow is useful, specify:

- Which parts are best made with code, such as exact typography, grid systems, charts, diagrams, clean vector shapes, procedural patterns, or precise UI-like composition.
- Which parts should use image generation, editing, or compositing, such as photographic subjects, painterly detail, material realism, or texture-rich scenes.
- Final PNG size, aspect ratio, resolution scale, transparent background needs, and any export constraints.

## `prompt.md` Requirements

Write `prompt.md` as the production prompt file. Include:

- Source brief summary.
- Style Lock copied or derived from `style-used.md`.
- Thumbnail prompt.
- Final image prompt.
- Negative constraints.
- Text rendering instructions with exact text in quotes.
- Invariants for edits and revisions.
- Self-check.

Use a clear prompt scaffold:

```text
Use case:
Output:
Primary request:
Input image roles:
Production method:
Visual style:
Composition:
Subject:
Text:
Lighting:
Color palette:
Materials and texture:
Must keep:
Must avoid:
Negative constraints:
```

For text-heavy designs, keep visible text short and explicit. Warn the user if the requested image contains too much text for reliable image generation, and suggest a lower-density layout.

## `style-used.md` Requirements

Create a style lock that can survive thumbnail, final generation, and later revisions.

Include:

- Overall style name or short label.
- Typography mood and hierarchy.
- Layout grid, safe margins, and spacing rhythm.
- Palette with named colors or hex values when known.
- Lighting and material rules.
- Decorative system and border/container rules.
- Image treatment: photo, editorial, 3D, illustration, collage, grain, flat graphic, etc.
- Continuity rules for revisions.
- Negative style constraints.

If the user provides a style reference, extract the style into `style-used.md` without importing unrelated visual DNA from previous chats or unrelated files.

## Code-Assisted Raster Workflow

Use SVG, HTML, CSS, canvas, browser rendering, Three.js, charting libraries, or other code-native methods as intermediate production tools when they improve precision, complexity, typography, layout control, repeatability, or visual polish.

Choose a code-assisted path especially for:

- Complex posters, infographics, diagrams, labels, charts, UI-like graphics, grids, data-driven layouts, typographic systems, geometric motifs, or exact brand layouts.
- Visuals where crisp text, vector-like edges, controlled spacing, or deterministic alignment matter more than purely generative texture.
- Hybrid compositions where code provides the layout shell, masks, type, symbols, or overlays, and image generation provides photos, illustrations, textures, backgrounds, or subject renders.

Rules for code-assisted work:

- The final user-facing deliverable must be a high-resolution PNG unless the user explicitly asks for another raster format.
- Save useful intermediate source files in the task output folder, but do not treat SVG, HTML, CSS, screenshots, or source code as the final image.
- Render or export intermediates at the requested final dimensions, or at a higher scale such as 2x or 3x when the size is not specified.
- Inspect the exported PNG, not only the source code, before presenting it as a thumbnail, final image, or revision.
- If text accuracy is important, prefer code-rendered typography or post-composited text over relying on an image generator to spell text.
- If the user requests a local revision to a code-assisted image, update the source, re-export the PNG, and self-check that locked areas still match the approved direction.

## Thumbnail Workflow

Generate `thumbnail-board.png` only after `design.md` and `prompt.md` are confirmed or the user explicitly skips confirmation.

The thumbnail board should show one or more small composition options. Use it to preview:

- Layout balance.
- Main subject placement.
- Text blocks and hierarchy.
- Color direction.
- Overall visual rhythm.

Do not treat thumbnail text as final typography. The thumbnail is for visual direction and layout approval.

For a single image, prefer a 2-4 option thumbnail board when the brief is open-ended. Prefer one focused thumbnail when the user has already given a precise layout.

After thumbnail generation, inspect and self-check:

- Does it match the brief?
- Is the composition readable at a glance?
- Does the text placement make sense?
- Is the style consistent with `style-used.md`?
- Are there unwanted elements or style drift?

If the thumbnail does not satisfy the brief, revise the thumbnail before asking the user to approve final generation.

## Final Generation Workflow

Generate the final image only after thumbnail approval unless the user explicitly skips that gate.

Before final generation:

- Re-read `design.md`, `prompt.md`, `style-used.md`, and the approved thumbnail.
- Carry forward the approved composition and visual direction.
- Treat the approved thumbnail as the composition and style anchor, not as a low-fidelity ceiling.
- Improve the final image's craft: richer detail where appropriate, better spacing, cleaner hierarchy, stronger material/lighting polish, and more deliberate visual tension.
- Keep the final image aesthetically mature. Avoid results that feel like a basic template, a beginner layout, clip-art assembly, or an image a child could make by placing obvious elements on a flat background.
- Use the final prompt, not a casual summary.
- Preserve the selected ratio and visible text requirements.

After final generation, inspect and self-check:

- Brief match.
- Style consistency.
- Composition and hierarchy.
- Text accuracy.
- Required elements present.
- Forbidden elements absent.
- No unintended redesign from the approved thumbnail.
- Aesthetic calibration: final image is at least as visually compelling as the thumbnail direction, with stronger finish but no style drift.
- Design maturity: final image is not overly simplified, generic, childish, or visually under-designed.

If there is a correctable issue, revise the image or prompt before presenting it as final.

## Revision Workflow

For every user revision request:

1. Identify whether it is a local revision or a full redesign.
2. Restate the change and locked areas before editing.
3. Update `revision-log.md`.
4. Update `prompt.md` with a revision prompt and invariants.
5. Apply only the requested change.
6. Self-check that locked areas remain consistent.
7. Present the revised image and summarize exactly what changed.

Local revision examples:

- Replace one word.
- Move the title slightly upward.
- Make the product brighter.
- Remove a small object.
- Change background color while keeping subject and text.
- Fix one person's hand, face, shadow, or edge.

For local revisions, keep:

- Same overall style.
- Same composition unless the change requires movement.
- Same color system unless color is the edit target.
- Same subject identity and pose unless requested.
- Same typography mood.
- Same lighting direction and camera feel.

Full redesign requires explicit language such as "redesign", "change the whole style", "make a new direction", "start over", "big revamp", or equivalent.

## Tool Use

Use the available image generation/editing capability for thumbnails, final images, and visual revisions. If the platform has the `imagegen` skill or built-in image generation tool, follow that tool's requirements for actual generation and file handling.

For local image files that need visual inspection, view the image first so the edit target or reference is visible in context.

Do not replace a raster image request with unfinished code, low-resolution screenshots, or mock placeholders. Code, SVG, HTML, CSS, and browser screenshots are allowed as production intermediates only when they are rasterized, inspected, and delivered as the requested high-resolution PNG.

## Final Delivery

At delivery, provide:

- Final image path or inline preview where supported.
- The main artifacts created or updated.
- A short note on verification: what was checked and whether any risk remains.

Do not claim the final image is complete until the thumbnail/final/revision has been inspected against the user's stated requirements and the final image passes aesthetic calibration against the approved thumbnail.
