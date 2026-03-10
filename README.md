# typedbyme

Personal portfolio and blog — [typedbyme.puneeth.io](https://typedbyme.puneeth.io/)

[![Hugo](https://img.shields.io/badge/Hugo-0.148+-blue.svg)](https://gohugo.io)
[![Theme](https://img.shields.io/badge/Theme-Toha_v4-green.svg)](https://github.com/hugo-toha/toha)

---

## What this is

This is the source for my personal portfolio and blog. Built with Hugo and the Toha v4 theme. It includes my work experience, skills, projects, accomplishments, and technical blog posts.

Live at: [typedbyme.puneeth.io](https://typedbyme.puneeth.io/)

---

## Prerequisites

- [Hugo Extended](https://gohugo.io/installation/) v0.148+
- [Node.js](https://nodejs.org/) (for theme dependencies)
- [Go](https://golang.org/) (for Hugo modules)

---

## Running locally

```bash
# Clone the repo
git clone https://github.com/punitpi/typedbyme.git
cd typedbyme

# Install dependencies
npm install
hugo mod get -u

# Start the dev server
hugo server
```

Open [http://localhost:1313](http://localhost:1313) in your browser. The site hot-reloads on any file change.

## Production build

```bash
hugo --minify
```

Output goes to `public/`. That directory is what gets deployed.

---

## Project structure

```
typedbyme/
├── hugo.yml                        # Main config — baseURL, theme, analytics, features
├── content/
│   └── posts/                      # Blog posts in markdown
├── data/en/
│   ├── author.yaml                 # Name, greeting, contact, hero summary bullets
│   └── sections/
│       ├── about.yaml              # Designation, company, summary, badges, social links
│       ├── skills.yaml             # Skill cards with descriptions
│       ├── experiences.yaml        # Work history
│       ├── education.yaml          # Education
│       ├── projects.yaml           # Projects (personal + professional)
│       ├── accomplishments.yaml    # Certifications and awards
│       ├── featured-posts.yaml     # Which posts appear in the featured section
│       └── recent-posts.yaml       # Recent posts config
├── assets/
│   └── styles/override.scss        # Custom CSS (minimal — removes hero background blur)
├── layouts/partials/head/
│   └── custom.html                 # Favicon configuration
├── static/
│   ├── files/Resume.pdf            # Downloadable resume
│   └── favicon*                    # Favicon variants
└── images/author/puneeth.png       # Profile photo
```

---

## How to update content

All portfolio data is in YAML files under `data/en/sections/`. Edit the relevant file directly.

| What to update | File |
|---|---|
| Name, contact, hero summary | `data/en/author.yaml` |
| Designation, company, about summary | `data/en/sections/about.yaml` |
| Skills | `data/en/sections/skills.yaml` |
| Work experience | `data/en/sections/experiences.yaml` |
| Projects | `data/en/sections/projects.yaml` |
| Certifications / awards | `data/en/sections/accomplishments.yaml` |
| Featured blog posts | `data/en/sections/featured-posts.yaml` |
| Resume PDF | `static/files/Resume.pdf` |
| Site config | `hugo.yml` |

### Adding a blog post

Create a new markdown file under `content/posts/`:

```yaml
---
title: 'Post Title'
date: YYYY-MM-DDTHH:MM:SS+01:00
draft: false
author: 'Puneeth Prakash'
description: 'Short description for SEO'
tags: ['Tag1', 'Tag2']
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

To feature a post on the home page, add its slug to `data/en/sections/featured-posts.yaml`.

---

## Deployment

The site can be deployed anywhere that serves static files:

- **Netlify** — connect the GitHub repo, set build command to `hugo --minify`, publish dir to `public`
- **Vercel** — import from GitHub, same build settings
- **GitHub Pages** — use a GitHub Actions workflow to build and push `public/` to `gh-pages`
- **AWS S3 + CloudFront** — upload the `public/` directory after building

---

## Customisation

- **Sections**: Enable or disable portfolio sections in `hugo.yml` under `features`
- **Analytics**: GoatCounter is configured in `hugo.yml` — swap the code for your own
- **Dark mode**: Enabled by default using DarkReader, defaults to system preference
- **CSS**: Add overrides in `assets/styles/override.scss`
- **Theme docs**: [toha-guides.netlify.app](https://toha-guides.netlify.app/)

---

## Credits

Background image generated using [City Roads](https://github.com/anvaka/city-roads) by [@anvaka](https://github.com/anvaka) — a beautiful visualization tool that renders any city's road network as art.

---

## License

Code and structure: [Creative Commons Attribution-NonCommercial 4.0](LICENSE) — free to use with attribution.

Personal content (profile photo, resume, blog posts, personal data): not available for reuse without permission.

---

## Contact

[contact@puneeth.io](mailto:contact@puneeth.io) | [typedbyme.puneeth.io](https://typedbyme.puneeth.io/)
