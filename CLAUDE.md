# CLAUDE.md — TypedByMe Portfolio & Blog

## Project Overview

**TypedByMe** is Puneeth Prakash's personal portfolio and technical blog at https://typedbyme.puneeth.io/

- **Framework:** Hugo (v0.148+) with the Toha v4 theme via Hugo Modules
- **Repo:** https://github.com/punitpi/typedbyme
- **Analytics:** GoatCounter (code: builder023)

---

## Writing Style Notes

- Avoid em dashes ( — ) in site content (summaries, skill descriptions, bio text). Use commas, colons, or rephrase instead. They read as AI-generated.
- Write naturally and directly, as Puneeth would.

## About Puneeth

**DevSecOps Engineer / Software Engineer** at OMICRON electronics, based in Klaus, Vorarlberg, Austria.
**8+ years** of experience. Contact: contact@puneeth.io | GitHub: @punitpi | LinkedIn: @ppuneeth

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
│   └── custom.html             # Custom favicon configuration
├── static/
│   ├── files/Resume.pdf        # Downloadable resume
│   └── favicon*                # Multiple favicon sizes
└── images/author/puneeth.png   # Profile photo
```

---

## Content Workflow

### Adding a New Blog Post

1. Create `content/posts/<slug>.md`
2. Use this front matter template:

```yaml
---
title: "Post Title"
date: YYYY-MM-DDTHH:MM:SS+05:30
author:
  name: Puneeth Prakash
  image: images/author/puneeth.png
description: "Brief description for SEO and previews"
tags: ["tag1", "tag2"]
categories: ["Category Name"]
menu:
  sidebar:
    name: "Short Name"
    identifier: post-slug
    weight: 10
