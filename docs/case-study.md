# Case Study: Blogger Mind

---

## Voice Card

> *Building practical AI that solves real problems.*

---

## Problem

I wanted to build a community blogging platform with modern features — AI-assisted writing, rich media editing, user authentication, and utility tools — but I did not come from a traditional software engineering background. Writing every line of code from scratch was not feasible.

Existing solutions were either too complex (WordPress with plugins), required cloud infrastructure (Ghost, Contentful), or did not include AI features. I needed a different approach: one where I could guide the development process while AI handled much of the implementation work.

## Goals

- Build a working, deployable community blogging platform.
- Integrate AI writing assistance using available APIs.
- Implement secure user authentication with email verification and OTP login.
- Deploy on standard cPanel shared hosting (no Docker, no cloud).
- Keep the codebase modular and maintainable.

## Approach

The project was broken into independent modules, each developed through the same AI-assisted workflow:

1. **Define** the feature requirements and acceptance criteria.
2. **Design** the database schema and module boundaries.
3. **Prompt** AI with detailed specifications.
4. **Review** the generated code for correctness and security.
5. **Test** manually across browsers and edge cases.
6. **Debug** and refine until the feature works correctly.
7. **Integrate** into the codebase.
8. **Deploy** to production.

### Module Breakdown

| Module | Files | Description |
|---|---|---|
| Authentication | `register.php`, `login.php`, `verify-login.php`, `forgot-password.php`, `lib/auth.php` | Registration with email verification, login with OTP, password reset, rate limiting. |
| Profile Management | `edit-profile.php` | Ajax-driven profile editing with avatar upload. |
| Content Management | `dashboard.php`, `edit-post.php`, `index.php`, `api/feed.php` | Post CRUD with TinyMCE editor, categories, infinite scroll feed. |
| Community | `like_toggle.php`, various widgets | Like system, author leaderboard, trending posts, sharing. |
| AI Integration | `bm-ai-assistant.php`, `ai-assistant.php`, `lib/ai_common.php` | Multi-provider AI chat with four modes, chat history, web search. |
| Utility Tools | `password-generator.php`, `remove-duplicate-lines.php`, `tools/` directory | Client-side tools with no server processing. |
| Contact & Support | `contact.php`, `support-bloggermind/` | Contact form with anti-spam, support pages. |

## Architecture Decisions

| Decision | Why |
|---|---|
| **No framework** | Zero dependencies. Full control. Works on any PHP hosting. |
| **PDO prepared statements** | Eliminates SQL injection without an ORM. |
| **Multi-provider AI** | Redundancy — if one provider is unavailable or rate-limited, others serve as fallback. |
| **Key rotation** | Up to 5 API keys per provider to handle rate limits without service interruption. |
| **Client-side tools** | Reduce server load. Tools work even under high traffic. |
| **OTP login** | Two-step authentication adds security beyond passwords. |

## Challenges

| Challenge | Resolution |
|---|---|
| **API rate limits** | Implemented round-robin rotation across 5 keys per provider. |
| **AI response quality** | Experimented with prompts, temperature settings, and model selection across three providers. |
| **Shared hosting constraints** | Kept all processes stateless. Client-side tools eliminate server processing for utility features. |
| **Image upload security** | Built custom upload handler with MIME type verification, extension whitelist, and CSRF protection. |
| **OTP delivery** | Implemented email-based OTP with 10-minute expiry and single-use enforcement. |
| **Brute force protection** | Rate limiting with per-IP tracking and admin notification on detection. |

## Testing

Every feature was tested manually:

- **Functional testing:** Does the feature do what it is supposed to do?
- **Edge cases:** Empty inputs, long strings, special characters, rapid form submissions.
- **Security:** CSRF token validation, SQL injection attempts, XSS vectors, file upload exploits.
- **Cross-browser:** Chrome, Firefox, Safari, Edge.
- **Responsive:** Desktop, tablet, and mobile viewports.
- **Production:** Full test suite after cPanel deployment.

### Issues Found and Fixed During Testing

