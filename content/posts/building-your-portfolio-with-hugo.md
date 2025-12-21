---
title: 'Building Your Portfolio & Blog with Hugo: From Zero to Deployed'
date: 2025-12-21T09:00:00+01:00
draft: false
author: 'Puneeth Prakash'
description: "A comprehensive guide to setting up a beautiful portfolio and blog using Hugo—whether you're coding-curious or command-line-comfortable."

tags:
  [
    'Hugo',
    'Web Development',
    'Portfolio',
    'Blogging',
    'Static Sites',
    'Tutorial'
  ]
categories: ['Web Development']

# hero: images/posts/hugo-setup/hero.jpg

toc:
  enable: true

menu:
  sidebar:
    name: 'Hugo Portfolio Guide'
    identifier: 'hugo-portfolio-guide'
    weight: 500
---

## Introduction: Why I Built This (And Why You Might Want To)

After years of saying "I should really have a blog," I finally built one. Not on Medium. Not on Dev.to. A real, honest-to-goodness website that I control. And you know what? It was easier than I expected, once I stopped overthinking it.

This guide will show you how to build a portfolio and blog using Hugo, a static site generator that's fast, flexible, and surprisingly beginner friendly. Whether you're a developer looking for a weekend project or someone who's never touched the command line, I've got you covered.

**Fair warning:** This gets detailed. Like, "here's the exact command" detailed. Grab a coffee.

---

## Table of Contents Quick Summary

- **Non-Technical Track**: Click-and-point focused, minimal terminal work
- **Technical Track**: Full control, command-line workflows, customization
- **Theme Selection**: How to choose and implement themes
- **Content Creation**: Adding posts, projects, and pages
- **Deployment**: Comparing GitHub Pages, Netlify, Vercel, and more
- **Costs & Trade-offs**: What's free, what's cheap, what's worth it

---

## Part 1: Understanding Hugo (The 5-Minute Version)

### What is Hugo?

Hugo is a **static site generator**. Instead of querying a database every time someone visits your site (like WordPress does), Hugo pre-builds all your pages as HTML files. The result? Lightning-fast websites that cost almost nothing to host.

Think of it like this:

- **WordPress**: A restaurant that cooks your meal fresh every time you order
- **Hugo**: A meal prep service that cooks everything in advance and just heats it up when you're ready

### Why Hugo Over WordPress/Wix/Squarespace?

| Feature            | Hugo                    | WordPress        | Wix/Squarespace |     |
| ------------------ | ----------------------- | ---------------- | --------------- | --- | --- |
| **Speed**          | Blazing fast            | Moderate         | Moderate        |     |
| **Cost**           | Free (hosting ~$0-5/mo) | $4-45/mo         | $16-49/mo       |     |     |
| **Control**        | Complete                | High             | Limited         |     |
| **Security**       | Minimal risk            | Requires updates | Managed         |     |
| **Learning Curve** | Moderate                | Low              | Very low        |     |

Hugo is perfect if you want:

- Full control over your site
- Near-zero hosting costs
- A developer-friendly workflow
- Lightning-fast page loads

---

## Part 2: For the Non-Technical (I Promise, You Can Do This)

### What You'll Need

