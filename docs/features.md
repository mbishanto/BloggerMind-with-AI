# Features

This page lists only features that are currently implemented and confirmed in the codebase. Planned features are noted separately at the bottom.

---

## Current Features

### Authentication

| Feature | Details |
|---|---|
| Registration | Email-based signup with email verification (token sent via email). Honeypot anti-bot field, uniqueness checks on email and username. |
| Login | Email + password with 6-digit OTP verification. Rate-limited (10 attempts per 10 min per IP). Brute-force admin notification. |
| Password Reset | Email-based OTP (6-digit, 15 min expiry). Anti-user-enumeration messaging. |
| Session Management | HttpOnly, SameSite=Lax, Secure cookies. 30-day session lifetime. |

### Profile Management

- **Username:** Change with Ajax live availability check.
- **Display Name:** Editable.
- **Bio:** Up to 2000 characters.
- **Avatar:** Upload JPG/PNG/WEBP, max 2MB, min 96x96. MIME type verification via `finfo`. Avatar removal option.
- **Password Change:** With client-side strength meter.

### Content Management

| Feature | Details |
|---|---|
| Post Creation | TinyMCE 6 rich text editor (self-hosted, GPL). Title, content, image URL, category assignment. |
| Post Editing | Only owner or admin can edit. Change log required (reason stored in `post_status_logs`). |
| Post Deletion | Owner or admin with authorization check. |
| Post Statuses | Published, hidden, deleted. |
| Categories | Select existing categories or create new ones inline. |
| Image Upload | Custom handler with CSRF protection and file validation. |

### Community Features

| Feature | Details |
|---|---|
| Homepage Feed | Infinite scroll pagination via `api/feed.php`. Category filter and search bar. |
| Like System | Ajax toggle. "Most Liked" sidebar widget (top 5). |
| Top Authors | Leaderboard widget by post count (top 5). |
| Trending Posts | Latest posts widget sorted by creation date. |
| Post Sharing | Native `navigator.share()` API with clipboard fallback for unsupported browsers. |
| Latest Headlines | News aggregation widget from `news_items` and `news_sources` tables. |

### AI Integration

| Feature | Details |
|---|---|
| AI Assistant Chat | Four modes: Chat, SEO Writer, Code Fixer, Tool Guide. |
| Multi-Provider | Groq (primary, `llama-3.1-8b-instant`), OpenRouter (fallback, `meta-llama/llama-3.2-3b-instruct:free`), Gemini (tertiary, `gemini-2.0-flash`). |
| Key Rotation | Up to 5 API keys per provider with round-robin rotation for rate limit handling. |
| Chat History | Last 90 messages stored per session in `bm_ai_messages` table. |
| Global Widget | Floating chat bubble available on all pages for logged-in users. |
| Web Search Integration | SerpAPI with round-robin key rotation for research queries. |
| Temperature Control | Configurable (default 0.4). Max tokens: 700. Character limit: 800. |
| Empty State | Hint pills with example prompts for new conversations. |

### Client-Side Tools

All tools below run entirely in the browser with no server-side processing:

| Tool | Description |
|---|---|
| **Password Generator** | Crypto-random passwords using `window.crypto.getRandomValues()`. Adjustable length (4-99 slider, 4-128 number input), character set toggles (uppercase, lowercase, numbers, symbols), exclude similar characters, start with letter, avoid repeats. Entropy-based strength meter with crack-time estimation (10^10 guesses/sec). Bulk generate 10 passwords with download as .txt. History list (max 12). |
| **Duplicate Line Remover** | Three operation modes: standard dedupe, keep only unique, consecutive only. Keep first/last occurrence. Case-insensitive or sensitive. Trim whitespace, remove empty lines, normalize spaces. Sort options: none, A-Z, Z-A, ASCII, numeric. Output format: no change, lowercase, UPPERCASE, Title Case, Sentence case. Export as TXT, CSV, JSON. Real-time stats. LocalStorage auto-save. Restore removed lines. |
| **Word Counter** | Count words, characters, sentences, paragraphs. |
| **BMI Calculator** | Body Mass Index calculation with category display. |
| **Age Calculator** | Calculate age from date of birth. |
| **Basic Calculator** | Standard arithmetic operations. |
| **Scientific Calculator** | Advanced mathematical functions. |
| **Accounting Calculator** | Business and accounting calculations. |
| **EMI Calculator** | Loan EMI calculation. |
| **Loan Interest Calculator** | Interest and payment schedule. |
| **Case Converter** | Text case transformation. |
| **Lorem Ipsum Generator** | Generate placeholder text. |
| **Text Repeater** | Repeat text with configurable count. |
| **JSON Formatter** | Format, validate, and prettify JSON. |
| **Code Minifier** | Minify JavaScript and CSS. |
| **Base64 Encoder/Decoder** | Encode and decode Base64 strings. |
| **Image Compressor** | Client-side image compression. |
| **Image Resizer** | Resize images in the browser. |
| **Image to Base64** | Convert images to Base64 strings. |
| **Color Generator** | Generate random colors with hex/rgb/hsl display. |
| **Name Generator** | Random name generation. |
| **Number Generator** | Random number generation. |
| **Password Generator (standalone)** | Also listed as a dedicated tool page. |
| **URL Slug Generator** | Generate SEO-friendly URL slugs. |
| **Meta Tag Generator** | Generate HTML meta tags. |
| **Readability Score** | Assess text readability. |
| **OG Image Preview** | Preview Open Graph image rendering. |

### Contact & Support

| Feature | Details |
|---|---|
| Contact Form | Name, email, message. Anti-spam: honeypot, timing threshold (3s min), URL counting, bad word filter, IP rate limiting (3 per 10 min). |
| Support Pages | Support center, help center, report abuse, appeals and account recovery. |

### Security

| Measure | Details |
|---|---|
| CSRF Protection | Token validation via `lib/csrf.php` on all forms. |
| SQL Injection Prevention | PDO prepared statements exclusively. |
| XSS Prevention | `htmlspecialchars()` with `ENT_QUOTES \| ENT_SUBSTITUTE \| ENT_HTML5`. |
| Password Hashing | `password_hash()` with `PASSWORD_DEFAULT` (bcrypt). |
| Rate Limiting | Login: 10 attempts per 10 min per IP. Contact: 3 per 10 min per IP. |
| Login Logging | All attempts logged to `login_attempts` table. |
| Anti-Spam | Honeypot, timing, URL count, bad word filter. |
| File Upload Security | MIME type via `finfo`, extension whitelist, size limits (2MB), unique filenames. |

---

## Planned Features

The following features are not yet implemented but are under consideration for future development:

| Feature | Notes |
|---|---|
| AI Research Assistant | Automated topic research and content outline generation. |
| AI Image Generation | DALL-E or Stable Diffusion integration for featured images. |
| Scheduled Publishing | Cron-based post scheduling. |
| Analytics Dashboard | Post performance metrics and visualizations. |
| Plugin System | Extensible architecture for third-party plugins. |
| Public REST API | Full CRUD API for external integrations. |
| Mobile Application | React Native or Flutter app. |
| Multi-Language Support | i18n framework integration. |
| Notification System | In-app and email notifications for comments, follows, etc. |
