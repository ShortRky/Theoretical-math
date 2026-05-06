# Contributing to Open Idea Repository

Thank you for your interest in contributing! This document provides guidelines and instructions for contributing to this open-source knowledge library.

## How to Contribute

### Option 1: Submit via Pull Request (Recommended)

1. Fork the repository
2. Create a new file in `_posts/` with the format `YYYY-MM-DD-title.md`
3. Use the [submission template](ideas/_submissions/template.md) as a guide
4. Commit your changes
5. Open a pull request

### Option 2: Submit via GitHub Issue

1. Go to the [Issues](https://github.com/username/idea-repository/issues) tab
2. Click "New Issue"
3. Select "New Idea Submission"
4. Fill out the form
5. Submit the issue

## Content Guidelines

### What to Submit

✅ **Allowed:**
- Original mathematical content and theories
- Study notes and educational materials
- Constructive ideas and concepts
- Proper citations and references
- Clear, well-formatted Markdown

❌ **Not Allowed:**
- Plagiarized content
- Spam or advertising
- Inappropriate language
- Off-topic content
- Copyrighted material without permission

### Writing Style

- Use clear, concise language
- Include relevant tags for discoverability
- Format equations using LaTeX syntax
- Cite sources when referencing others' work
- Keep paragraphs short and readable

## Markdown and LaTeX

### Basic Markdown

```markdown
# Heading 1
## Heading 2
### Heading 3

**Bold text**
*Italic text*

- List item 1
- List item 2

[Link text](https://example.com)
```

### LaTeX Equations

Inline equations: `$E = mc^2$`

Display equations:
```latex
$$
\int_{-\infty}^{\infty} e^{-x^2} dx = \sqrt{\pi}
$$
```

## Front Matter Template

```yaml
---
title: "Your Title Here"
author: "Your GitHub Username"
date: 2024-01-15
tags: [tag1, tag2, tag3]
category: ideas
---
```

## Development Setup

1. Install Ruby and Bundler
2. Run `bundle install`
3. Run `bundle exec jekyll serve`
4. Open `http://localhost:4000`

## Code of Conduct

Be respectful and constructive. We're building a community-driven knowledge library for everyone.

## Questions?

Open an issue with the "question" label and we'll help you out!