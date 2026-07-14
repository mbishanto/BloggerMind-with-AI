# FlyRank Case Study: Blogger Mind AI CMS

## Voice Card

> Building practical AI that solves real problems.

---

## Problem

Content creators spend significant time researching topics, writing articles, optimizing SEO, managing images, and publishing content. These repetitive tasks slow down content production and make it difficult for small teams to maintain a consistent publishing schedule.

Existing solutions are either too simple (basic blog platforms with no AI) or too complex (enterprise CMS requiring cloud infrastructure and ongoing costs).

## What I Did

I built a community blogging platform using PHP and MySQL that combines traditional content management with AI-assisted writing tools. The platform runs on standard cPanel shared hosting — no Docker, no cloud infrastructure.

**Key work included:**

- Designing the database schema for users, posts, categories, likes, comments, and AI chat history.
- Building secure authentication with email verification and OTP login.
- Integrating multiple AI providers (Groq, OpenRouter, Gemini) with automatic fallback and key rotation for rate limit handling.
- Implementing 15+ client-side utility tools that work without server processing.
- Adding a contact system with multi-layer anti-spam protection (honeypot, timing checks, URL counting, bad word filter, IP rate limiting).
- Deploying and testing the complete system on cPanel shared hosting.

## Challenges

| Challenge | How It Was Handled |
|---|---|
| API rate limits | Round-robin rotation across 5 keys per provider |
| Shared hosting limitations | Client-side tools, stateless scripts, no background workers needed |
| AI output quality | Experimented with models, temperatures, and prompt engineering |
| Authentication security | OTP two-step login, rate limiting, brute-force detection, login logging |

## Results

- A community blogging platform with AI assistance, running on shared hosting.
- Secure authentication protecting user accounts from brute-force attacks.
- AI chat assistant with four modes and automatic provider fallback.
- 15+ utility tools requiring no server resources.
- Modular codebase structure supporting future feature additions.

## Reflection

This project demonstrated that AI-assisted development is most effective when the human maintains control of architecture, testing, and product decisions. The technology choices — PHP, MySQL, shared hosting — prove that AI-powered applications do not require enterprise infrastructure.

The most valuable lesson was that **prompt quality determines output quality.** Spending time writing clear, specific prompts with requirements, constraints, and examples consistently produced better AI-generated code than vague descriptions.

## Before vs After

**Before:** A concept for a blogging website with AI features.

**After:** A deployed platform with user authentication, content management, AI chat assistance, 15+ utility tools, and anti-spam contact forms — all running on PHP and MySQL on shared hosting.

---

## Contact

- **Website:** [https://bloggersminds.com/](https://bloggersminds.com/)
- **GitHub:** [https://github.com/mbishanto/BloggerMind-with-AI](https://github.com/mbishanto/BloggerMind-with-AI)
