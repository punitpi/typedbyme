# typedbyme

> Personal portfolio website built with Hugo and the Toha theme

[![Hugo](https://img.shields.io/badge/Hugo-0.148+-blue.svg)](https://gohugo.io)
[![Theme](https://img.shields.io/badge/Theme-Toha-green.svg)](https://github.com/hugo-toha/toha)
[![License](https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey.svg)](http://creativecommons.org/licenses/by-nc/4.0/)

## 🌐 Live Site

Visit my portfolio at: [typedbyme.puneeth.io](https://typedbyme.puneeth.io/)

## 🚀 About

This is my personal portfolio website showcasing my experience as a software developer with 7+ years in:
- **Languages**: C#, Node.js, JavaScript, Python
- **Cloud**: AWS, Azure
- **Databases**: SQL Server, MongoDB, MySQL, DynamoDB, Redis
- **DevOps**: Docker, Kubernetes, CI/CD
- **Architecture**: Microservices, API Development

## 🛠️ Built With

- **[Hugo](https://gohugo.io/)** - Static site generator
- **[Toha Theme](https://github.com/hugo-toha/toha)** - Modern portfolio theme
- **Hugo Modules** - For theme management
- **GitHub Actions** - For automated deployment (if applicable)

## 🏗️ Local Development

### Prerequisites

- [Hugo Extended](https://gohugo.io/installation/) (v0.148.0+)
- [Node.js](https://nodejs.org/) (for theme dependencies)
- [Go](https://golang.org/) (for Hugo modules)

### Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/punitpi/typedbyme.git
   cd typedbyme
   ```

2. **Install dependencies**
   ```bash
   npm install
   hugo mod get -u
   ```

3. **Start development server**
   ```bash
   hugo server -D
   ```

4. **Open in browser**
   Navigate to `http://localhost:1313`

### Building for Production

```bash
hugo --minify
```

The generated site will be in the `public/` directory.

## 📁 Project Structure

```
typedbyme/
├── assets/                 # Theme assets and images
│   └── images/
│       └── author/         # Profile images
├── content/                # Blog posts and content
├── data/                   # Site configuration data
│   └── en/
│       ├── author.yaml     # Personal information
│       └── about.yaml      # About section data
├── static/                 # Static files
├── hugo.yml               # Hugo configuration
├── package.json           # Node.js dependencies
└── go.mod                 # Hugo modules
```

## ⚙️ Configuration

### Personal Information

Edit `data/en/author.yaml` to update:
- Personal details
- Contact information
- Professional summary

### About Section

Edit `data/en/about.yaml` to update:
- Skills and expertise
- Certifications
- Social links

### Site Settings

Edit `hugo.yml` for:
- Site metadata
- Theme configuration
- Module settings

## 🎨 Customization

The Toha theme offers extensive customization options:

- **Colors & Styling**: Modify theme variables
- **Sections**: Enable/disable portfolio sections
- **Content**: Add blog posts, projects, experiences
- **Analytics**: Configure tracking (Google Analytics, etc.)

Refer to the [Toha documentation](https://toha-guides.netlify.app/) for detailed customization options.

## 📝 Adding Content

### Blog Posts
```bash
hugo new posts/my-new-post.md
```

### Projects
Add project data in `data/en/sections/projects.yaml`

### Experience
Add experience data in `data/en/sections/experiences.yaml`

## 🚀 Deployment

This site can be deployed to various platforms:

- **Netlify**: Connect your Git repository
- **Vercel**: Import from GitHub
- **GitHub Pages**: Use GitHub Actions
- **AWS S3/CloudFront**: Upload `public/` directory

## 🤝 Contributing

While this is a personal portfolio, you're welcome to:
- Report bugs or issues
- Suggest improvements
- Use as inspiration for your own portfolio

Please note: Personal content (images, resume, contact info) is not available for reuse.

## 📄 License

This project is licensed under the [Creative Commons Attribution-NonCommercial 4.0 International License](LICENSE).

- ✅ **Code & Structure**: Free to use with attribution
- ❌ **Personal Content**: Requires explicit permission

## 📬 Contact

- **Website**: [typedbyme.puneeth.io](https://typedbyme.puneeth.io/)
- **Email**: [contact@puneeth.io](mailto:contact@puneeth.io)
- **GitHub**: [@punitpi](https://github.com/punitpi)
- **LinkedIn**: [ppuneeth](https://www.linkedin.com/in/ppuneeth/)

---

⭐ If you found this useful, please consider giving it a star!
