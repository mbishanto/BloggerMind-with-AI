# Contributing

Contributions to Blogger Mind are welcome. Since this is a personal project built with AI assistance, the codebase may not follow standard framework conventions. The guidelines below explain how to contribute effectively.

---

## How to Contribute

### Reporting Bugs

Open a [GitHub issue](https://github.com/mbishanto/BloggerMind-with-AI/issues) with:

- A clear, descriptive title.
- Steps to reproduce the bug.
- Expected vs. actual behavior.
- Screenshots if applicable.
- Browser, PHP version, and hosting environment details.

### Suggesting Features

Open a [GitHub issue](https://github.com/mbishanto/BloggerMind-with-AI/issues) with:

- A description of the feature and the problem it solves.
- Any implementation ideas you have.
- Whether you are willing to help implement it.

### Submitting Code Changes

1. Fork the repository on GitHub.
2. Create a feature branch: `git checkout -b feature/your-feature-name`.
3. Make your changes following the guidelines below.
4. Test your changes thoroughly.
5. Commit with a clear message describing the change.
6. Push to your fork and open a pull request.

---

## Guidelines

### Code Style

- Follow the existing patterns in the codebase. The code uses plain PHP without a framework.
- Use descriptive variable and function names.
- Use PDO prepared statements for all database queries.
- Include CSRF protection on any form that modifies data.
- Use `htmlspecialchars()` with `ENT_QUOTES | ENT_SUBSTITUTE | ENT_HTML5` for output escaping.

### File Organization

- Add new features as independent PHP files in the appropriate directory.
- Place shared logic in the `lib/` directory.
- Place API endpoints in the `api/` directory.
- Place reusable template partials in the `partials/` directory.

### Testing

Test all changes manually:

- Functional testing: does the feature work as expected?
- Edge cases: empty inputs, long strings, special characters.
- Security: CSRF tokens, input validation, prepared statements.
- Cross-browser: Chrome, Firefox, Safari, Edge.
- Responsive: desktop, tablet, mobile viewports.

### Security

- Do not commit API keys or database credentials.
- Use PDO prepared statements for all database queries.
- Include CSRF tokens on all forms.
- Validate and sanitize all user inputs.
- Use `password_hash()` for password storage.

---

## Questions

If you have questions about contributing, open a GitHub issue or reach out through the contact information in the README.
