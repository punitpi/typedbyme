# CLAUDE.md — TypedByMe Portfolio & Blog

## Project Overview

**TypedByMe** is Puneeth Prakash's personal portfolio and technical blog at https://typedbyme.puneeth.io/

- **Framework:** Hugo (v0.148+) with the Toha v4 theme via Hugo Modules
- **Repo:** https://github.com/punitpi/typedbyme
- **Analytics:** GoatCounter (code: builder023)
- **Spotify Now Playing:** API proxy at `spotify.api.puneeth.io`

---

## Writing Style Notes

How Puneeth writes, and how to edit that writing, lives in `~/.claude/me/voice.md`. Read it before writing or editing any post or site text. This file only covers blog mechanics.

## About Puneeth

**DevSecOps Engineer / Software Engineer** at OMICRON electronics, based in Klaus, Vorarlberg, Austria.
**9+ years** of experience. Contact: contact@puneeth.io | GitHub: @punitpi | LinkedIn: @ppuneeth

**Background:** DevSecOps, cloud-native microservices, AWS & Azure, CI/CD security automation, system reliability.
**Interests:** Homebrewing, backpacking, self-hosting/homelab, cybersecurity.

---

## Tech Stack

- **Hugo** static site generator
- **Toha v4** theme (imported via Hugo Modules)
- **Node.js/npm** for frontend tooling (Bootstrap, PostCSS, Highlight.js, KaTeX, Fuse.js)
- **GoatCounter** for privacy-friendly analytics
- **DarkReader** for dark mode toggle
- Build: `hugo --minify` (production), `hugo server` (development)

---

## Site Structure

```
typedbyme/
├── hugo.yml                    # Main Hugo config (baseURL, theme, features, analytics)
├── content/
│   └── posts/                  # All blog posts (markdown)
│       ├── docker-best-practices.md
│       ├── learning-in-public.md
│       ├── building-your-portfolio-with-hugo.md
│       └── homelab-setup-guide.md
├── data/en/sections/           # YAML data files for all portfolio sections
│   ├── author.yaml             # Name, greeting, image, contact, summary bullets
│   ├── about.yaml              # Designation, company, resume link, badges, social links
│   ├── skills.yaml             # 8 skill categories with summaries (no percentage bars)
│   ├── experiences.yaml        # Work history (OneAdvanced, Samsung)
│   ├── education.yaml          # B.E. CSE, VTU 2013-2017
│   ├── projects.yaml           # 7 projects (personal + professional)
│   ├── accomplishments.yaml    # AWS cert, Spot Award, Cost Optimization
│   ├── featured-posts.yaml     # 3 featured posts config
│   └── recent-posts.yaml       # 4 recent posts, sorted by date desc
├── assets/styles/override.scss # Minimal SCSS: removes background filter on hero
├── layouts/partials/head/
│   └── custom.html             # Favicon config + Spotify Now Playing bar (style + script)
├── static/
│   ├── files/Resume.pdf        # Downloadable resume
│   └── favicon*                # Multiple favicon sizes
└── images/author/puneeth.png   # Profile photo
```

---

## Content Workflow

### Adding a New Blog Post

1. Create `content/posts/<slug>.md`
2. Use the frontmatter template under Blog Writing Guidelines below.
3. To feature a post, add its slug to `data/en/sections/featured-posts.yaml`.

### Updating Portfolio Data

All professional info lives in `data/en/sections/` YAML files. Edit the relevant file directly:

- **Skills:** `skills.yaml` — 8 categories, each with a `name`, `logo`, and `summary`. No percentage bars.
- **Experience:** `experiences.yaml` — Company → positions → responsibilities
- **Projects:** `projects.yaml` — Name, description, technologies, timeline, links
- **Accomplishments:** `accomplishments.yaml` — Certifications and awards
- **About/Resume:** `about.yaml` — Designation, company, summary, badges, resume link

---

## Facts for posts

Use only the "Proof I can use" list in `~/.claude/me/voice.md` for numbers, roles and certifications in posts. The site's own career data is in `data/en/sections/*.yaml`.

---

## Blog Posts

