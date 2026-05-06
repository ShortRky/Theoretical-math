# Open-Source Idea Repository Website - Implementation Plan

## Overview

A public, collaborative knowledge library hosted on GitHub Pages for storing, organizing, and sharing notes, schoolwork, and mathematical theories with MathJax rendering.

---

## 1. Technical Architecture

### Recommended Stack: **Jekyll + GitHub Pages**

**Why Jekyll?**
- Native GitHub Pages support (no build step required)
- Built-in Markdown processing
- Liquid templating for dynamic content
- Large plugin ecosystem
- Zero-config deployment

### MathJax Integration

```html
<!-- In _layouts/default.html -->
<script>
  MathJax = {
    tex: {
      inlineMath: [['$', '$'], ['\\(', '\\)']],
      displayMath: [['$$', '$$'], ['\\[', '\\]']],
      processEscapes: true,
      processEnvironments: true
    },
    options: {
      skipHtmlTags: ['script', 'noscript', 'style', 'textarea', 'pre']
    }
  };
</script>
<script id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>
```

### Alternative: Pure HTML/CSS/JS (No SSG)

For maximum simplicity and longevity:
- Static HTML files with client-side JavaScript
- No build dependencies
- Easier for non-technical contributors

---

## 2. Data Storage

### File Structure

```
/ideas/
├── _posts/                    # Blog-style entries
│   ├── 2024-01-15-eulers-identity.md
│   └── 2024-01-16-group-theory-basics.md
├── _theories/                 # Mathematical theories
│   ├── calculus/
│   │   └── fundamental-theorem.md
│   └── algebra/
│       └── galois-theory.md
├── _notes/                    # Study notes
│   ├── physics/
│   └── computer-science/
├── _data/                     # JSON metadata
│   ├── categories.json
│   └── tags.json
└── _submissions/              # Pending submissions
    └── template.md
```

### Content Format (Markdown with Front Matter)

```markdown
---
title: "Euler's Identity and Its Implications"
author: "contributor-name"
date: 2024-01-15
tags: [mathematics, complex-analysis, euler]
category: theories
math: true
---

## Introduction

Euler's identity is considered one of the most beautiful equations in mathematics:

$$e^{i\pi} + 1 = 0$$

### Proof

Using Euler's formula: $e^{ix} = \cos(x) + i\sin(x)$...
```

### JSON Data Files

```json
// _data/categories.json
{
  "theories": {
    "name": "Mathematical Theories",
    "description": "Formal mathematical theories and proofs",
    "icon": "📐"
  },
  "notes": {
    "name": "Study Notes",
    "description": "Class notes and study materials",
    "icon": "📚"
  },
  "ideas": {
    "name": "Ideas & Concepts",
    "description": "Original ideas and brainstorming",
    "icon": "💡"
  }
}
```

---

## 3. User Interaction System

### Option A: GitHub Pull Requests (Recommended)

**Workflow:**
1. User forks the repository
2. Creates a new `.md` file in `/ideas/_submissions/`
3. Submits a pull request
4. Maintainers review and merge

**Submission Template:**

```markdown
---
title: "[Your Title Here]"
author: "[Your GitHub Username or Anonymous]"
date: YYYY-MM-DD
tags: [tag1, tag2]
category: ideas
status: pending
---

## Content

Write your content here using Markdown and LaTeX.

**Example equation:** $E = mc^2$
```

### Option B: GitHub Discussions

- Use GitHub Discussions as a submission queue
- Maintainers convert discussions to markdown files
- Lower barrier to entry for non-technical users

### Option C: Form with GitHub Actions

```yaml
# .github/workflows/submission-form.yml
name: Process Submission
on:
  issues:
    types: [opened, edited]
    
jobs:
  process:
    runs-on: ubuntu-latest
    steps:
      - name: Create file from issue
        uses: actions/github-script@v6
        with:
          script: |
            // Convert issue to markdown file
```

---

## 4. Longevity & Accessibility

### Documentation Strategy

```
/docs/
├── CONTRIBUTING.md       # How to contribute
├── MAINTAINING.md        # Maintainer guide
├── ARCHITECTURE.md       # Technical architecture
└── STYLE-GUIDE.md        # Content style guide
```

### Backup Protocols

1. **Automated Backups**
   - GitHub Actions weekly backup to multiple repositories
   - Export to static JSON archive

2. **Multiple Mirrors**
   - Primary: `username.github.io/idea-repo`
   - Mirror: `gitlab.com/username/idea-repo`
   - Archive: `archive.org/details/idea-repo`

3. **Static Export**
   ```bash
   # Generate static HTML archive
   jekyll build
   zip -r idea-repo-archive.zip _site/
   ```

