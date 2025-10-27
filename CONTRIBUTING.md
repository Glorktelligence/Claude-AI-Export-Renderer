# Contributing to Claude AI Export Renderer

Thank you for your interest in contributing to Claude AI Export Renderer! This document provides guidelines and instructions for contributing to the project.

## Code of Conduct

This project adheres to a [Code of Conduct](CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code. Please report unacceptable behavior via GitHub issues.

## How Can I Contribute?

### Reporting Bugs

Before creating bug reports, please check existing issues to avoid duplicates. When creating a bug report, include as many details as possible:

- **Use a clear and descriptive title**
- **Describe the exact steps to reproduce the problem**
- **Provide specific examples** (sample export files if possible)
- **Describe the behavior you observed and what you expected**
- **Include screenshots** if relevant
- **Specify your browser and version**
- **Note the file size** of the export you're testing with

### Suggesting Enhancements

Enhancement suggestions are tracked as GitHub issues. When creating an enhancement suggestion:

- **Use a clear and descriptive title**
- **Provide a detailed description** of the suggested enhancement
- **Explain why this enhancement would be useful** to most users
- **List any similar features** in other applications if applicable

### Pull Requests

1. **Fork the repository** and create your branch from `main`
2. **Make your changes** following the project guidelines below
3. **Test thoroughly** with various export files and browsers
4. **Update documentation** if you've changed functionality
5. **Ensure your code follows** the existing style
6. **Submit a pull request** with a clear description

## Development Guidelines

### Project Architecture

This is a **single-file application** (`claude-export-renderer.html`) with no build process or dependencies. All changes must maintain this architecture:

- All HTML, CSS, and JavaScript in one file
- No external dependencies or CDN resources
- No build tools or compilation steps
- Must work by simply opening the HTML file in a browser

See [CLAUDE.md](CLAUDE.md) for detailed architecture documentation.

### Testing Your Changes

1. **Browser Testing**: Test in Chrome, Firefox, Safari, and Edge
2. **File Size Testing**: Test with small (<100), medium (100-500), and large (500+) conversation exports
3. **Format Testing**: Test with different export format variations
4. **Feature Testing**: Verify search, filters, pagination, and language switching all work
5. **Console Check**: Open browser DevTools (F12) and ensure no JavaScript errors

### Code Style

- **JavaScript**: Use modern ES6+ syntax, clear variable names, JSDoc comments for functions
- **CSS**: Follow existing naming conventions, keep styles in the `<style>` section
- **HTML**: Maintain semantic structure, use data attributes for i18n
- **Indentation**: Use 2 spaces (not tabs)

### Privacy & Security Requirements

**Critical**: All contributions must maintain these principles:

- ✅ All processing happens locally in the browser
- ❌ No data sent to external servers
- ❌ No external resource loading (CDNs, fonts, scripts)
- ❌ No analytics or tracking
- ❌ No internet connection required

### Adding New Features

When adding features, consider:

1. **Performance**: Will this work with 32MB+ files?
2. **Compatibility**: Does this work in all major browsers?
3. **Privacy**: Does this maintain our local-only processing?
4. **Usability**: Is this intuitive for non-technical users?
5. **Internationalization**: Have you added translations for all supported languages?

### Adding New Languages

To add a new language:

1. Add translation object to `translations` constant (~line 609)
2. Add `<option>` to language selector (~line 500)
3. Ensure all UI strings have corresponding translation keys
4. Test auto-detection and manual switching

Translation keys should be in English and descriptive (e.g., `"searchPlaceholder"`, `"filterByDate"`).

## Versioning

This project uses semantic versioning (MAJOR.MINOR.PATCH):

- **MAJOR**: Breaking changes or significant feature additions
- **MINOR**: New features, backward-compatible
- **PATCH**: Bug fixes, minor improvements

Update `VERSION` file and add entry to `CHANGELOG.md` for all releases.

## Documentation

When making changes that affect functionality:

- Update [README.md](README.md) for user-facing changes
- Update [CLAUDE.md](CLAUDE.md) for architecture/development changes
- Update [CHANGELOG.md](CHANGELOG.md) with a clear description
- Add code comments for complex logic

## Questions?

If you have questions about contributing:

- Check [CLAUDE.md](CLAUDE.md) for detailed technical documentation
- Review existing issues and pull requests
- Open a new issue with the question label

## License

By contributing, you agree that your contributions will be licensed under the same [MIT License](LICENSE) that covers the project.

---

Thank you for contributing to Claude AI Export Renderer!
