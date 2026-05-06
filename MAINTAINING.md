# Maintainer Guide

This document provides guidance for maintaining the Open Idea Repository.

## Repository Structure

```
/
├── _config.yml           # Jekyll configuration
├── _layouts/             # Page templates
├── _posts/               # Published content
├── _data/                # JSON data files
├── ideas/                # Submission system
├── .github/              # GitHub workflows and templates
├── assets/               # CSS, JS, images
└── docs/                 # Documentation
```

## Review Process

### Pull Request Review

1. Check for spam or inappropriate content
2. Verify front matter is complete
3. Ensure content follows guidelines
4. Verify MathJax equations render correctly
5. Merge or request changes

### Issue Review

1. Convert valid submissions to markdown files
2. Assign appropriate tags and categories
3. Close the issue with a link to the new content

## Backup Procedures

### Monthly Archive

```bash
# Generate static archive
jekyll build
zip -r idea-repository-$(date +%Y%m).zip _site/
```

### Mirror Repository

- Create mirrors on GitLab and other platforms
- Use GitHub Actions to sync changes

## Community Management

### Adding Maintainers

1. Add to CODEOWNERS file
2. Grant write access to repository
3. Share this documentation

### Handling Disputes

- Use GitHub's blocking/reporting features
- Document decisions in issue comments
- Maintain transparency in all actions

## Technical Updates

### Updating Dependencies

```bash
bundle update
```

### Testing Changes

```bash
bundle exec jekyll serve
# Visit http://localhost:4000
```

## Long-term Sustainability

### Succession Planning

- Document all processes
- Train multiple maintainers
- Create a maintainer guide
- Establish clear handoff procedures

### Archiving

If the project becomes unmaintained:
1. Add ARCHIVED.md to root
2. Update README with status
3. Point to mirrors/archives