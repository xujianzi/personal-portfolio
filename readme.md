<div align="center">

# 🌐 Personal Portfolio & Documentation Hub

**A modern, responsive portfolio website with integrated technical documentation**

[![Live Demo](https://img.shields.io/badge/demo-online-brightgreen)](https://personal-portfolio-theta-wheat.vercel.app/)
[![Deployment](https://img.shields.io/badge/Deployed%20on-Vercel-black?logo=vercel)](https://vercel.com)
[![MkDocs](https://img.shields.io/badge/Docs-MkDocs%20Material-blue?logo=markdown)](https://www.geopulse.fun/work/)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![HTML](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
[![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)](https://www.python.org/)

[Live Demo](https://personal-portfolio-theta-wheat.vercel.app/) • [Documentation](https://www.geopulse.fun/work/) • [Report Bug](https://github.com/xujianzi/personal-portfolio/issues)

</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Demo](#-demo)
- [Tech Stack](#-tech-stack)
- [Installation](#-installation)
- [Usage](#-usage)
- [Architecture](#-architecture)
- [Documentation Site](#-documentation-site)
- [Customization](#-customization)
- [Deployment](#-deployment)
- [Contributing](#-contributing)
- [License](#-license)
- [Acknowledgements](#-acknowledgements)

---

## 🚀 Overview

A **dual-purpose web platform** combining a modern personal portfolio with a comprehensive technical documentation site. Built for **Jian Xu**, a GIS and spatial data scientist, this project showcases professional work while providing an organized knowledge base for technical tutorials, project documentation, and tools.

### What Makes It Special?

- **🎨 Stunning Visual Design**: Animated gradient backgrounds, floating elements, and smooth transitions
- **📱 Fully Responsive**: Optimized for desktop, tablet, and mobile devices
- **📚 Integrated Documentation**: MkDocs-powered blog with topics ranging from Docker to LLMs
- **⚡ Zero Build Complexity**: Main portfolio runs directly in the browser—no compilation needed
- **🌙 Dark Mode Support**: Documentation site features light/dark theme toggle

---

## ✨ Features

### Main Portfolio (`index.html`)

- ✅ **Hero Section** with animated gradient background and floating elements
- ✅ **About Section** highlighting professional background
- ✅ **Skills Showcase** with categorized tech stack (Frontend, Backend, Tools, Languages)
- ✅ **Project Gallery** featuring COVID Dashboard and Chat Bot projects
- ✅ **Contact Form** powered by EmailJS for direct communication
- ✅ **Responsive Navigation** with smooth scroll and hover effects
- ✅ **Social Links** (GitHub, LinkedIn, Google Scholar, ResearchGate)

### Documentation Site (`docs-site/`)

- 📖 **Project Documentation**: COVID Dashboard, Chat Bot
- 🎨 **Frontend Guides**: Basic frontend techniques, EmailJS integration
- 📊 **Data Science Tutorials**: Long-format vs wide-format data
- 🐧 **Linux Instructions**: Essential commands and workflows
- 🛠️ **Tools & DevOps**: Docker, Cloudflared, uv package manager
- 🤖 **LLM Documentation**: Claude AI guides
- 🔍 **Full-Text Search** and git-based revision tracking

---

## 🎬 Demo

### Main Portfolio
![Portfolio Screenshot](https://via.placeholder.com/800x400.png?text=Portfolio+Hero+Section)

**Live Site**: [https://www.geopulse.fun/](https://www.geopulse.fun/)

### Documentation Site
![Docs Screenshot](https://via.placeholder.com/800x400.png?text=MkDocs+Documentation)

**Live Docs**: [https://www.geopulse.fun/work/](https://www.geopulse.fun/work/)

---

## 🛠️ Tech Stack

### Frontend
- **HTML5** - Semantic markup
- **Tailwind CSS** (CDN) - Utility-first styling
- **Vanilla JavaScript** - Interactive functionality
- **EmailJS** - Contact form backend
- **Font Awesome** - Icons
- **Academicons** - Academic social icons

### Documentation
- **Python 3.x** - Build tooling
- **MkDocs** - Static site generator
- **Material for MkDocs** - Premium theme
- **Git Revision Date Plugin** - Automatic timestamp tracking

### Deployment
- **Vercel** - Main portfolio hosting
- **GitHub Pages** - Documentation hosting
- **Custom Domain** - CNAME configuration

---

## 📦 Installation

### Prerequisites

- **Web Browser** (for portfolio)
- **Python 3.7+** (for documentation)
- **pip** package manager

### Quick Start

```bash
# Clone the repository
git clone https://github.com/xujianzi/personal-portfolio.git
cd personal-portfolio

# Option 1: Run portfolio directly
# Open index.html in your browser

# Option 2: Set up documentation site
pip install -r requirements.txt
cd docs-site
mkdocs serve
```

Visit `http://127.0.0.1:8000` to view the documentation locally.

---

## 🧠 Usage

### Viewing the Portfolio

```bash
# Simply open the HTML file
open index.html  # macOS
start index.html # Windows
xdg-open index.html # Linux
```

Or use a local server:

```bash
python -m http.server 8080
# Visit http://localhost:8080
```

### Building Documentation

```bash
cd docs-site

# Serve locally with hot reload
mkdocs serve

# Build static files to ../work/ directory
mkdocs build

# Deploy to GitHub Pages (optional)
mkdocs gh-deploy
```

### Adding New Documentation

1. Create a markdown file in `docs-site/docs/<category>/`
2. Update navigation in `docs-site/mkdocs.yml`:

```yaml
nav:
  - New Category:
      - New Page: category/new-page.md
```

3. Build and commit:

```bash
cd docs-site && mkdocs build
git add docs-site/docs/ work/
git commit -m "docs: add new documentation page"
```

---

## ⚙️ Architecture

```
personal-portfolio/
├── index.html              # Main portfolio page
├── CNAME                   # Custom domain config
├── requirements.txt        # Python dependencies
├── README.md              # This file
│
├── public/
│   └── images/            # Portfolio image assets
│
├── docs-site/             # Documentation source
│   ├── mkdocs.yml        # MkDocs configuration
│   └── docs/             # Markdown files
│       ├── index.md      # Docs homepage
│       ├── Projects/     # Project documentation
│       ├── Frontend/     # Frontend guides
│       ├── DataScience/  # Data science tutorials
│       ├── Linux/        # Linux guides
│       ├── Tools/        # DevOps tools
│       ├── LLMs/         # AI/LLM documentation
│       └── assets/       # Images and media
│
└── work/                  # Generated docs (built from docs-site/)
    └── *.html            # Static HTML files
```

### Key Design Decisions

| Component | Technology | Rationale |
|-----------|-----------|-----------|
| Portfolio | Vanilla HTML/CSS/JS | Zero build complexity, instant loading |
| Styling | Tailwind CSS (CDN) | Rapid development, no build step |
| Documentation | MkDocs Material | Professional theme, excellent UX |
| Deployment | Vercel | Automatic deployments, edge network |
| Email | EmailJS | No backend required, spam protection |

---

## 📚 Documentation Site

The documentation site is built with **MkDocs Material** and deployed to `/work/` path.

### Configuration Highlights

```yaml
# docs-site/mkdocs.yml
site_name: "Jian Xu's Work Space"
docs_dir: docs
site_dir: ../work              # Builds to project root /work/
use_directory_urls: false      # Generates .html files
```

### Content Categories

| Category | Topics |
|----------|--------|
| **Projects** | COVID Dashboard, Chat Bot |
| **Frontend** | HTML/CSS basics, EmailJS integration |
| **Data Science** | Data format conversions, analysis workflows |
| **Linux** | Command-line essentials |
| **Tools** | Docker, Cloudflared, uv package manager |
| **LLMs** | Claude AI documentation |

### Features

- 🔍 **Full-text search** across all documentation
- 🕒 **Git-based timestamps** showing last update time
- 🏷️ **Tag system** for content organization
- 🌓 **Light/dark mode** with smooth transitions
- 📱 **Mobile-optimized** navigation and reading experience

---

## 🎨 Customization

### Portfolio Configuration

**Update Personal Information** (`index.html`):

```html
<!-- Line 6: Change title -->
<title>Your Name | Personal Portfolio</title>

<!-- Lines 200-220: Update hero section -->
<h1>Your Name</h1>
<p>Your Tagline</p>
```

**EmailJS Setup** (Lines 8-9, 580-595):

1. Sign up at [EmailJS](https://www.emailjs.com/)
2. Create email service and template
3. Replace credentials:

```javascript
emailjs.init("YOUR_PUBLIC_KEY");
emailjs.send("YOUR_SERVICE_ID", "YOUR_TEMPLATE_ID", params);
```

### Documentation Customization

**Theme Colors** (`docs-site/mkdocs.yml`):

```yaml
theme:
  palette:
    - scheme: default
      primary: indigo      # Change to: blue, teal, green, etc.
      accent: light blue   # Change to: amber, pink, etc.
```

**Social Links**:

```yaml
extra:
  social:
    - icon: fontawesome/brands/github
      link: https://github.com/yourusername
```

---

## 🚢 Deployment

### Deploy to GitHub Pages

```bash
# Enable GitHub Pages in repository settings
# Select "Deploy from branch" → gh-pages

# Deploy documentation
cd docs-site
mkdocs gh-deploy
```

### Deploy to Netlify

1. Connect repository to [Netlify](https://app.netlify.com/)
2. Set build command: `cd docs-site && mkdocs build`
3. Set publish directory: `work/`

### Custom Domain

Add `CNAME` file with your domain:

```
yourdomain.com
```

Update DNS records:
```
Type: CNAME
Name: www
Value: your-site.vercel.app
```

---

## 🧪 Testing & Development

### Local Development Server

```bash
# Python simple server
python -m http.server 8080

# Or use PHP
php -S localhost:8080

# Or Node.js http-server
npx http-server -p 8080
```

### Documentation Preview

```bash
cd docs-site
mkdocs serve --dev-addr localhost:8000
```

### Validation

```bash
# Validate HTML (requires validator.nu)
curl -H "Content-Type: text/html; charset=utf-8" \
     --data-binary @index.html \
     https://validator.nu/?out=gnu

# Check broken links in docs
mkdocs build --strict
```

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Commit your changes** (use conventional commits)
   ```bash
   git commit -m "feat(portfolio): add new project section"
   ```
4. **Push to the branch**
   ```bash
   git push origin feature/amazing-feature
   ```
5. **Open a Pull Request**

### Commit Message Convention

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<scope>): <description>

Examples:
docs(Docker): update Docker documentation
feat(portfolio): add skills section
fix(contact): resolve EmailJS integration bug
```

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2025 Jian Xu

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction...
```

---

## 🙏 Acknowledgements

### Frameworks & Libraries
- [Tailwind CSS](https://tailwindcss.com/) - Utility-first CSS framework
- [MkDocs Material](https://squidfunk.github.io/mkdocs-material/) - Documentation theme
- [EmailJS](https://www.emailjs.com/) - Email service for contact forms
- [Font Awesome](https://fontawesome.com/) - Icon library
- [Academicons](https://jpswalsh.github.io/academicons/) - Academic icons

### Inspiration
- [FastAPI Docs](https://fastapi.tiangolo.com/) - Documentation structure
- [LangChain](https://github.com/langchain-ai/langchain) - README design
- [Stable Diffusion](https://github.com/Stability-AI/stablediffusion) - Project organization

### Hosting & Tools
- [Vercel](https://vercel.com/) - Portfolio deployment
- [GitHub Pages](https://pages.github.com/) - Documentation hosting
- [Python](https://www.python.org/) - Build tooling

---

<div align="center">

**Made with ❤️ by [Jian Xu](https://github.com/xujianzi)**

[![GitHub](https://img.shields.io/badge/GitHub-xujianzi-181717?logo=github)](https://github.com/xujianzi)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Jian%20Xu-0077B5?logo=linkedin)](https://linkedin.com/in/jian-xu-gis/)

⭐ Star this repo if you find it helpful!

</div>