| Post | Date | Category | Topic |
|---|---|---|---|
| Docker Best Practices for Production | Oct 2025 | Documentation & Guides | 10 production Docker best practices with Dockerfile examples |
| The Power of Learning in Public | Sep 2025 | Career & Learning | Why and how to share your learning journey publicly |
| Building Your Portfolio & Blog with Hugo | Dec 2025 | Documentation & Guides | Comprehensive Hugo setup guide from zero to deployed |
| Building My Homelab: A Journey into Self-Hosting | Sep 2025 | Life & Processes | Intel NUC homelab with Proxmox, pfSense, Home Assistant, Immich |


---

## Blog Writing Guidelines

### Voice

Voice, editing rules, positions, off-limits topics and usable numbers are all in `~/.claude/me/voice.md`. Posts start from Puneeth's own story or notes (dictated or typed); if there's only a topic, ask for the story first. Run `/humanize-me` on the draft.

### Post Structure

A starting point for how-tos and guides, not a template every post must fill. Personal and reflective posts follow the story instead, and can skip sections like Prerequisites or a formal Conclusion. Use sentence-case headings that name what the section holds.

```
## Introduction / Hook
[Personal context OR problem statement]
[Why this matters]
[What the reader will learn]

## Prerequisites / Context

## Main Content Sections

## Practical Examples / Application

## Tips / Best Practices / Troubleshooting

## Conclusion
[Summary, next steps, encouragement]

## Resources

---
Questions? Reach out at contact@puneeth.io
```

### Frontmatter Template

```yaml
---
title: 'Post Title'
date: YYYY-MM-DDTHH:MM:SS+01:00
draft: false
author: 'Puneeth Prakash'
description: 'One-sentence SEO summary (150-160 chars)'
tags: ['Tag1', 'Tag2', 'Tag3']
categories: ['Category Name']
toc:
  enable: true
menu:
  sidebar:
    name: 'Short Name'
    identifier: 'unique-slug'
    weight: 500
---
```

**Valid categories:** Cloud & Infrastructure, Documentation & Guides, Life & Processes, Career & Learning, Web Development

### Content Types & Word Counts

| Type | Length | Notes |
|---|---|---|
| Comprehensive tutorials | 2,000–6,000 words | Beginner + advanced tracks, troubleshooting section |
| Technical implementation guides | 1,500–2,500 words | One focused implementation, security best practices |
| Best practices / reference | 600–1,000 words | Scannable, heavy lists and code, Good vs Bad examples |
| Personal / reflective | 1,500–1,800 words | Story-driven opening, narrative + actionable advice |

### Opening Hook Patterns

Open on what actually happened or the specific problem, in Puneeth's own words. Don't announce what the post will cover.

### Formatting Rules

1. Paragraphs: 2–6 sentences max. One-sentence paragraphs allowed for emphasis.
2. Mix short punchy sentences with longer explanatory ones.
3. Header hierarchy: H2 → H3 → H4. Never skip levels.
4. Unordered lists for features/tips. Ordered lists for sequential steps.
5. Always use descriptive anchor text, never raw URLs inline.
6. Define acronyms and technical terms on first use.

### Code Blocks

- Always include the language identifier
- Add comments explaining what the code does
- Provide complete, runnable examples where possible
- Add a sentence of context before a block when the reader needs it. Skip a trailing sentence that only restates the block.

### Closing Pattern

End the post on its last real point. A how-to can close with next steps in plain sentences or a short numbered list. A personal post can simply stop. Always keep the Resources list (when there are links) and the contact line:

```markdown
## Resources
- [Resource](URL)

---
Questions? Reach out at contact@puneeth.io
```

Don't recap the post at the end.

### Quality Checklist

- [ ] All code blocks have language identifiers and inline comments
- [ ] Technical terms introduced with context
- [ ] `/humanize-me` was run
- [ ] Post ends with contact CTA
- [ ] Frontmatter is complete

---

## Hugo Configuration Highlights (`hugo.yml`)

```yaml
baseURL: https://typedbyme.puneeth.io/
timeZone: Europe/Vienna
theme: toha

features:
  portfolio: enabled
  blog: enabled
  toc:
    enable: true
  analytics:
    enable: true
    services:
      goatCounter:
        code: builder023
  darkMode:
    enable: true
    provider: darkreader
    default: system

  # Disabled sections
  notes: disabled
  support: disabled
  newsletter: disabled
```

---

## Customizations

