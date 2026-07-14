# Security

Blogger Mind implements security at multiple layers of the application. This page documents the measures in place.

---

## Authentication Security

| Measure | Implementation |
|---|---|
| Password hashing | `password_hash()` with `PASSWORD_DEFAULT` (bcrypt) |
| Session cookies | HttpOnly, SameSite=Lax, Secure (30-day lifetime) |
| Password reset | 6-digit OTP, 15-minute expiry, single-use |
| Login throttling | 10 attempts per 10 minutes per IP |
| Brute-force detection | Admin notified when threshold is exceeded |
| Login logging | All attempts recorded in `login_attempts` table |

## CSRF Protection

Every state-changing form includes a CSRF token, generated and validated via `lib/csrf.php`.

```
Token generation:
  $_SESSION['csrf_token'] = bin2hex(random_bytes(32))

Token validation:
  if (!hash_equals($_SESSION['csrf_token'], $_POST['csrf_token'])) {
      // reject request
  }
```

## SQL Injection Prevention

All database queries use PDO prepared statements with named parameters. There is no raw SQL interpolation anywhere in the codebase.

```php
// Safe — used everywhere
$stmt = $pdo->prepare('SELECT * FROM users WHERE email = :email');
$stmt->execute(['email' => $email]);
```

## XSS Prevention

Output is escaped using `htmlspecialchars()` with `ENT_QUOTES | ENT_SUBSTITUTE | ENT_HTML5` before rendering in HTML context.

## File Upload Security

| Measure | Implementation |
|---|---|
| MIME type verification | `finfo` module checks actual file type |
| Extension whitelist | JPG, PNG, WEBP only for avatars |
| Size limits | 2MB maximum |
| Unique filenames | `bin2hex(random_bytes(16))` to prevent collisions and path traversal |

## Input Validation

- Email: validated via `filter_var()` with `FILTER_VALIDATE_EMAIL`
- Username: regex `/^[A-Za-z0-9_]{3,20}$/`
- URLs: validated format and protocol
- Numeric fields: cast to appropriate types
- String lengths: enforced limits on all text inputs

## Anti-Spam (Contact Form)

| Layer | Implementation |
|---|---|
| Honeypot | Hidden field that bots fill in, humans do not |
| Timing threshold | Form submission must take at least 3 seconds |
| URL counting | Messages with 3+ URLs are rejected |
| Bad word filter | Blocked words in message content |
| IP rate limiting | 3 submissions per 10 minutes per IP |

## Error Handling

- Production errors are logged to `error_log`, not displayed to users.
- Custom error pages (404, 500) without system information.
- Debug mode is disabled in production.
