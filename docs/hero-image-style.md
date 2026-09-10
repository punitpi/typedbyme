# Blog Hero Image Style

Locked visual style for post hero images at `assets/images/posts/<slug>/hero.jpg` (or `.jpeg`).
Derived from the existing set (`learning-in-public`, `homelab-setup-guide`, `docker-best-practices`,
`ai-changed-how-i-build-part-*`, `austrian-driving-licence-exchange-non-eea`, `id-austria`).

Exception: `id-austria`'s *original* hero was the official ID Austria logo lockup, not this
illustrated style — it has since been replaced to match. Don't use an official brand/logo asset
as a hero image; always use the illustrated style below.

## Fixed elements (always include)

- **Medium:** flat vector illustration, not photorealistic.
- **Composition:** warm, cozy home-office desk scene, lit by soft window light from the left.
- **Subject:** one simplified, faceless person at a wooden desk, doing something relevant to the
  post's topic (typing on a laptop, holding a phone, reading a document).
- **Floating icons:** 3-4 topic-relevant icons in rounded speech-bubble or card shapes, floating
  above/around the subject, connected to the scene rather than randomly scattered.
- **Recurring props:** a steaming mug, a small potted plant, and one more topic-relevant prop
  (notebook, documents, passport booklet, etc.) on the desk.
- **Palette:** muted teal, cream, and dark navy. Keep it desaturated and soft, not neon or high
  contrast.
- **Shapes:** soft rounded corners, gentle drop shadows, no hard edges.
- **Signature mark:** a tiny white sparkle/star mark in the bottom-right corner.
- **Aspect ratio:** wide 16:9.
- **No readable text, no real logos, no real flags** — use color motifs (e.g. red-white-red
  stripes for Austria) instead of official emblems, since these render publicly.

## Prompt template

Fill in the bracketed parts per post; keep everything else as-is.

```
Flat vector illustration, warm cozy home-office desk scene lit by soft window light from the
left, in the style of a modern tech blog hero image. A simplified, faceless person [ACTION,
e.g. "in a teal sweater types on a laptop showing lines of colorful code"]. Above the desk,
3-4 floating icons in rounded speech-bubble or card shapes: [ICON 1], [ICON 2], [ICON 3],
[optional ICON 4]. On the desk: a steaming mug, a small potted plant, [ADDITIONAL PROP]. Muted
teal, cream, and dark navy color palette, soft rounded shapes, gentle drop shadows. Tiny white
sparkle/star mark in the bottom right corner. Wide 16:9 aspect ratio, clean and uncluttered, no
readable text, no real logos or flags, generic and decorative only.
```

## Filing convention

- Folder: `assets/images/posts/<post-slug>/` (slug matches the post's filename, not necessarily
  its `menu.sidebar.identifier`).
- File: `hero.jpg` or `hero.jpeg` (match whatever was actually generated; don't re-encode).
- Frontmatter: `hero: images/posts/<post-slug>/hero.jpeg` (uncomment if scaffolded commented-out).
- After adding an image via Finder, delete any `.DS_Store` that lands in the folder before
  staging: `find assets/images -name '.DS_Store' -delete`.