---
```

3. To feature a post, add its slug to `data/en/sections/featured-posts.yaml`.

### Updating Portfolio Data

All professional info lives in `data/en/sections/` YAML files. Edit the relevant file directly:

- **Skills:** `skills.yaml` — 8 categories, each with a `name`, `logo`, and `summary`. No percentage bars.
- **Experience:** `experiences.yaml` — Company → positions → responsibilities
- **Projects:** `projects.yaml` — Name, description, technologies, timeline, links
- **Accomplishments:** `accomplishments.yaml` — Certifications and awards
- **About/Resume:** `about.yaml` — Designation, company, summary, badges, resume link

---

## Professional Profile (for content generation)

### Skills

| Category | Technologies |
|---|---|
| DevSecOps & CI/CD | GitHub Actions, Jenkins, Harness, SonarQube, IDS/IPS, vulnerability management, pipeline hardening |
| Backend Development | Node.js, Express.js, .NET, Flask, microservices, RESTful APIs, Microsoft Graph API |
| Cloud Platforms | AWS (Lambda, ECS, EKS, Fargate, API Gateway, CloudFront, S3, Route 53, SNS, SQS, IAM, CloudWatch), Azure (Functions, WebJobs, App Services, Blob Storage, KeyVault). Terraform + CloudFormation for IaC. |
| Containers & Orchestration | Docker, Kubernetes (EKS), Inlets Pro, automated TLS |
| Databases | MSSQL, DynamoDB, MongoDB, MySQL, Redis |
| Programming Languages | JavaScript (Node.js), C#, Python, SQL, Bash, YAML, React |

### Work History

**OMICRON electronics** — DevSecOps Engineer / Software Engineer (Dec 2025 – Present)
- Klaus, Vorarlberg, Austria
- DevSecOps practices, security automation, CI/CD pipeline hardening
- Cloud-native architecture and infrastructure as code in the energy technology sector

**OneAdvanced** — Senior Software Engineer (Feb 2021 – Oct 2025)
- Cloud-native solutions on AWS (Lambda, ECS, DynamoDB) and Azure (Functions, WebJobs)
- Built BYOBI platform with dbt + Snowflake
- Kubernetes on EKS with Inlets Pro, cert-manager, GitOps
- CI/CD with GitHub Actions, Harness, Terraform/CloudFormation (70% deployment time reduction)
- OAuth2/SSO/2FA with Keycloak; pentest and SonarQube vulnerability fixes
- $1,000+/month AWS cost optimization
- Technical training on AWS services and architecture

**OneAdvanced** — Software Engineer (Mar 2018 – Feb 2021)
- .NET WinForms automation tool: 92% deployment time reduction (60 min → 5 min)
- AWS Lambda, API Gateway, S3 serverless apps
- Jenkins CI/CD; MSSQL stored procedure optimization (50% improvement)

**Samsung R&D Institute India** — Test Engineer (Mar 2017 – Nov 2017)
- 600+ test cases for Project Bixby (functional, integration, performance, regression)

### Certifications & Accomplishments

- **AWS Certified Solutions Architect – Associate** (2023)
- **Spot Award** – Critical project completion ahead of schedule (OneAdvanced, 2023)
- **Cost Optimization** – $1,000+/month AWS savings (OneAdvanced, 2022)

---

## Blog Posts

| Post | Date | Category | Topic |
|---|---|---|---|
| Docker Best Practices for Production | Oct 2025 | Documentation & Guides | 10 production Docker best practices with Dockerfile examples |
| The Power of Learning in Public | Sep 2025 | Career & Learning | Why and how to share your learning journey publicly |
| Building Your Portfolio & Blog with Hugo | Dec 2025 | Documentation & Guides | Comprehensive Hugo setup guide from zero to deployed |
| Building My Homelab: A Journey into Self-Hosting | Sep 2025 | Life & Processes | Intel NUC homelab with Proxmox, pfSense, Home Assistant, Immich |

**Recurring themes:** hands-on learning, self-hosting, cloud/DevOps, practical documentation, security awareness.

---

## Blog Writing Guidelines

### Voice & Identity

Write as Puneeth Prakash — a software engineer sharing knowledge in a conversational, approachable way while maintaining technical authority. Mental model: a software engineer chatting with a friend over coffee, not an English professor writing a thesis.

- Always use first-person ("I", "I've learned") and second-person for the reader ("you", "your")
- Use contractions naturally ("you're", "I'll", "don't")
- Simple words over fancy ones ("use" not "utilize", "help" not "facilitate")
- Encouraging tone, never condescending

**Humor:** 4-5 out of 10. Never forced. Approved styles:
- Self-deprecating: "Past me learned this lesson at least five times before it stuck"
- Tech culture: "It's always DNS. Every. Single. Time."
- Relatable frustration: "Coffee count: 3. Working code count: 0."
- Witty asides: "Spoiler alert: It's complicated."

### Post Structure

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

- **Personal story:** "It all started innocently enough. I was scrolling through..."
- **Problem statement:** "[Task] can be [challenging]. In this guide, I'll walk you through [solution]..."
- **Reflective:** "After years of [X], I finally [Y]. And you know what? It was easier than I expected..."

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
- Always add a sentence of context before and after every block

### Closing Pattern

```markdown
## Conclusion

[1-2 wrap-up sentences]

- **Benefit 1**: explanation
- **Benefit 2**: explanation

### Your Next Steps

1. **Action 1**: details
2. **Action 2**: details

---
## Resources
- [Resource](URL)

---
Questions? Reach out at contact@puneeth.io
```

**Closing line options:** "Just start." / "Your future self will thank you." / "Now stop reading and start building."

### Quality Checklist

- [ ] Hook engages in first 2–3 sentences
- [ ] All code blocks have language identifiers and inline comments
- [ ] Voice is conversational throughout (first + second person)
- [ ] Technical terms introduced with context
- [ ] Conclusion has actionable next steps
- [ ] Post ends with contact CTA
- [ ] Frontmatter is complete

### The One Rule

If something sounds too fancy or complicated, simplify it. Write like you talk.

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
- **`layouts/partials/head/custom.html`** — Apple touch icon and multiple favicon PNG sizes.
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
