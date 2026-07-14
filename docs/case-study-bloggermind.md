# Case Study: Blogger Mind AI CMS

## Voice Card

> Building practical AI that solves real problems.

---

## Project Overview

Blogger Mind is a community blogging platform with AI-assisted writing tools — built with PHP and MySQL, deployed on cPanel shared hosting.

| Role | Tech Stack |
|---|---|
| Backend AI Engineer (Personal Project) | PHP, MySQL, JavaScript, HTML/CSS, Groq API, Git & GitHub, cPanel Hosting |

## The Problem

Publishing content as an individual creator requires juggling multiple tools: one for writing, another for SEO, another for image editing, another for publishing. For creators who run their own websites, this fragmentation slows production and makes consistent publishing difficult.

Existing solutions fall into two camps:
- **Simple blogging platforms** that lack AI assistance and modern features.
- **Enterprise CMS platforms** that require cloud infrastructure and ongoing costs.

Neither option suited a self-hosted, AI-assisted approach on affordable shared hosting.

## Goals

- Build a deployable community blogging platform with AI assistance.
- Implement secure authentication (email verification, OTP login, rate limiting).
- Keep the codebase modular for future extension.
- Deploy on cPanel shared hosting — no Docker, no cloud.

## Approach

I broke the project into independent modules and developed each through an AI-assisted workflow:

1. Define feature requirements and acceptance criteria.
2. Design the database schema and module boundaries.
3. Write a detailed prompt for AI, specifying requirements, schema, edge cases, and security constraints.
4. Review the AI-generated code for correctness and security.
5. Test manually across browsers, edge cases, and attack vectors.
6. Debug and refine until the feature worked correctly.
7. Integrate into the codebase.
8. Deploy and monitor.

### Modules

| Module | What It Does |
|---|---|
| Authentication | Registration with email verification, login with OTP, password reset, rate limiting |
| Profile Management | Ajax-driven editing: username, display name, bio, avatar upload |
| Content Management | Post CRUD with TinyMCE editor, categories, status management |
| Community | Infinite scroll feed, like system, author leaderboard, sharing |
| AI Integration | Multi-provider chat assistant with four modes, chat history, web search |
| Utility Tools | 15+ client-side tools (password generator, calculators, image tools, text tools) |
| Contact & Support | Contact form with anti-spam, support center pages |

## My Decisions

| Decision | Reasoning |
|---|---|
| **No framework** | Zero dependencies, full control, works on any PHP hosting |
| **PDO prepared statements** | Eliminates SQL injection without ORM complexity |
| **Multi-provider AI** | Redundancy — if one provider is rate-limited, others serve as fallback |
| **Key rotation** | Up to 5 keys per provider distributed via round-robin to handle rate limits |
| **Client-side tools** | Reduce server load; tools work under high traffic |
| **OTP login** | Two-step authentication adds security beyond passwords alone |
| **Vanilla JavaScript** | No build step required; works directly on shared hosting |

## Challenges

| Challenge | Resolution |
|---|---|
| **API rate limits** | Implemented round-robin rotation across 5 keys per provider |
| **AI response quality** | Experimented with prompts, temperature settings, and model selection across three providers |
| **Shared hosting constraints** | Kept processes stateless; client-side tools for utility features |
| **Image upload security** | Custom upload handler with MIME verification, extension whitelist, CSRF protection |
| **OTP delivery reliability** | Email-based OTP with 10-minute expiry and single-use enforcement |
| **Brute-force protection** | Rate limiting with per-IP tracking and admin notification |

## Iterations

The AI Assistant is the best example of the iteration process.

**First attempt:** AI suggested a single-provider implementation with no fallback. I rejected this and specified multi-provider architecture in the prompt.

**Second attempt:** The multi-provider structure was correct, but error handling was missing for API timeouts. I added error handling requirements to the prompt.

**Third attempt:** Error handling was in place, but the chat UI did not show connection status to the user. I added a status indicator requirement.

**Fourth attempt:** The UI was complete, but the global widget in the footer was not included. I added the widget requirement.

Each iteration closed a gap between what was generated and what was needed. The process was not linear — it required testing, identifying issues, refining prompts, and re-testing.

## Testing

Every feature was tested manually:

- **Functional:** Does the feature do what it is supposed to?
- **Edge cases:** Empty inputs, long strings, special characters, rapid submissions.
- **Security:** CSRF token validation, SQL injection attempts, XSS vectors, file upload exploits.
- **Cross-browser:** Chrome, Firefox, Safari, Edge.
- **Responsive:** Desktop, tablet, mobile.
- **Production:** Full test suite after cPanel deployment.

### Issues found during testing

- Missing input validation on edge cases (empty fields, very long strings).
- Incorrect database queries that worked in development but failed with real data.
- CSS layout issues on specific browser/device combinations.
- JavaScript errors from undefined variables in certain states.
- Session handling edge cases with expired or invalid sessions.

## Deployment

Deployed using cPanel's native tools — no Git-based deployment, no CI/CD pipeline:

1. Uploaded files via cPanel File Manager.
2. Created MySQL database and user via MySQL Databases wizard.
3. Imported schema via phpMyAdmin.
4. Configured `config.php` with production credentials.
5. Set directory permissions on upload directories.
6. Tested all features in production.

## Results

- A fully functional community blogging platform deployed on shared hosting.
- Secure authentication with email verification, OTP login, rate limiting, brute-force detection.
- Multi-provider AI integration with automatic fallback and key rotation.
- 15+ client-side utility tools available to users.
- Contact system with multi-layer anti-spam protection.
- Modular codebase that can be extended with new features.

## Lessons Learned

**Prompt quality determines output quality.** Spending time writing clear, specific prompts with requirements, constraints, and examples consistently produced better AI-generated code. Vague prompts produced vague (often broken) code.

**AI-generated code must be tested thoroughly.** Common issues included missing edge case handling, insecure defaults, incorrect database relationships, and assumptions that did not hold in production.

**Modular architecture pays for itself.** Independent modules can be debugged, fixed, or replaced without touching the rest of the system. This made iteration faster and reduced the risk of regressions.

**Shared hosting is viable for PHP + AI projects.** The main constraints — execution time limits and memory limits — can be worked around with stateless scripts and client-side processing.

## Reflection

This project taught me that building software with AI is not about replacing developer skills. It is about learning to communicate requirements clearly, think systematically about architecture, and maintain quality standards through testing and iteration.

AI accelerated the implementation, but the product direction, architecture decisions, testing methodology, and quality control remained my responsibility.

## Before vs After

**Before:** A concept for a blogging website with AI features.

**After:** A deployed platform with user authentication, content management, AI chat assistance, 15+ utility tools, and anti-spam contact forms — all running on PHP and MySQL on shared hosting.

## Future Improvements

- AI research assistant for automated topic research.
- Scheduled publishing via Cron.
- Analytics dashboard.
- Mobile application.

---

## Contact

- **Website:** [https://bloggersminds.com/](https://bloggersminds.com/)
- **GitHub:** [https://github.com/mbishanto/BloggerMind-with-AI](https://github.com/mbishanto/BloggerMind-with-AI)
