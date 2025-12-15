# Ragelang Website

The official website for Ragelang, a programming language built for [Langjam Gamejam 2025](https://langjamgamejam.com).

## 🚀 Quick Start

### Prerequisites

- Ruby 2.7+ (recommended: 3.0+)
- Bundler (`gem install bundler`)

### Local Development

```bash
# Install dependencies
bundle install

# Start the development server
bundle exec jekyll serve

# Visit http://localhost:4000
```

### Building for Production

```bash
bundle exec jekyll build
# Output will be in the _site directory
```

## 📁 Project Structure

```
├── _config.yml          # Jekyll configuration
├── _layouts/            # Page templates
│   ├── default.html     # Base layout
│   ├── page.html        # Static pages
│   ├── post.html        # Blog posts
│   └── doc.html         # Documentation pages
├── _includes/           # Reusable components
│   ├── head.html        # HTML <head>
│   ├── header.html      # Site navigation
│   └── footer.html      # Site footer
├── _posts/              # Blog posts (add new posts here!)
├── _docs/               # Documentation pages
├── assets/
│   ├── css/style.css    # Main stylesheet (Dracula theme)
│   └── images/          # Images and favicon
├── index.html           # Landing page
├── about.md             # About page
├── blog.html            # Blog listing
└── docs.html            # Documentation index
```

## ✍️ Writing Blog Posts

1. Create a new file in `_posts/` with the format:
   ```
   YYYY-MM-DD-your-post-title.md
   ```

2. Add front matter at the top:
   ```yaml
   ---
   layout: post
   title: "Your Post Title"
   date: YYYY-MM-DD
   author: Your Name
   tags: [tag1, tag2]
   ---
   ```

3. Write your content in Markdown below the front matter.

### Example Post

```markdown
---
layout: post
title: "Day 2: Building the Lexer"
date: 2025-12-16
author: Ragelang Team
tags: [devlog, implementation]
---

Today we built the lexer for Ragelang...
```

## 📚 Adding Documentation

1. Create a new file in `_docs/`:
   ```
   your-doc-page.md
   ```

2. Add front matter:
   ```yaml
   ---
   layout: doc
   title: Your Page Title
   description: Brief description
   order: 4  # Controls sidebar ordering
   ---
   ```

3. Write documentation in Markdown.

## 🎨 Theme

This site uses a custom dark theme with fiery accents inspired by the "Rage" in Ragelang:

| Color | Hex | Usage |
|-------|-----|-------|
| Background | `#12131a` | Main background |
| Secondary | `#1a1c25` | Cards, header |
| Ember | `#e89b4a` | Primary accent |
| Flame | `#f06543` | Secondary accent |
| Teal | `#3fc1b0` | Highlights, tags |
| Mint | `#5cc98c` | Success states |
| Sand | `#d4c07a` | Strings, warnings |

Edit `assets/css/style.css` to customize.

## 🌐 Deploying to GitHub Pages

This site is configured to deploy automatically with GitHub Pages:

1. Push to the `main` branch
2. GitHub Actions will build and deploy the site
3. Visit `https://rizato.github.io` (or your custom domain)

### Manual Deployment

If you need to deploy manually:

```bash
bundle exec jekyll build
# Upload _site/ contents to your hosting provider
```

## 📝 License

This website and its content are part of the Ragelang project for Langjam Gamejam 2025.

## 🔗 Links

- [Langjam Gamejam](https://langjamgamejam.com)
- [GitHub Repository](https://github.com/Rizato/ragelang)
