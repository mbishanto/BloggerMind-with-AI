# Technology Stack

Blogger Mind uses a minimal, hosting-compatible stack. No frameworks, no build tools, no containerization.

---

## Stack Table

| Category | Technology | Role |
|---|---|---|
| Backend Language | PHP | Application logic, page rendering, database access |
| Database | MySQL | Data storage, content retrieval, user management |
| Markup | HTML5 | Page structure |
| Styling | CSS3 | Layout and responsive design |
| Frontend Scripting | JavaScript (ES6+) | Interactivity, Ajax calls, DOM manipulation |
| Rich Text Editor | TinyMCE 6 | WYSIWYG content editing |
| Primary AI Provider | Groq API | Fast inference for AI chat and writing assistance |
| Secondary AI Provider | OpenRouter API | Multi-model fallback for AI features |
| Tertiary AI Provider | Gemini API | Google AI model integration |
| Web Search API | SerpAPI | Web search for AI research queries |
| Web Server | Apache | HTTP serving with `mod_rewrite` |
| Hosting | cPanel Shared Hosting | Production deployment environment |
| API Style | REST (JSON) | Ajax endpoints for feed, AI, likes, uploads |

---

## Detailed Breakdown

### PHP

- **No framework** — application is built with plain PHP files.
- **PDO** for all database access with prepared statements.
- **`password_hash()` / `password_verify()`** for bcrypt password hashing.
- **Sessions** with secure cookie configuration (HttpOnly, SameSite, Secure).
- **`declare(strict_types=1)`** used in library modules.

### MySQL

- **InnoDB** storage engine for transaction support and foreign keys.
- **Full-text indexes** on searchable content columns.
- **Prepared statements** exclusively — no raw SQL interpolation.

### JavaScript

- **Vanilla JS** — no framework (no jQuery, no React, no Vue).
- **Fetch API** for Ajax requests to API endpoints.
- **`window.crypto.getRandomValues()`** for cryptographically secure password generation.
- **`navigator.share()`** for native post sharing with clipboard fallback.

### TinyMCE 6

- **Self-hosted** (GPL license) — not loaded from a CDN.
- **Custom image upload handler** with CSRF protection.
- **Full toolbar** — formatting, headings, lists, links, tables, source code view.

### AI Providers

| Provider | Model | Use Case |
|---|---|---|
| Groq | `llama-3.1-8b-instant` | Primary — fast inference |
| OpenRouter | `meta-llama/llama-3.2-3b-instruct:free` | Fallback — free tier |
| Gemini | `gemini-2.0-flash` | Tertiary — Google model |

**Key rotation:** Up to 5 API keys per provider, distributed via round-robin to manage rate limits.

### SerpAPI

- **Google search engine** integration.
- **Round-robin key rotation** across multiple API keys.
- Used for web search context in AI assistant responses.

### cPanel Shared Hosting

- **File management:** cPanel File Manager or FTP.
- **Database:** phpMyAdmin for MySQL management.
- **Cron Jobs:** cPanel Cron Job interface for scheduled tasks.
- **SSL:** AutoSSL via Let's Encrypt.

---

## What Is Not Used

| Technology | Reason Not Used |
|---|---|
| Docker / Containers | Shared hosting does not support Docker. |
| Node.js | PHP handles all server-side logic. |
| React / Vue / Angular | Vanilla JS is sufficient for the level of interactivity required. |
| Composer / npm | No external PHP or JS dependencies beyond TinyMCE. |
| Redis / Memcached | Not available on standard shared hosting. |
| PostgreSQL | MySQL is universally available on cPanel hosting. |
