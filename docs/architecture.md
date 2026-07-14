# Architecture

Blogger Mind follows a traditional PHP architecture. Each page is an independent PHP entry point that includes shared libraries for database access, authentication, CSRF protection, and AI integration.

---

## Request Flow

```
Browser Request
      │
      ▼
  .htaccess (Apache rewrite rules)
      │
      ▼
  PHP Entry Point (index.php, dashboard.php, login.php, etc.)
      │
      ├──▶ config.php
      │     ├── Database credentials
      │     ├── AI API keys
      │     ├── Site settings
      │     └── Session initialization
      │
      ├──▶ lib/db.php
      │     └── PDO connection singleton
      │
      ├──▶ lib/auth.php
      │     ├── Authentication checks
      │     ├── Rate limiting
      │     └── OTP verification
      │
      ├──▶ lib/csrf.php
      │     ├── CSRF token generation
      │     └── Token validation
      │
      ├──▶ Business Logic
      │     ├── Input validation
      │     ├── Permission checks
      │     ├── Database queries (PDO prepared statements)
      │     └── Data processing
      │
      ├──▶ API Services (when applicable)
      │     ├── AI providers (Groq / OpenRouter / Gemini)
      │     └── SerpAPI web search
      │
      └──▶ Frontend Rendering
            ├── Include partials/header.php
            ├── Render page content
            ├── Include partials/footer.php
            └── JavaScript enhancement (Ajax, TinyMCE, infinite scroll)
```

---

## Module Layout

```
                    ┌──────────────────────┐
                    │    Client Browser     │
                    │  (HTML, CSS, JS)      │
                    └──────────┬───────────┘
                               │ HTTP
                               ▼
                    ┌──────────────────────┐
                    │   PHP Entry Points    │
                    │  (Page-specific .php) │
                    └──────────┬───────────┘
                               │
                    ┌──────────┴───────────┐
                    │   Library Layer       │
                    │  lib/db.php           │
                    │  lib/auth.php         │
                    │  lib/csrf.php         │
                    │  lib/util.php         │
                    │  lib/ai_common.php    │
                    └──────────┬───────────┘
                               │
                    ┌──────────┴───────────┐
                    │   Data Layer          │
                    │  MySQL Database       │
                    │  File System (uploads)│
                    └──────────┬───────────┘
                               │
                    ┌──────────┴───────────┐
                    │   External APIs       │
                    │  Groq / OpenRouter    │
                    │  Gemini / SerpAPI     │
                    └──────────────────────┘
```

---

## Database Schema (Key Tables)

| Table | Purpose |
|---|---|
| `users` | User accounts (email, password_hash, username, display_name, avatar, bio, role) |
| `pending_users` | Unverified registrations awaiting email confirmation |
| `posts` | Blog posts (title, slug, content, image, category_id, status, user_id, timestamps) |
| `categories` | Content categories (name, slug) |
| `likes` | Post likes (user_id, post_id) |
| `comments` | Post comments (post_id, user_id, content, parent_id) |
| `news_items` | Aggregated news headlines (title, url, source_id, image_url, published_at) |
| `news_sources` | News source configuration (name, url) |
| `contact_messages` | Contact form submissions (name, email, message, ip_address, user_agent) |
| `login_attempts` | Login attempt logging (email, ip_address, timestamp, success) |
| `login_otp` | OTP codes for login (email, otp, expires_at, used) |
| `password_resets` | Password reset OTPs (email, otp, expires_at, used) |
| `post_status_logs` | Post edit history (post_id, user_id, old_status, new_status, reason) |
| `bm_ai_messages` | AI chat history (session_id, role, message, created_at) |
| `sessions` | PHP session storage (id, user_id, token, ip, user_agent, expires_at) |

---

## Key Design Decisions

| Decision | Rationale |
|---|---|
| **Traditional PHP** | No framework dependencies. Works on any hosting that supports PHP. |
| **PDO + Prepared Statements** | SQL injection prevention without ORM complexity. |
| **Multi-Provider AI** | Redundancy — if one provider is unavailable or rate-limited, others serve as fallback. |
| **Key Rotation** | Up to 5 API keys per provider distributed via round-robin to handle rate limits. |
| **Client-Side Tools** | Utility tools run entirely in the browser — no server processing, no database load. |
| **cPanel Deployment** | Demonstrates that AI-assisted PHP applications work on standard shared hosting. |
| **Infinite Scroll via API** | Feed data is loaded as JSON from `api/feed.php` rather than rendered server-side. |
| **OTP-Based Auth** | Two-step login adds a layer of security beyond password-only authentication. |
