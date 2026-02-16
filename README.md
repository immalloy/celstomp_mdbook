> [!CAUTION]
> **Deprecated / Unmaintained:** This project is no longer maintained and may be broken.

# Celstomp Documentation

This is the comprehensive documentation site for Celstomp, a free browser-based 2D animation tool.

## About This Documentation

This documentation is built with [mdBook](https://rust-lang.github.io/mdBook/), a command line tool to create books with Markdown.

## Quick Links

- [Live Documentation](https://ginyoa.github.io/celstomp-docs) (when deployed)
- [Celstomp App](https://ginyo.space/celstomp/)
- [GitHub Repository](https://github.com/ginyoa/celstomp_v1)

## Local Development

### Prerequisites

- [mdBook](https://rust-lang.github.io/mdBook/guide/installation.html) installed
- Git (optional, for version control)

### Setup

1. Clone this repository:
```bash
git clone <repository-url>
cd celstomp_mdbook
```

2. Serve the documentation locally:
```bash
mdbook serve
```

3. Open your browser to `http://localhost:3000`

### Building

To build the static site:

```bash
mdbook build
```

Output will be in the `book/` directory.

## Contributing to Documentation

We welcome contributions! Here's how:

### Reporting Issues

- Typos or errors: Open an issue
- Missing content: Suggest additions
- Outdated information: Let us know

### Submitting Changes

1. Fork the repository
2. Make your changes in the `src/` directory
3. Test locally with `mdbook serve`
4. Submit a pull request

### Style Guide

- Use clear, concise language
- Include examples where helpful
- Test all code snippets
- Add screenshots for UI features
- Follow existing structure

## Documentation Structure

```
src/
├── introduction.md          # Welcome page
├── SUMMARY.md              # Navigation structure
├── custom.css              # Styling
│
├── installation.md         # Getting Started
├── quickstart.md
├── requirements.md
│
├── concepts/               # Core Concepts
│   ├── overview.md
│   ├── canvas.md
│   ├── timeline.md
│   ├── layers.md
│   ├── onion-skinning.md
│   └── tools-overview.md
│
├── guides/                 # User Guides
│   ├── drawing-tools.md
│   ├── selection-tools.md
│   ├── color-palette.md
│   ├── animation-workflow.md
│   ├── export-formats.md
│   ├── shortcuts.md
│   └── tutorial.md
│
├── development/            # Development
│   ├── architecture.md
│   ├── project-structure.md
│   ├── code-organization.md
│   ├── building.md
│   └── contributing.md
│
├── reference/              # Reference
│   ├── api-overview.md
│   ├── file-formats.md
│   ├── configuration.md
│   ├── faq.md
│   └── troubleshooting.md
│
└── community/              # Community
    ├── contributors.md
    ├── code-of-conduct.md
    ├── security.md
    └── license.md
```

## Deployment

### GitHub Pages

1. Build: `mdbook build`
2. Copy `book/` contents to `docs/` folder
3. Push to repository
4. Enable GitHub Pages in settings

### Other Hosts

Upload the `book/` directory to any static hosting:
- Netlify
- Vercel
- Surge.sh
- Any web server

## License

This documentation is licensed under the same GPL v3 license as Celstomp.

## Contact

- Issues: [GitHub Issues](https://github.com/ginyoa/celstomp_v1/issues)
- Discussions: [GitHub Discussions](https://github.com/ginyoa/celstomp_v1/discussions)

---

Built with love by the Celstomp community.
