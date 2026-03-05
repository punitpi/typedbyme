# Images Directory Structure

This document outlines the images needed for the Hugo Toha theme website.

## Required Images

### Author
- `author/puneeth.png` - Your profile photo (already exists)

### Sections

#### Skills (`sections/skills/`)
Add icon images for each skill (recommended size: 256x256px):
- `backend.png` - Backend Development icon
- `cloud.png` - Cloud Platforms icon
- `kubernetes.png` - Containers & Orchestration icon
- `database.png` - Databases icon
- `devops.png` - DevOps & CI/CD icon
- `iac.png` - Infrastructure as Code icon
- `programming.png` - Programming Languages icon
- `security.png` - Authentication & Security icon

**Tip:** You can use free icons from [Flaticon](https://www.flaticon.com/), [Icons8](https://icons8.com/), or [Font Awesome](https://fontawesome.com/)

#### Companies (`sections/companies/`)
Company logos for experience section (recommended size: 200x200px):
- `oneadvanced.png` - OneAdvanced logo
- `samsung.png` - Samsung R&D logo

**Tip:** Download official logos from company websites or use a placeholder

#### Projects (`sections/projects/`)
Project icons/logos (recommended size: 200x200px):
- `nodejs.png` - Node.js logo (for My Express Template)
- `game.png` - Game controller icon (for Scotland Yard Tracker)
- `dsa.png` - Algorithm/data structure icon
- `app.png` - Mobile app icon (for ASL App)
- `scripts.png` - Terminal/script icon (for Adhoc Scripts)
- `microservices.png` - Microservices architecture icon
- `cicd.png` - CI/CD pipeline icon
- `kubernetes.png` - Kubernetes logo
- `placeholder.png` - Generic placeholder for future projects

#### Education (`sections/education/`)
- `vtu.png` - VTU university logo (recommended size: 200x200px)

### Blog Posts (`posts/`)

Each blog post directory should contain:
- `hero.jpg` or `hero.png` - Hero/featured image (recommended size: 1200x630px)

Create hero images for:
- `microservices-go/hero.jpg` - Go gopher with microservices
- `aws-eks/hero.jpg` - AWS/Kubernetes themed
- `uk-visa/hero.jpg` - UK/travel themed
- `docker/hero.jpg` - Docker whale logo
- `homelab/hero.jpg` - Server rack or home office
- `learning/hero.jpg` - Education/learning themed

**Tip:** Use [Unsplash](https://unsplash.com/) or [Pexels](https://www.pexels.com/) for free stock photos, or create custom images with [Canva](https://www.canva.com/)

## Quick Setup Options

### Option 1: Use Placeholder Service
For quick testing, use placeholder images:
```markdown
![Placeholder](https://via.placeholder.com/800x600?text=Coming+Soon)
```

### Option 2: Download Icon Packs
1. Visit [DevIcon](https://devicon.dev/) for technology icons
2. Use [Simple Icons](https://simpleicons.org/) for brand logos
3. Try [Flaticon](https://www.flaticon.com/) for general purpose icons

### Option 3: Generate with AI
Use AI image generators like:
- DALL-E
- Midjourney
- Stable Diffusion

## Image Guidelines

### Format
- **Logos/Icons:** PNG with transparency
- **Photos/Hero images:** JPG or WebP
- **Max file size:** 500KB (optimize for web)

### Optimization Tools
- [TinyPNG](https://tinypng.com/) - Compress PNG/JPG
- [Squoosh](https://squoosh.app/) - Image optimization
- ImageMagick - Command-line tool

```bash
# Resize and optimize example
convert input.png -resize 256x256 -quality 85 output.png
```

## Current Status

### ✅ Already Exists
- `author/puneeth.png` - Profile photo
- `favicon/*` - Favicon files

### ⏳ Needs to be Added
- All skill icons
- Company logos
- Project images
- Education logo
- Blog post hero images

## Quick Start

1. Add placeholder images for immediate testing
2. Replace with proper images gradually
3. Optimize all images before committing
4. Update this README when adding new sections

---

**Note:** You can also disable images in section YAML files by commenting out the `logo:` or `hero:` lines until you have proper images ready.