- Missing input validation on edge cases (empty fields, very long strings).
- Incorrect database queries that worked in development but failed with real data.
- CSS layout issues on specific browser/device combinations.
- JavaScript errors from undefined variables in certain states.
- Session handling edge cases with expired or invalid sessions.

## Deployment

Deployment used cPanel's native tools:

1. Uploaded files via cPanel File Manager.
2. Created MySQL database and user via MySQL Databases wizard.
3. Imported schema via phpMyAdmin.
4. Configured `config.php` with production credentials.
5. Set directory permissions for upload directories.
6. Tested all features in production.

No Git-based deployment, no CI/CD pipeline, no containerization — just direct file uploads to shared hosting.

## Lessons Learned

> **Prompt quality directly determines output quality.**

Spending time writing clear, specific prompts with detailed requirements, constraints, and examples consistently produced better AI-generated code. Vague prompts produced vague (often broken) code.

> **AI-generated code must be tested thoroughly.**

Common issues included missing edge case handling, insecure defaults, incorrect database relationships, and assumptions that did not hold in production. Every line of generated code was reviewed and tested.

> **Modular architecture is worth the investment.**

Independent modules can be debugged, fixed, or replaced without touching the rest of the system. This made iteration faster and reduced the risk of regressions.

> **Shared hosting is viable for PHP + AI projects.**

The main constraints are PHP execution time limits and memory limits, but these can be worked around with stateless scripts and client-side processing.

## Results

- A fully functional community blogging platform deployed on shared hosting.
- Secure authentication with email verification, OTP login, rate limiting, and brute-force detection.
- Multi-provider AI integration with automatic fallback and key rotation.
- 15+ client-side utility tools available to users.
- Contact system with anti-spam protection.
- Modular codebase that can be extended with new features.

## Reflection

This project taught me that building software with AI is not about replacing developer skills. It is about learning to communicate requirements clearly, think systematically about architecture, and maintain quality standards through rigorous testing and iteration.

AI accelerated the implementation significantly, but the product direction, architecture decisions, testing methodology, and quality control remained my responsibility. The most valuable skill I developed was not getting AI to generate code — it was learning how to specify what I needed, evaluate what I received, and iterate toward a working solution.

---

## FlyRank Case Study

### Voice Card

> *Building practical AI that solves real problems.*

### Problem

Content creators need a platform where they can publish articles, engage a community, and get AI assistance with writing and SEO — all without complex infrastructure. Most existing solutions are either too simple (basic blog platforms) or too complex (enterprise CMS with cloud hosting requirements).

### What I Did

I built a community blogging platform using PHP and MySQL that combines traditional content management with AI-assisted writing tools. The platform runs on standard cPanel shared hosting.

**Key work included:**
- Designing the database schema for users, posts, categories, likes, comments, and AI chat history.
- Building secure authentication with email verification and OTP login.
- Integrating multiple AI providers (Groq, OpenRouter, Gemini) with automatic fallback and key rotation.
- Implementing client-side utility tools that work without server processing.
- Adding a contact system with multi-layer anti-spam protection.
- Deploying and testing the complete system on cPanel shared hosting.

### Challenges

| Challenge | How It Was Handled |
|---|---|
| API rate limits | Round-robin rotation across 5 keys per provider. |
| Shared hosting limitations | Client-side tools, stateless scripts, no background workers needed. |
| AI output quality | Experimented with models, temperatures, and prompt engineering. |
| Authentication security | OTP two-step login, rate limiting, brute-force detection, login logging. |

### Results

- A community blogging platform with AI assistance, running on shared hosting.
- Secure authentication protecting user accounts.
- AI chat assistant with four modes and automatic provider fallback.
- 15+ utility tools requiring no server resources.

### Before vs After

**Before:** A concept for a blogging website with AI features.

**After:** A deployed, functioning platform with user authentication, content management, AI chat assistance, utility tools, and anti-spam contact forms — all running on PHP and MySQL on shared hosting.

### Reflection

This project demonstrated that AI-assisted development is most effective when the human maintains control of architecture, testing, and product decisions. The technology choices (PHP, MySQL, shared hosting) prove that AI-powered applications do not require enterprise infrastructure.

---

*Built with AI assistance. Designed, tested, and shipped by a product-minded developer.*
