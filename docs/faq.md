# FAQ

---

**Is Blogger Mind a finished product?**

It is under active development. Core features work in production, but new features are still being added.

**Can I host it myself?**

Yes. The project is designed for cPanel shared hosting. See the [deployment guide](deployment.md).

**Do I need API keys for AI features?**

Yes. The AI Assistant requires at least one Groq API key. See the [installation guide](installation.md) for configuration.

**Is there a demo I can try?**

The live site is at [https://bloggersminds.com/](https://bloggersminds.com/).

**Does it work without JavaScript?**

The core reading experience works without JavaScript. Creating posts, AI chat, and utility tools require JavaScript.

**Is there a mobile app?**

No mobile app exists. The website is responsive and works in mobile browsers.

**Can I contribute?**

Yes. See [contributing.md](contributing.md).

**What AI providers are supported?**

Groq (primary), OpenRouter (fallback), and Gemini (tertiary). The system falls back automatically if one provider is unavailable.

**Why PHP instead of a modern framework?**

PHP runs on virtually every web host with no additional setup. For a self-hosted project targeting shared hosting, this is the most accessible choice.