- **`assets/styles/override.scss`** — Removes background-filter blur on the home page hero section.
- **`layouts/partials/head/custom.html`** — Apple touch icon, multiple favicon PNG sizes, and the Spotify Now Playing bar (inline CSS + JS).
- **`layouts/partials/cards/project.html`** — local override of the Toha theme's project card. The stock theme partial only renders one footer button (a GitHub star button if `repo` is set, which also wins the outer card click-through over `url`; otherwise a "Details" link if only `url` is set). This override adds a second button driven by a `liveUrl` field, so a project can show both a repo link and a live-site link.
- **`layouts/partials/opengraph.html`** — local override of the Toha theme's OG meta tags. Before this override existed, both this file's `head/custom.html` (correct, absolute URL, per-post `hero`) and the theme's own `opengraph.html` (broken: relative URL via `relURL`, always the site-wide author photo) emitted a duplicate `og:image` tag. Different social crawlers picked different duplicate tags inconsistently, so link previews showed the wrong image depending on platform (WhatsApp vs. Facebook, etc.). Fixed by making this override the single source of truth: prefers `.Params.hero`, falls back to site config then the author photo, always `absURL`. If you add another local override of a theme partial that already emits a meta tag elsewhere, grep the rendered `public/**/index.html` for duplicate `<meta property="og:` tags before assuming it works.
- Skills section has **no percentage bars** (removed in `7af85b0`); each skill has a text summary instead.
- Comments section was **added then removed** (`0dcc4dd` → `c1d123d`) — currently disabled.

---

## Common Tasks

| Task | File(s) to edit |
|---|---|
| Add a blog post | `content/posts/<slug>.md` |
| Update resume/about | `data/en/sections/about.yaml` |
| Add/edit a skill | `data/en/sections/skills.yaml` |
| Add work experience | `data/en/sections/experiences.yaml` |
| Add a project | `data/en/sections/projects.yaml` |
| Add an accomplishment | `data/en/sections/accomplishments.yaml` |
| Feature a post | `data/en/sections/featured-posts.yaml` |
| Update resume PDF | `static/files/Resume.pdf` |
| Change site config | `hugo.yml` |
| Custom CSS tweaks | `assets/styles/override.scss` |
| Set Spotify Worker URL | `hugo.yml` → `params.spotifyWorkerUrl` |

---

## Spotify Now Playing

A slim bar at the very top of each page shows what's currently playing on Spotify, with the Spotify icon, track name, and artist. Clicking it opens the track on Spotify.

### Architecture

```
Browser → Hugo site (JS polls every 30s) → spotify.api.puneeth.io → Spotify API
```

- The bar is injected into `<body>` via JavaScript at runtime (no Hugo template changes needed).
- The API proxy (hosted separately) handles OAuth token refresh and caches responses for 30 seconds.
- The bar is hidden when nothing is playing or if the API is unreachable.

### Configuration

The API URL is set in `hugo.yml`:

```yaml
params:
  spotifyWorkerUrl: "https://spotify.api.puneeth.io"
```

Set to `""` (empty string) to disable the bar entirely.

---

## Build & Dev

```bash
# Local development server
hugo server

# Production build
hugo --minify

# Output goes to: public/
```

Dependencies require Node.js. Run `npm install` if node_modules is missing.

- `.DS_Store` files land in new `assets/images/posts/<slug>/` folders when dragging images in via Finder — remove before staging: `find assets/images -name '.DS_Store' -delete`.
- Toha theme source (for inspecting template partials, e.g. to check what fields a card/layout supports): `~/Library/Caches/hugo_cache/modules/filecache/modules/pkg/mod/github.com/hugo-toha/toha/v4@<version>/`.
- If a PR is merged while its branch still has unpushed commits, pushing them afterward does **not** reopen the PR or add them to `main` — they're silently orphaned on the branch. Cherry-pick them onto a fresh branch off `main` and open a new PR. This has happened repeatedly (including across sessions, weeks apart) — after merging a PR, check `git log main..<branch>` before treating that branch's work as done, and periodically audit all branches the same way (`git merge-base --is-ancestor <branch> main` for each, then diff any non-ancestor branch's unique commits against what's actually on `main` before assuming they're missing — the commit may have landed via a different cherry-picked PR).
