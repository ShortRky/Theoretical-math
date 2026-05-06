# Open Idea Repository

A public, open-source knowledge library for mathematical theories, study notes, and original ideas. Built with Jekyll and hosted on GitHub Pages.

![MathJax](https://img.shields.io/badge/MathJax-3.0-blue)
![Jekyll](https://img.shields.io/badge/Jekyll-4.0-red)
![License](https://img.shields.io/badge/License-MIT-green)

## Features

- 📚 **Collaborative Knowledge Library** - Store, organize, and share ideas
- 🔢 **MathJax Support** - Full LaTeX equation rendering
- 🌐 **GitHub Pages** - Free, reliable hosting
- 🤝 **Community Driven** - Anyone can contribute via pull requests
- 📱 **Responsive Design** - Works on all devices

## Quick Start

### View the Site

Visit: `https://username.github.io/idea-repository`

### Contribute

1. Fork the repository
2. Copy `ideas/_submissions/template.md`
3. Create a new file in `_posts/` with your content
4. Submit a pull request

See [CONTRIBUTING.md](CONTRIBUTING.md) for details.

## Writing Content

### Markdown with LaTeX

```markdown
# My Theory

This is an inline equation: $E = mc^2$

This is a display equation:
$$
\int_{-\infty}^{\infty} e^{-x^2} dx = \sqrt{\pi}
$$
```

### Front Matter

```yaml
---
title: "Your Title"
author: "Your Name"
date: 2024-01-15
tags: [math, theory]
category: ideas
---
```

## Development

```bash
# Install dependencies
bundle install

# Run locally
bundle exec jekyll serve

# Build for production
bundle exec jekyll build
```

## Project Structure

```
/
├── _config.yml           # Configuration
├── _layouts/             # Templates
├── _posts/               # Content
├── _data/                # Data files
├── ideas/                # Submission system
├── .github/              # Workflows
└── assets/               # Static files
```

## License

MIT License - See [LICENSE](LICENSE) for details.

## Maintainers

- [Your Name](https://github.com/username)

## Acknowledgments

- Built with [Jekyll](https://jekyllrb.com/)
- Hosted on [GitHub Pages](https://pages.github.com/)
- Math rendering by [MathJax](https://www.mathjax.org/)