### Community Maintenance

- **CODEOWNERS** file for automatic review assignment
- **Issue templates** for different contribution types
- **Good first issue** labels for newcomers
- **Monthly digest** of new contributions

---

## 5. Security & Moderation

### GitHub-Based Moderation

```yaml
# .github/settings.yml (using GitHub Settings app)
repository:
  # Only allow specific file types
  allowed_file_extensions: ['.md', '.json', '.yml', '.yaml']
  
  # Block common spam patterns
  blocked_patterns:
    - 'http://bit\.ly'
    - 'viagra|casino'
```

### Content Guidelines

**CONTRIBUTING.md excerpt:**
```markdown
## Content Policy

✅ **Allowed:**
- Original mathematical content
- Study notes and explanations
- Constructive discussions
- Proper citations

❌ **Not Allowed:**
- Plagiarized content
- Spam or advertising
- Inappropriate language
- Off-topic content
```

### Automated Checks

```yaml
# .github/workflows/moderation.yml
name: Content Moderation
on: [pull_request]

jobs:
  check:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Check for spam
        run: |
          # Simple spam detection
          if grep -rE "(viagra|casino|bit\.ly)" _posts/; then
            echo "Potential spam detected"
            exit 1
          fi
```

---

## 6. Deployment Workflow

### Step 1: Repository Setup

```bash
# 1. Create repository on GitHub
# 2. Clone locally
git clone https://github.com/username/idea-repository.git
cd idea-repository

# 3. Create basic structure
mkdir -p _posts _data _layouts _includes ideas
```

### Step 2: Enable GitHub Pages

1. Go to **Settings > Pages**
2. Select **Source**: `main` branch, `/ (root)`
3. Choose **Theme**: Minimal Mistakes or custom

### Step 3: Configure Jekyll

```yaml
# _config.yml
title: Open Idea Repository
description: A collaborative knowledge library
baseurl: "/idea-repository"
url: "https://username.github.io"

# MathJax configuration
markdown: kramdown
kramdown:
  math_engine: mathjax
  input: GFM
  hard_wrap: false

# Plugins
plugins:
  - jekyll-feed
  - jekyll-sitemap
  - jekyll-seo-tag
```

### Step 4: Create GitHub Actions

```yaml
# .github/workflows/deploy.yml
name: Deploy to GitHub Pages
on:
  push:
    branches: [main]
  workflow_dispatch:

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Ruby
        uses: ruby/setup-ruby@v1
        with:
          bundler-cache: true
      
      - name: Build and deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./_site
```

### Step 5: Add Issue Templates

```markdown
<!-- .github/ISSUE_TEMPLATE/submission.md -->
---
name: New Idea Submission
about: Submit a new idea, note, or theory
title: '[SUBMISSION] '
labels: submission, pending-review
---

**Title:** 

**Category:** (theories/notes/ideas)

**Content (Markdown):**

**Tags:**
```

---

## File Structure Summary

```
idea-repository/
├── _config.yml              # Jekyll configuration
├── _layouts/
│   ├── default.html         # Main layout with MathJax
│   └── post.html            # Post layout
├── _includes/
│   ├── header.html
│   ├── footer.html
│   └── mathjax.html
├── _posts/                  # Published content
├── _data/                   # JSON data files
├── ideas/
│   ├── _submissions/        # Pending submissions
│   └── template.md          # Submission template
├── assets/
│   ├── css/
│   └── js/
├── .github/
│   ├── workflows/
│   │   ├── deploy.yml
│   │   └── moderation.yml
│   └── ISSUE_TEMPLATE/
├── docs/
│   ├── CONTRIBUTING.md
│   └── MAINTAINING.md
├── index.html
├── README.md
└── CNAME                    # Custom domain (optional)
```

---

## Best Practices

1. **Keep it simple** - Avoid complex dependencies
2. **Document everything** - Assume future maintainers know nothing
3. **Use semantic versioning** for major changes
4. **Regular backups** - Monthly archive exports
5. **Community first** - Make contribution as easy as possible
6. **Test locally** - Provide Docker setup for testing

---

## Quick Start Commands

```bash
# Local development
bundle install
bundle exec jekyll serve

# Create new post
cp ideas/template.md _posts/$(date +%Y-%m-%d)-my-idea.md

# Test build
bundle exec jekyll build
```

---

## Next Steps

1. [ ] Choose between Jekyll or pure HTML approach
2. [ ] Set up basic repository structure
3. [ ] Configure MathJax rendering
4. [ ] Create submission workflow
5. [ ] Write documentation
6. [ ] Test deployment