# Installation

Blogger Mind is designed for cPanel shared hosting. These instructions cover manual deployment from scratch.

---

## Requirements

- PHP 8.0 or higher
- MySQL 5.7 or higher
- Apache with `mod_rewrite` enabled
- A cPanel hosting account (or any hosting with PHP + MySQL)

---

## Deployment Steps

### Step 1: Upload Files

**Via cPanel File Manager:**

1. Log in to your cPanel dashboard.
2. Open **File Manager**.
3. Navigate to `public_html/` (or create a subdirectory such as `blog/`).
4. Click **Upload** and select all project files from your local machine.
5. Wait for the upload to complete.

**Via FTP:**

1. Get FTP credentials from cPanel (FTP Accounts section).
2. Connect using an FTP client (FileZilla, Cyberduck, WinSCP).
3. Upload all files to `public_html/` or your chosen subdirectory.

### Step 2: Create a MySQL Database

1. In cPanel, open **MySQL Databases**.
2. Under "Create New Database", enter a name (e.g., `youruser_blogger`).
3. Click **Create Database**.
4. Scroll down to **Add New User**, create a username and strong password.
5. Click **Create User**.
6. Under **Add User to Database**, select your user and database, then grant **All Privileges**.
7. Click **Make Changes**.

### Step 3: Import the Database Schema

1. In cPanel, open **phpMyAdmin**.
2. Select your newly created database from the left sidebar.
3. Click the **Import** tab at the top.
4. Click **Choose File** and select the `.sql` schema file from your project files.
5. Click **Go** to import the database structure and initial data.

### Step 4: Configure `config.php`

1. In cPanel File Manager, navigate to your project directory.
2. Open `config.php` for editing.
3. Update the following values:

```php
// Database configuration
define('DB_HOST', 'localhost');
define('DB_NAME', 'youruser_blogger');
define('DB_USER', 'youruser_dbuser');
define('DB_PASS', 'your_secure_password');

// Site URL
define('APP_URL', 'https://yourdomain.com');

// Admin email
define('ADMIN_EMAIL', 'you@example.com');
```

### Step 5: Set Directory Permissions

Upload directories need to be writable by the web server. In cPanel File Manager:

1. Right-click the `uploads/` directory.
2. Select **Change Permissions**.
3. Set permissions to `755` (or `0755`).
4. Repeat for `uploads/avatars/` if that subdirectory exists.

### Step 6: Verify Installation

1. Open your domain in a browser.
2. The homepage should load with the community feed and sidebar widgets.
3. Click **Register** and create an account.
4. Check the email address you registered for the verification link.
5. Log in with your email and password, then enter the 6-digit OTP sent to your email.
6. Try creating a post using the TinyMCE editor.
7. Test the AI Assistant from the navigation or the floating widget.

---

## AI API Keys (Optional)

The AI Assistant feature requires at least one AI provider API key. Without these keys, the AI features will not function.

### Configuration

In `config.php`, add your API keys:

```php
// Groq (primary) — at least one key required for AI
define('GROQ_API_KEY', 'gsk_your_groq_api_key_here');

// OpenRouter (fallback) — optional
define('OPENROUTER_API_KEY', 'sk-or-your_openrouter_key_here');

// Gemini (tertiary) — optional
define('GEMINI_API_KEY', 'your_gemini_api_key_here');

// SerpAPI for web search — optional
define('SERP_API_KEY', 'your_serpapi_key_here');
```

You can add up to 5 keys per provider for rate limit handling. Keys are used in round-robin rotation.

---

## Troubleshooting

| Issue | Likely Cause | Solution |
|---|---|---|
| Blank page | PHP error not displayed | Check PHP error logs in cPanel > Error Log. |
| "Database connection failed" | Wrong credentials in config.php | Verify DB_HOST, DB_NAME, DB_USER, DB_PASS. |
| 404 errors | mod_rewrite not enabled | Enable Apache mod_rewrite in cPanel > Select PHP Version > Extensions. |
| File upload fails | Directory permissions | Set 755 on uploads/ directories. |
| AI not responding | Missing API key | Add API keys to config.php. |
| Registration email not sent | PHP mail() not configured | Use SMTP configuration if available, or check with your hosting provider. |
| OTP not received | Email in spam folder | Check spam folder. Verify email configuration. |
