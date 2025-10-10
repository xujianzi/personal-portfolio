# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a personal portfolio website for Jian Xu, a GIS and spatial data scientist. The project consists of:

1. **Main Portfolio** (`index.html`): A single-page portfolio built with HTML, Tailwind CSS, and JavaScript
2. **Documentation Site** (`docs-site/`): A MkDocs-based technical blog and documentation site

The documentation site builds to the `work/` directory and is deployed to `/work/` path on the live site.

## Architecture

### Main Portfolio (`index.html`)
- Single-page application using vanilla HTML/CSS/JavaScript
- Tailwind CSS via CDN for styling
- EmailJS integration for contact form functionality
- Custom CSS animations (floating elements, gradient backgrounds)
- Responsive design with mobile-first approach
- Sections: Hero, About, Skills, Projects, Contact

### Documentation Site (`docs-site/`)
- **Source**: `docs-site/docs/` - Markdown documentation files
- **Config**: `docs-site/mkdocs.yml` - MkDocs configuration
- **Build Output**: `work/` - Generated HTML files
- **Theme**: Material for MkDocs with custom palette (light/dark mode)
- **Content Categories**:
  - Projects: COVID Dashboard, Chat Bot
  - Frontend: Basic frontend guides, EmailJS
  - Data Science: Data format tutorials
  - Linux: Basic instructions
  - Tools: Cloudflared, Docker, uv
  - LLMs: Claude documentation

## Common Commands

### Documentation Site (MkDocs)

**Build the documentation site:**
```bash
cd docs-site
mkdocs build
```
This builds from `docs-site/docs/` to `work/` directory.

**Serve documentation locally for development:**
```bash
cd docs-site
mkdocs serve
```
Default serves at http://127.0.0.1:8000

**Deploy/update the work site:**
After editing documentation in `docs-site/docs/`, run build to update `work/` directory:
```bash
cd docs-site && mkdocs build
```

### Main Portfolio

No build process required - edit `index.html` directly and refresh browser.

## Important Configuration Details

### MkDocs Configuration (`docs-site/mkdocs.yml`)
- `docs_dir: docs` - Source markdown files location
- `site_dir: ../work` - Build output directory (relative to docs-site/)
- `use_directory_urls: false` - Generates `.html` files instead of directory structure
- `base_path: /work/` - Critical for correct routing on deployed site

### Git Commit Message Style
Commits follow conventional commit format with emoji:
```
<type>(<scope>): <description>
```
Examples:

- `docs(Docker): 更新Docker文档并修复jquery链接`
- `feat(docs): 添加Chat Bot项目文档及更新导航配置`

Common types: `docs`, `feat`, `fix`

## File Structure Notes

- `/index.html` - Main portfolio landing page
- `/public/images/` - Image assets for main portfolio
- `/docs-site/docs/` - Markdown source files for documentation
- `/docs-site/docs/assets/` - Assets for documentation (images, etc.)
- `/work/` - **Generated directory** from MkDocs build (do not edit directly)
- `/CNAME` - Custom domain configuration
- `/requirements.txt` - Python dependencies for MkDocs

## Deployment

- **Main site**: Deployed on github page on https://www.geopulse.fun/
- **Documentation**: Built to `/work/` and served at `/work/` path
- **Custom domain**: Configured via CNAME

## Content Management

When adding new documentation:
1. Create markdown file in `docs-site/docs/<category>/`
2. Update navigation in `docs-site/mkdocs.yml` under `nav:`
3. Run `mkdocs build` from `docs-site/` directory
4. Commit both source markdown and generated HTML in `work/`

## Dependencies

Python packages (install via `pip install -r requirements.txt`):
- `mkdocs-material` - Material theme for MkDocs
- `mkdocs-git-revision-date-plugin` - Shows last update time on pages
