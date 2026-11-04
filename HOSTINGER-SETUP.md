# Hostinger installation

Use **emotional-spending-hostinger.zip** for Hostinger. It is a custom PHP website upload, not an exported backup from an existing hosting account. Use your site's **File Manager** in hPanel, not the website-migration/backup-import screen. That migration screen may reject custom source archives even when their PHP code is valid.

## 1. Protect any existing website

Back up existing files and the database first. Use an empty/new website or staging domain when possible. Do not delete or overwrite an existing `public_html` site without a recoverable backup. No Hostinger account has been accessed or modified by this implementation.

## 2. Upload and extract

In File Manager, navigate to the domain directory that **contains** `public_html`. Upload and extract `emotional-spending-hostinger.zip` there. The resulting layout must be:

```
your-domain-directory/
    public_html/
        index.php
        .htaccess
        assets/
        uploads/
    emotional-spending-private/
        app/
        templates/
        vendor/
        database/
        storage/
        config.example.php
    HOSTINGER-SETUP.txt
```

Do not extract the whole ZIP inside `public_html`: that creates the wrong nesting. If your File Manager opens directly inside `public_html`, go up one level or use the account's all-files view. If your plan restricts access to that parent directory, ask Hostinger support how to place private application files alongside the domain's document root; do not put database credentials or writable session storage in a public folder as a workaround.

The public entry point references its sibling `emotional-spending-private` directory. That folder must keep its exact name. All PHP libraries and production dependencies are included; there are no Python scripts, Node tests, TypeScript, ASP.NET files, or required npm commands in this ZIP.

Use a PHP-enabled hosting plan and PHP 8.2 or newer. Enable PDO MySQL, mbstring, fileinfo, OpenSSL, JSON, and sessions. Keep HTTPS enabled. Hostinger's actual account configuration and server rules still require verification after upload.

## 3. Database and private configuration

Create a MySQL/MariaDB database and database user in hPanel. Use the exact host, database name, username, and password shown for your account; do not assume the example placeholders are real credentials. In phpMyAdmin, select the new empty database, import `emotional-spending-private/database/schema.sql`, then import `emotional-spending-private/database/seed.sql` once. Never import starter content over an existing production database.

Copy `emotional-spending-private/config.example.php` to `emotional-spending-private/config.local.php`. In File Manager's editor, replace the database placeholders with your account's values, keep the `mysql:host=...;dbname=...;charset=utf8mb4` structure, set your actual HTTPS domain, and set a unique random setup token of at least 32 characters. Generate that token in a password manager. Never post credentials in chat. Do not move this file under `public_html`.

Make private `storage/` and public `uploads/` writable by PHP. Ordinary directories 755 and files 644 are a starting point; private configuration/key files should be 600 where supported. Do not use 777. Sessions are created in private storage, and contact/SMTP credentials remain private. Keep TLS verification enabled.

## 4. Create your administrator

Visit `https://YOUR-DOMAIN/admin/setup`. Use the private setup token and choose your own administrator email and a unique password of at least 12 characters. There is no public/default password. Setup locks after the first administrator is created. Clear `setup_token` from the private configuration afterward, then sign in at `/admin/login`.

## 5. Test before launch

Visit all pages; verify images, mobile navigation, forms, admin login/logout, content editing, and media upload. Submit a contact message and verify it in the private inbox. Configure SMTP only with a real provider and test delivery separately. Enable HTTPS and check the domain/canonical settings.

The original workbook PDF, genuine logo/cover, tested separate fillable edition, real legal operator details, and actual Whop checkout/delivery still need to be supplied. Checkout defaults to closed. Never enable sales until the delivered files, source copy, price, consumer consent, and checkout have been verified. This packaging fix does not create those missing product materials or prove a live payment works.

## Troubleshooting

- **The migration screen rejects the archive:** use File Manager as above. This package is not a hosting backup or a WordPress migration export.
- **Nested `public_html/public_html`:** extraction was done one directory too deep. Correct the layout after backing up any existing files.
- **Missing bootstrap/private-directory error:** make sure `emotional-spending-private` is a sibling of `public_html` with the exact name shown.
- **500 error:** check the private hosting/PHP error log for the cause. Check database credentials, enabled extensions, PHP version, and directory permissions. Never display credentials publicly to debug.
- **404 on every route except the homepage:** confirm `public_html/.htaccess` was uploaded and the hosting server applies its rewrite rules.
- **Form/session problems:** verify PHP can write the private `storage` directory, then reload to obtain a new CSRF token.

The Hostinger package was tested locally in its extracted two-directory layout. No live hPanel upload, migration acceptance, Hostinger server configuration, or domain deployment has been performed.
