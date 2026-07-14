# Deployment

This guide covers deploying Blogger Mind to cPanel shared hosting.

---

## Requirements

- PHP 8.0 or higher
- MySQL 5.7 or higher
- Apache with `mod_rewrite`
- A cPanel hosting account

---

## Step 1: Upload Files

**cPanel File Manager:**

1. Log in to cPanel, open **File Manager**.
2. Navigate to `public_html/`.
3. Click **Upload** and select all project files.

**FTP:**

1. Get FTP credentials from cPanel (FTP Accounts).
2. Connect using FileZilla, Cyberduck, or WinSCP.
3. Upload all files to `public_html/`.

## Step 2: Create Database

1. In cPanel, open **MySQL Databases**.
2. Create a new database.
3. Create a new user with a strong password.
4. Add the user to the database with **All Privileges**.

## Step 3: Import Schema

1. Open **phpMyAdmin**.
2. Select your database.
3. Go to **Import**, choose the `.sql` file, click **Go**.

## Step 4: Configure

Edit `config.php`:

```php
define('DB_HOST', 'localhost');
define('DB_NAME', 'your_database_name');
define('DB_USER', 'your_database_user');
define('DB_PASS', 'your_database_password');
define('APP_URL', 'https://yourdomain.com');
define('ADMIN_EMAIL', 'you@example.com');
```

## Step 5: Set Permissions

Set `uploads/` directories to `755` via File Manager > Change Permissions.

## Step 6: Verify

- Visit your domain, confirm the homepage loads.
- Register an account, check email for verification.
- Log in with OTP verification.
- Create a test post.
- Test the AI Assistant.

## AI API Keys

To enable AI features, add API keys to `config.php`:

```php
define('GROQ_API_KEY', 'gsk_your_key');
define('OPENROUTER_API_KEY', 'sk-or-your_key');
define('GEMINI_API_KEY', 'your_gemini_key');
define('SERP_API_KEY', 'your_serpapi_key');
```

Up to 5 keys per provider supported (round-robin rotation).