1. **A computer** (Mac, Windows, Linux all work)
2. **1-2 hours** of focused time
3. **Willingness to copy-paste commands** (I'll provide them all)
4. **Optional**: A GitHub account (free)

### The Big Picture: Our 6-Step Plan

1. Install Hugo on your computer
2. Pick a theme (like choosing a WordPress theme, but better)
3. Create your site structure
4. Add your content (posts, about page, projects)
5. Test it locally (see it on your computer first)
6. Deploy it (make it live on the internet)

### Step 1: Installing Hugo

#### On Mac:

1. Open **Terminal** (press `Cmd + Space`, type "terminal", press Enter)
2. Install Homebrew (a package manager—think of it as an app store for developers):

   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

3. Install Hugo:

   ```bash
   brew install hugo
   ```

4. Verify it worked:

   ```bash
   hugo version
   ```

   You should see something like `hugo v0.xxx.x`

#### On Windows:

**Option 1: Using Winget (Recommended if you are on Windows 11)**

Winget is Microsoft's official free and open-source package manager for Windows. To install the extended edition of Hugo:

1. Open PowerShell or Command Prompt
2. Install Hugo:
   ```powershell
   winget install Hugo.Hugo.Extended
   ```
3. Verify:
   ```powershell
   hugo version
   ```

**Option 2: Using Chocolatey**

1. Install **Chocolatey** (if you don't have it):
   - Open PowerShell as Administrator
   - Run:
     ```powershell
     Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
     ```
2. Install Hugo:
   ```powershell
   choco install hugo-extended -y
   ```
3. Verify:
   ```powershell
   hugo version
   ```

#### On Linux (Ubuntu/Debian):

```bash
sudo apt-get update
sudo apt-get install hugo
```

### Step 2: Choosing Your Theme

This is the fun part. Hugo has hundreds of free themes. Here's how to choose:

**Visit:** https://themes.gohugo.io/

**What to look for:**

- Portfolio themes (if you want to showcase projects)
- Blog themes (if you're mainly writing)
- Combined themes (like Hugo Profile, which I use and has both)

**Popular recommendations:**

| Theme            | Best For                      | Difficulty |
| ---------------- | ----------------------------- | ---------- |
| **Hugo Profile** | Developers, portfolios + blog | Easy       |
| **PaperMod**     | Minimalist blogs              | Very Easy  |
| **Terminal**     | Developer blogs, retro look   | Easy       |
| **Hugo-coder**   | Personal sites, clean design  | Easy       |
| **Ananke**       | General-purpose               | Very Easy  |

**For this guide, I'll show both:**

- Generic setup (works with any theme)
- Specific Hugo Profile setup (my theme)

### Step 3: Creating Your Site

Open Terminal/Command Prompt and navigate to where you want your site folder:

```bash
# Navigate to your Documents folder (or anywhere you like)
cd ~/Documents

# Create a new Hugo site
hugo new site my-portfolio

# Enter the folder
cd my-portfolio
```

You now have a folder structure that looks like:

```
my-portfolio/
├── archetypes/
├── content/
├── data/
├── layouts/
├── static/
├── themes/
└── hugo.toml (or hugo.yml)
```

### Step 4: Installing a Theme

#### Option A: Using Hugo Modules (Modern, Recommended)

**Prerequisites:** Install Go (Hugo modules need it)

On Mac:

```bash
brew install go
```

On Windows (with winget or chocolatey):

```powershell
winget install -e --id GoLang.Go
```

Or

```powershell
choco install golang
```

**Initialize your site as a Hugo module:**

```bash
hugo mod init github.com/yourusername/my-portfolio
```

**Add a theme (using Hugo Profile as example):**

Edit `hugo.toml` (or create `hugo.yaml`) and add:

```yaml
baseURL: 'https://yourwebsite.com/'
languageCode: 'en-us'
title: 'Your Name - Portfolio'
theme: hugo-profile

module:
  imports:
    - path: github.com/gurusabarish/hugo-profile
```

Then run:

```bash
hugo mod get -u
```

#### Option B: Using Git Submodules (Traditional)

```bash
# Initialize git in your project
git init

# Add theme as submodule (example with Hugo Profile)
git submodule add https://github.com/gurusabarish/hugo-profile.git themes/hugo-profile

# Update hugo.yaml
echo "theme: hugo-profile" >> hugo.yaml
```

### Step 5: Configuring Your Site

Open `hugo.yaml` in any text editor (VS Code, Notepad, TextEdit).

**Basic configuration for Hugo Profile:**

```yaml
baseURL: 'https://yourname.com/'
languageCode: 'en-us'
title: 'Your Name - Portfolio & Blog'
theme: hugo-profile

# Enable emoji support
enableEmoji: true

# Output formats
outputs:
  home:
    - HTML
    - RSS
    - JSON

# Markdown settings
markup:
  goldmark:
    renderer:
      unsafe: true

# Site parameters
params:
  title: 'Your Name'
  description: 'Your site description'
  favicon: '/images/fav.png'

  # Theme settings
  useBootstrapCDN: false
  animate: true

  theme:
    disableThemeToggle: false
    defaultTheme: 'light' # or 'dark'

  # Navbar
  navbar:
    align: ms-auto
    brandName: 'Your Name'
    disableSearch: false
    menus:
      disableAbout: false
      disableExperience: false
      disableEducation: false
      disableProjects: false
      disableAchievements: false
      disableContact: false

  # Hero section
  hero:
    enable: true
    title: 'Hi, I am Your Name'
    subtitle: 'I build things for the web'
    content: 'A passionate developer. I tend to make use of modern technologies to build websites and applications.'
    image: /images/hero.png
    socialLinks:
      fontAwesomeIcons:
        - icon: fab fa-github
          url: https://github.com/yourusername
        - icon: fab fa-linkedin
          url: https://linkedin.com/in/yourprofile
        - icon: fab fa-twitter
          url: https://twitter.com/yourhandle

  # Footer
  footer:
    socialNetworks:
      github: https://github.com/yourusername
      linkedin: https://linkedin.com/in/yourprofile
      twitter: https://twitter.com/yourhandle
```

### Step 6: Adding Content

#### Create an About Page:

```bash
hugo new about.md
```

Open `content/about.md` and edit:

```markdown
---
title: 'About Me'
date: 2025-12-21
draft: false
---

## Hi, I'm Your Name

I'm a [your profession] who loves [your interests].

### What I Do

- Thing 1
- Thing 2
- Thing 3

### My Journey

Write your story here...

### Get in Touch

- Email: your@email.com
- LinkedIn: [Your Profile](https://linkedin.com/in/yourprofile)
```

#### Create Your First Blog Post:

```bash
hugo new posts/my-first-post.md
```

Edit `content/posts/my-first-post.md`:

```markdown
---
title: 'My First Post'
date: 2025-12-21
draft: false
tags: ['introduction', 'blogging']
---

## Welcome to My Blog

This is my first post. Here's why I'm starting this blog...

### What I'll Write About

- Topic 1
- Topic 2
- Topic 3

Stay tuned!
```

### Step 7: Preview Your Site Locally

```bash
hugo server -D
```

Open your browser and go to: `http://localhost:1313`

**What the `-D` flag means:** Shows draft posts too

**To stop the server:** Press `Ctrl + C` in Terminal

### Step 8: Ready to Deploy?

Skip to the **Deployment Options** section below!

---

## Part 3: For the Technical (Let's Get Granular)

### Prerequisites & Setup

**System requirements:**

- Hugo Extended (for SCSS/SASS support): `v0.112.0+`
- Git: `v2.30+`
- Go (for Hugo Modules): `v1.20+`
- Node.js (for some themes): `v18+`

**Verify your environment:**

```bash
hugo version   # Should show "extended"
git --version
go version
node --version
```

### Project Initialization with Best Practices

```bash
# Create project directory
mkdir -p ~/projects/portfolio && cd ~/projects/portfolio

# Initialize Hugo site
hugo new site . --force

# Initialize git
git init
echo "public/" >> .gitignore
echo "resources/" >> .gitignore
echo ".hugo_build.lock" >> .gitignore
echo "node_modules/" >> .gitignore

# Initialize as Go module (for Hugo modules)
hugo mod init github.com/yourusername/portfolio

# Initialize npm (if theme requires it)
npm init -y
```

### Hugo Modules vs Git Submodules vs Manual Installation

**Comparison:**

| Method             | Pros                                       | Cons           | Best For            |
| ------------------ | ------------------------------------------ | -------------- | ------------------- |
| **Hugo Modules**   | Auto-updates, clean, no git submodule pain | Requires Go    | Production sites    |
| **Git Submodules** | Version control, traditional               | Clunky updates | Team projects       |
| **Manual**         | Full control                               | Manual updates | Heavy customization |

#### Hugo Modules Setup (Recommended):

```yaml
# hugo.yaml
module:
  imports:
    - path: github.com/gurusabarish/hugo-profile
```

```bash
# Install/update theme
hugo mod get -u

# Tidy dependencies
hugo mod tidy
```

#### Git Submodules Setup:

```bash
git submodule add --depth=1 https://github.com/gurusabarish/hugo-profile.git themes/hugo-profile
git submodule update --init --recursive

# Update submodule later
git submodule update --remote --merge
```

### Advanced Hugo Configuration

**`hugo.yml` with full config:**

```yaml
baseURL: 'https://yourdomain.com/'
languageCode: 'en-us'
title: 'Your Portfolio'
theme: 'your-theme' # Only if using git submodule

# Build settings
buildDrafts: false
buildFuture: false
buildExpired: false

# Output formats
outputs:
  home:
    - HTML
    - RSS
    - JSON # For search functionality

# Markdown rendering
markup:
  goldmark:
    renderer:
      unsafe: true # Allow raw HTML in markdown
  highlight:
    codeFences: true
    guessSyntax: true
    lineNos: true
    style: monokai
  tableOfContents:
    startLevel: 2
    endLevel: 6
    ordered: false

# Taxonomies
taxonomies:
  tag: tags
  category: categories
  series: series

# Privacy settings
privacy:
  googleAnalytics:
    respectDoNotTrack: true
  twitter:
    enableDNT: true

# Minification
minify:
  disableXML: true
  minifyOutput: true

# Caching
caches:
  assets:
    dir: :resourceDir/_gen
    maxAge: '24h'
  getjson:
    dir: :cacheDir/:project
    maxAge: '1h'

# Parameters (theme-specific)
params:
  author:
    name: 'Your Name'
    email: 'your@email.com'
    image: 'images/author.jpg'

  # Features
  features:
    portfolio:
      enable: true
    blog:
      enable: true
    darkMode:
      enable: true
      default: system

  # SEO
  description: 'Your site description for SEO'
  keywords: ['keyword1', 'keyword2']
  images: ['images/og-image.jpg']

  # Analytics (example: GoatCounter - privacy-friendly)
  analytics:
    goatCounter:
      code: 'your-code'

  # Social
  social:
    github: 'yourusername'
    linkedin: 'yourprofile'
    twitter: 'yourhandle'
```

### Content Organization Strategies

**Recommended structure:**

```
content/
├── _index.md              # Homepage content
├── about.md               # About page
├── posts/                 # Blog posts
│   ├── _index.md
│   ├── 2025/
│   │   ├── my-first-post/
│   │   │   ├── index.md
│   │   │   └── images/
│   │   │       └── hero.jpg
│   │   └── another-post.md
├── projects/              # Portfolio projects
│   ├── _index.md
│   ├── project-alpha/
│   │   └── index.md
│   └── project-beta.md
└── notes/                 # Quick notes/TILs
    ├── _index.md
    └── 2025-12-21-til.md
```

**Page bundles (recommended for posts with images):**

```
posts/
└── my-post/
    ├── index.md       # Content
    ├── hero.jpg       # Featured image
    └── diagram.png    # Inline image
```

Reference in markdown:

```markdown
![Diagram](diagram.png)
```

**Frontmatter best practices:**

```yaml
---
title: 'Your Post Title'
date: 2025-12-21T14:30:00Z
lastmod: 2025-12-21T16:00:00Z
draft: false
author: 'Your Name'

# SEO
description: 'A concise description (150-160 chars) for search engines'
keywords: ['keyword1', 'keyword2']

# Taxonomy
tags: ['tag1', 'tag2']
categories: ['Category']
series: ['Series Name'] # For multi-part posts

# Images
images:
  - 'posts/my-post/hero.jpg' # OG image

# Table of contents
toc:
  enable: true
  auto: true

# Comments (if using)
comments: true

# Math support (if needed)
math: true

# Code highlighting
highlight: true

# Custom params (theme-dependent)
hero: 'hero.jpg'
menu:
  sidebar:
    name: 'Display Name'
    identifier: 'unique-id'
    weight: 100
---
```

### Creating Archetypes (Content Templates)

**Create `archetypes/posts.md`:**

```yaml
---
title: "{{ replace .File.ContentBaseName "-" " " | title }}"
date: {{ .Date }}
draft: true
author: "Your Name"
description: ""

tags: []
categories: []

toc:
  enable: true

# hero: images/posts/{{ .File.ContentBaseName }}/hero.jpg
---

## Introduction

Why this topic matters...

## Main Content

Your content here...

## Conclusion

Key takeaways...

## Resources

- [Resource](https://example.com)
```

**Usage:**

```bash
hugo new posts/my-new-post.md
# Auto-fills template
```

### Custom Shortcodes

Create `layouts/shortcodes/note.html`:

```html
<div class="note"><strong>Note:</strong> {{ .Inner | markdownify }}</div>
```

**Use in markdown:**

```markdown
{{</* note */>}}
This is an important note!
{{</* /note */>}}
```

### Local Development Workflow

```bash
# Standard dev server
hugo server -D

# With drafts, future posts, and live reload
hugo server -D -F --navigateToChanged

# Bind to all interfaces (access from phone on same network)
hugo server -D --bind 0.0.0.0

# Fast render mode (disables some features)
hugo server --disableFastRender

# Clean build
rm -rf public resources && hugo
```

### Performance Optimization

**Image optimization:**

Install ImageMagick:

```bash
brew install imagemagick
```

**Optimize images before adding:**

```bash
# Resize large images
mogrify -resize 1920x1080\> -quality 85 -format jpg *.png

# Convert to WebP
for file in *.jpg; do
  cwebp -q 80 "$file" -o "${file%.jpg}.webp"
done
```

**Use Hugo's image processing:**

```go-html-template
{{ $img := resources.Get "images/hero.jpg" }}
{{ $optimized := $img.Resize "800x q80" }}
<img src="{{ $optimized.RelPermalink }}" alt="Hero">
```

### Version Control Best Practices

**`.gitignore` template:**

```gitignore
# Hugo build files
public/
resources/
.hugo_build.lock

# OS files
.DS_Store
Thumbs.db

# Editor files
.vscode/
.idea/
*.swp

# Dependencies
node_modules/
package-lock.json

# Environment files
.env
.env.local
```

**Git workflow:**

```bash
# Initial commit
git add .
git commit -m "Initial Hugo site setup"

# Create GitHub repo (using gh CLI)
gh repo create portfolio --public --source=. --remote=origin
git push -u origin main

# Regular workflow
git add .
git commit -m "Add new post: Building with Hugo"
git push
```

---

## Part 4: Theme Selection Deep Dive

### Evaluating Themes

**Key criteria:**

1. **Documentation quality** - Can you figure out how to configure it?
2. **Last updated** - Is it maintained? (Check GitHub)
3. **Features** - Portfolio? Blog? Both? Dark mode? Search?
4. **Performance** - Check Lighthouse scores on demo sites
5. **Customization** - Can you easily override layouts?
6. **Dependencies** - Does it require Node, PostCSS, etc.?

### Popular Themes Breakdown

#### 1. **Hugo Profile** (My Choice)

- **Best for:** Developer portfolios with blog
- **Features:** Hero section, About, Experience, Education, Projects, Achievements, Blog, Contact form, Light/Dark mode
- **Tech:** Bootstrap, Font Awesome
- **Customization:** YAML configuration files
- **Setup complexity:** Easy
- **Hugo version required:** 0.87.0+
- **GitHub:** https://github.com/gurusabarish/hugo-profile
- **Demo:** https://hugo-profile.netlify.app

**Quick start with Git Submodule:**

```bash
# Initialize git
git init

# Add theme as submodule
git submodule add https://github.com/gurusabarish/hugo-profile.git themes/hugo-profile
git submodule update --init --recursive
```

**Or with Hugo Modules:**

```bash
hugo mod init github.com/yourusername/portfolio
```

```yaml
# hugo.yaml
baseURL: 'https://yourwebsite.com/'
languageCode: 'en-us'
title: 'Your Name - Portfolio'
theme: hugo-profile  # Only for submodule method

# For Hugo modules, add:
module:
  imports:
    - path: github.com/gurusabarish/hugo-profile

outputs:
  home:
    - HTML
    - RSS
    - JSON

markup:
  goldmark:
    renderer:
      unsafe: true

params:
  title: 'Your Name'
  description: 'Software Engineer | Developer'
  favicon: '/images/fav.png'

  useBootstrapCDN: false
  animate: true

  theme:
    disableThemeToggle: false
    defaultTheme: 'light'

  # Hero section
  hero:
    enable: true
    intro: 'Hi, my name is'
    title: 'Your Name'
    subtitle: 'I build things for the web'
    content: 'A passionate developer focused on creating impactful digital experiences.'
    image: /images/hero.png
    socialLinks:
      fontAwesomeIcons:
        - icon: fab fa-github
          url: https://github.com/yourusername
        - icon: fab fa-linkedin
          url: https://linkedin.com/in/yourprofile

  # About section
  about:
    enable: true
    title: 'About Me'
    image: '/images/me.png'
    content: |
      I am a software developer with a passion for web development.
    skills:
      enable: true
      title: 'Here are a few technologies I work with:'
      items:
        - 'React'
        - 'Node.js'
        - 'Python'
        - 'Docker'

  # Experience section
  experience:
    enable: true
    items:
      - job: 'Senior Software Engineer'
        company: 'Company Name'
        companyUrl: 'https://example.com'
        date: 'Jan 2022 - Present'
        content: 'Description of your role and achievements'

  # Projects section
  projects:
    enable: true
    items:
      - title: 'Project Name'
        content: 'Project description'
        image: /images/projects/project.png
        links:
          - icon: fab fa-github
            url: https://github.com/yourusername/project

  # Blog configuration
  # Create posts in content/blogs/

  # Contact section
  contact:
    enable: true
    email: your@email.com
    btnName: 'Contact me'
```

**Content structure:**

```
content/
└── blogs/           # Blog posts go here
    └── my-post.md
static/
└── images/
    ├── hero.png
    ├── me.png
    └── projects/
```

**Creating blog posts:**

```bash
hugo new content/blogs/my-first-post.md
```

#### 2. **PaperMod**

- **Best for:** Minimalist blogs
- **Features:** Fast, clean, search, dark mode
- **Setup complexity:** Low
- **GitHub:** https://github.com/adityatelange/hugo-PaperMod

**Install:**

```bash
git submodule add https://github.com/adityatelange/hugo-PaperMod themes/PaperMod
echo "theme = 'PaperMod'" >> hugo.toml
```

#### 3. **Terminal**

- **Best for:** Retro/hacker aesthetic
- **Features:** Unique design, monospace fonts
- **Setup complexity:** Low

#### 4. **Anatole**

- **Best for:** Personal blogs with photo focus
- **Features:** Beautiful typography, sidebar
- **Setup complexity:** Low

#### 5. **Clarity**

- **Best for:** Technical documentation + blog
- **Features:** Search, syntax highlighting, mobile-first
- **Setup complexity:** Medium

### Customizing Themes

**Override layouts:**

Create `layouts/` directory matching theme structure:

```
layouts/
├── _default/
│   ├── baseof.html      # Override base template
│   └── single.html      # Override single post
├── partials/
│   ├── head.html        # Override head
│   └── footer.html      # Override footer
└── index.html           # Override homepage
```

**Custom CSS:**

Create `assets/css/custom.css`:

```css
/* Your custom styles */
.custom-header {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}
```

Reference in config:

```yaml
params:
  customCSS: ['css/custom.css']
```

---

## Part 5: Deployment Options (The Comparison You've Been Waiting For)

### Quick Comparison Table

| Platform                | Cost      | Ease of Setup | Performance | Custom Domain | Analytics      | Best For        |     |     |     |
| ----------------------- | --------- | ------------- | ----------- | ------------- | -------------- | --------------- | --- | --- | --- | --- | --- | --- |
| **GitHub Pages**        | Free      | Easy          | Good        | Yes (free)    | Via 3rd party  | Developers      |     |     |     |
| **Netlify**             | Free tier | Very Easy     | Excellent   | Yes (free)    | Yes            | Everyone        |     |     |     |
| **Vercel**              | Free tier | Very Easy     | Excellent   | Yes (free)    | Yes            | Developers      |     |     |     |
| **Cloudflare Pages**    | Free      | Easy          | Excellent   | Yes (free)    | Yes            | Privacy-focused |     |     |     |
| **AWS S3 + CloudFront** | ~$1-5/mo  | Complex       | Excellent   | Yes ($12/yr)  | Via CloudWatch | Enterprise      |     |     |     |     |     |     |
| **Firebase Hosting**    | Free tier | Medium        | Excellent   | Yes (free)    | Yes            | Firebase users  |     |     |     |
| **Render**              | Free tier | Easy          | Good        | Yes (free)    | No             | Simple deploys  |     |     |     |

### Detailed Deployment Guides

---

### Option 1: GitHub Pages (My Setup)

**Pros:**

- Completely free
- Automatic deployments on git push
- Reliable (backed by GitHub)
- Easy custom domain setup

**Cons:**

- Public repos only (free tier)
- Build time limits
- No serverless functions

**Setup Steps:**

#### 1. Create GitHub Repository

```bash
# If you haven't already
git init
git add .
git commit -m "Initial commit"

# Create repo using GitHub CLI
gh repo create portfolio --public --source=. --remote=origin --push

# Or manually: Go to github.com/new
```

#### 2. Create GitHub Actions Workflow

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy Hugo site to Pages

on:
  push:
    branches:
      - main
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: 'pages'
  cancel-in-progress: false

defaults:
  run:
    shell: bash

jobs:
  build:
    runs-on: ubuntu-latest
    env:
      HUGO_VERSION: 0.120.4
    steps:
      - name: Install Hugo CLI
        run: |
          wget -O ${{ runner.temp }}/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb \
          && sudo dpkg -i ${{ runner.temp }}/hugo.deb

      - name: Install Dart Sass
        run: sudo snap install dart-sass

      - name: Checkout
        uses: actions/checkout@v4
        with:
          submodules: recursive
          fetch-depth: 0

      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v4

      - name: Install Node.js dependencies
        run: '[[ -f package-lock.json || -f npm-shrinkwrap.json ]] && npm ci || true'

      - name: Build with Hugo
        env:
          HUGO_ENVIRONMENT: production
          HUGO_ENV: production
        run: |
          hugo \
            --gc \
            --minify \
            --baseURL "${{ steps.pages.outputs.base_url }}/"

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./public

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

#### 3. Enable GitHub Pages

1. Go to your repo on GitHub
2. Settings → Pages
3. Source: GitHub Actions
4. Save

#### 4. Push and Deploy

```bash
git add .github/workflows/deploy.yml
git commit -m "Add GitHub Actions workflow"
git push
```

Your site will be live at: `https://yourusername.github.io/portfolio/`

#### 5. Custom Domain (Optional)

**Buy a domain** (Namecheap, Google Domains, Cloudflare - ~$10-15/year)

**Add to GitHub:**

1. Repo Settings → Pages → Custom domain
2. Enter your domain (e.g., `yourdomain.com`)
3. Save

**Configure DNS (example: Cloudflare):**

Add these DNS records:

```
Type: A
Name: @
Content: 185.199.108.153
         185.199.109.153
         185.199.110.153
         185.199.111.153

Type: CNAME
Name: www
Content: yourusername.github.io
```

**Update `hugo.yml`:**

```yaml
baseURL: 'https://yourdomain.com/'
```

---

### Option 2: Netlify (Easiest for Non-Developers)

**Pros:**

- Extremely easy setup
- Automatic builds
- Form handling
- Serverless functions
- Deploy previews for PRs
- Built-in analytics (paid)

**Cons:**

- Build minute limits (free: 300/month)
- Bandwidth limits (free: 100GB/month)

**Setup Steps:**

#### 1. Sign Up

Go to [netlify.com](https://netlify.com) → Sign up with GitHub

#### 2. Deploy

1. "Add new site" → "Import an existing project"
2. Connect to GitHub
3. Select your repository
4. Build settings:
   - **Build command:** `hugo --gc --minify`
   - **Publish directory:** `public`
   - **Advanced:** Add environment variable:
     - `HUGO_VERSION`: `0.120.4`
5. Deploy site

#### 3. Custom Domain

1. Domain settings → Add custom domain
2. Follow DNS instructions
3. Enable HTTPS (automatic)

**netlify.toml (optional, for more control):**

```toml
[build]
  publish = "public"
  command = "hugo --gc --minify"

[build.environment]
  HUGO_VERSION = "0.120.4"
  HUGO_ENV = "production"
  HUGO_ENABLEGITINFO = "true"

[context.production.environment]
  HUGO_ENVIRONMENT = "production"

[context.deploy-preview]
  command = "hugo --gc --minify --buildFuture -b $DEPLOY_PRIME_URL"

[context.branch-deploy]
  command = "hugo --gc --minify -b $DEPLOY_PRIME_URL"

[[headers]]
  for = "/*"
  [headers.values]
    X-Frame-Options = "DENY"
    X-XSS-Protection = "1; mode=block"
    X-Content-Type-Options = "nosniff"

[[headers]]
  for = "/*.css"
  [headers.values]
    Cache-Control = "public, max-age=31536000, immutable"

[[headers]]
  for = "/*.js"
  [headers.values]
    Cache-Control = "public, max-age=31536000, immutable"
```

---

### Option 3: Vercel

**Pros:**

- Excellent performance
- Edge network
- Great developer experience
- Analytics (paid)

**Cons:**

- Commercial sites require paid plan

**Setup:**

1. Go to [vercel.com](https://vercel.com)
2. Import Git Repository
3. Framework Preset: Hugo
4. Deploy

**vercel.json (optional):**

```json
{
  "build": {
    "env": {
      "HUGO_VERSION": "0.120.4"
    }
  }
}
```

---

### Option 4: Cloudflare Pages

**Pros:**

- Cloudflare's global network
- Unlimited bandwidth (free)
- Privacy-focused
- Web analytics included

**Cons:**

- Newer platform (fewer integrations)

**Setup:**

1. [dash.cloudflare.com](https://dash.cloudflare.com) → Pages
2. Connect GitHub
3. Select repo
4. Build settings:
   - **Build command:** `hugo`
   - **Build output:** `public`
   - **Environment variable:** `HUGO_VERSION = 0.120.4`
5. Deploy

---

### Option 5: AWS S3 + CloudFront (For the Over-Engineers)

**Pros:**

- Enterprise-grade
- Full control
- Can handle massive traffic

**Cons:**

- Complex setup
- Costs money (minimal, but not free)
- Requires AWS knowledge

**Estimated costs:** $1-3/month for small sites

**High-level steps:**

1. Create S3 bucket
2. Enable static website hosting
3. Build Hugo site locally: `hugo --gc --minify`
4. Upload `public/` to S3: `aws s3 sync public/ s3://your-bucket`
5. Create CloudFront distribution
6. Configure Route53 for custom domain
7. Set up SSL certificate (free via ACM)

**Not recommended unless you're already in AWS ecosystem.**

---

### My Recommendation

| Your Situation            | Best Choice                |
| ------------------------- | -------------------------- |
| **Developer with GitHub** | GitHub Pages               |
| **Complete beginner**     | Netlify                    |
| **Want best performance** | Vercel or Cloudflare Pages |
| **Privacy-conscious**     | Cloudflare Pages           |
| **Need forms/functions**  | Netlify                    |
| **Enterprise/scale**      | AWS or Cloudflare          |

**My setup:** GitHub Pages + Cloudflare (for DNS and caching)

---

## Part 6: Adding Features

### Analytics (Privacy-Friendly)

**Options:**

1. **GoatCounter** (Free, open-source, privacy-friendly)

   ```yaml
   params:
     analytics:
       goatCounter:
         code: 'yourcode'
   ```

   Sign up: [goatcounter.com](https://goatcounter.com)

2. **Plausible** (Paid, privacy-focused, beautiful UI)
   ~$9/month for 10k pageviews
3. **Cloudflare Web Analytics** (Free, privacy-first)
   Add script to `layouts/partials/head.html`

### Comments

**Options:**

1. **Giscus** (GitHub Discussions-powered, free)

   - Enable Discussions on your repo
   - Configure at [giscus.app](https://giscus.app)
   - Add script to layouts

2. **Utterances** (GitHub Issues-powered)
3. **Disqus** (Traditional, but privacy concerns)

### Search

**For static sites:**

1. **Built-in JSON index**

   ```yaml
   outputs:
     home:
       - HTML
       - RSS
       - JSON
   ```

2. **Fuse.js** (client-side search)
3. **Algolia** (external service, free tier available)

### Contact Forms

**Options:**

1. **Netlify Forms** (if on Netlify)

   ```html
   <form name="contact" method="POST" data-netlify="true">
     <input type="email" name="email" required />
     <textarea name="message" required></textarea>
     <button type="submit">Send</button>
   </form>
   ```

2. **Formspree** (free tier: 50/month)
3. **Google Forms** (embed)

---

## Part 7: Content Writing Tips

### Post Structure That Works

1. **Hook** - Why should I care?
2. **Context** - What's the background?
3. **Main content** - The meat
4. **Visuals** - Code, diagrams, screenshots
5. **Conclusion** - Key takeaways
6. **Resources** - Further reading

### SEO Basics

```yaml
# In frontmatter
title: 'Clear, descriptive title with keywords'
description: '150-160 char description for Google preview'
keywords: ['keyword1', 'keyword2']
images: ['path/to/og-image.jpg'] # For social shares
```

**Create `layouts/partials/seo.html`:**

```html
<meta name="description" content="{{ .Description }}" />
<meta property="og:title" content="{{ .Title }}" />
<meta property="og:description" content="{{ .Description }}" />
<meta
  property="og:image"
  content="{{ .Site.BaseURL }}{{ index .Params.images 0 }}"
/>
<meta name="twitter:card" content="summary_large_image" />
```

### Code Syntax Highlighting

Hugo has built-in syntax highlighting:

````markdown
```python
def hello():
    print("Hello, world!")
```
````

````

**Configure in `hugo.yml`:**

```yaml
markup:
  highlight:
    codeFences: true
    guessSyntax: true
    lineNos: true
    style: monokai  # or: github, dracula, etc.
````

---

## Part 8: Maintenance & Workflow

### Regular Tasks

**Weekly:**

- Write content
- Push to GitHub (auto-deploys)

**Monthly:**

- Update Hugo: `brew upgrade hugo`
- Update theme: `hugo mod get -u`
- Check analytics
- Respond to comments

**Quarterly:**

- Review old posts for updates
- Check broken links
- Audit performance (Lighthouse)

### Backup Strategy

Your site is already backed up (it's in GitHub!), but:

```bash
# Clone to another location periodically
git clone https://github.com/yourusername/portfolio.git backup-portfolio

# Or use GitHub's export feature
```

### Content Ideas When You're Stuck

- TIL (Today I Learned) posts
- Bug fixes you solved
- Tutorials you wish existed
- Book/course reviews
- Project retrospectives
- Tools you use
- Career reflections
- "How I built this" posts (like this one!)

---

## Part 9: Troubleshooting Common Issues

### "Hugo command not found"

**Solution:** Reinstall Hugo or add to PATH

```bash
# Mac
brew install hugo

# Verify
which hugo
```

### "Theme not found"

**Solution:**

- Check `hugo.yml` has correct theme name
- For modules: `hugo mod get -u`
- For submodules: `git submodule update --init --recursive`

### "Site looks broken locally"

**Solution:** Check baseURL

```yaml
# hugo.yml - for local dev, use:
baseURL: 'http://localhost:1313/'
# Or use environment-specific:
# baseURL: '/'  # Hugo will use current URL
```

### "Images not showing"

**Solution:**

- Images go in `static/` or `assets/`
- Reference from markdown: `/images/photo.jpg`
- Or use page bundles (see above)

### "Build failing on Netlify/Vercel"

**Common causes:**

- Wrong Hugo version
- Missing environment variables
- Theme not properly installed

**Solution:** Check build logs, set `HUGO_VERSION` variable

---

## Conclusion: You're Ready to Build

Building a portfolio and blog with Hugo might seem intimidating, but it's actually pretty straightforward once you get past the initial setup. Here's what makes it worth it:

- **Performance**: Your site will be blazing fast
- **Cost**: Free to nearly free
- **Control**: You own your content and platform
- **Learning**: You'll understand how the web works
- **Flexibility**: Endless customization possibilities

### Your Next Steps

1. **Pick your path**: Non-technical or technical guide above
2. **Choose a theme**: Browse [themes.gohugo.io](https://themes.gohugo.io)
3. **Set up locally**: Follow the installation steps
4. **Write your first post**: Use the template
5. **Deploy**: Choose GitHub Pages or Netlify
6. **Share**: Post on LinkedIn, Twitter, wherever

### What I Wish I Knew Starting Out

- Start simple, customize later
- Perfect is the enemy of shipped
- Writing is harder than setup (allocate time accordingly)
- Your first posts will be rough—that's okay
- The community is helpful (Hugo Discourse, Reddit)

---

## Resources

### Official Documentation

- [Hugo Docs](https://gohugo.io/documentation/)
- [Hugo Themes](https://themes.gohugo.io/)
- [Hugo Discourse](https://discourse.gohugo.io/)

### Tools I Use

- **Editor**: VS Code with Hugo extension
- **Markdown**: [Markdown Guide](https://www.markdownguide.org/)
- **Images**: [TinyPNG](https://tinypng.com/) for compression
- **Diagrams**: [Excalidraw](https://excalidraw.com/)
- **Icons**: [Font Awesome](https://fontawesome.com/)

### Learning Resources

- [Hugo Quick Start](https://gohugo.io/getting-started/quick-start/)
- [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
- [Intro to Git](https://www.freecodecamp.org/news/git-and-github-for-beginners/)

### Hosting Comparisons

- [GitHub Pages Docs](https://docs.github.com/en/pages)
- [Netlify Docs](https://docs.netlify.com/)
- [Vercel Docs](https://vercel.com/docs)
- [Cloudflare Pages Docs](https://developers.cloudflare.com/pages/)

---

## One More Thing

If you build your portfolio using this guide, I'd genuinely love to see it. Send me a link at contact@puneeth.io or tag me on LinkedIn. Seriously—seeing what people build makes my day.

And if you get stuck? The Hugo community is incredibly helpful. Post on the [Discourse forum](https://discourse.gohugo.io/) and you'll usually get help within hours.

**Now stop reading and start building.** Your future self will thank you.

---

**Questions? Stuck somewhere? Reach out at contact@puneeth.io**

_This post will be updated periodically as Hugo evolves and I learn new tricks. Last updated: December 2025_
