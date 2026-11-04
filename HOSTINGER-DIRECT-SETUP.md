# Extract this ZIP directly inside public_html

This is the **DIRECT public_html** package. Its ZIP root already contains `index.php`, `.htaccess`, `assets`, `uploads`, and `_private`. There is no enclosing `public_html` folder and no folder to move above it.

## Installation

1. Back up your existing website files and database. This archive does not include or overwrite `config.local.php`, databases, user uploads, session files, setup tokens, or encryption keys.
2. In Hostinger File Manager, open the domain's **public_html** folder. Upload **emotional-spending-public-html.zip** there.
3. Extract the ZIP **in that same public_html folder**, without creating an extra subfolder. Permit replacement of the packaged `index.php`, root `.htaccess`, and application/assets files. If the extraction dialog offers an extra destination folder, choose the current public_html directory.
4. Confirm that `index.php` is visible immediately inside public_html, beside `assets`, `uploads`, and `_private`. Do not extract `_private` alone or move its contents to the website root.
5. Use PHP 8.2 or newer with PDO MySQL, mbstring, fileinfo, OpenSSL, JSON, and sessions. This layout requires Apache/LiteSpeed access-control and rewrite support, as provided on compatible PHP hosting. It is a File Manager upload, not a hosting-backup migration export.

```
public_html/
    index.php
    .htaccess
    START-HERE.txt
    assets/
    uploads/
    _private/
        .htaccess
        app/
        database/
        storage/
        templates/
        vendor/
        config.example.php
```

## Database and administrator

Create a MySQL/MariaDB database and user in Hostinger, then import `_private/database/schema.sql` and `_private/database/seed.sql` into the new empty database using phpMyAdmin. Never import starter content over an existing working database.

In File Manager, copy `_private/config.example.php` to `_private/config.local.php`. Enter the real database host/name/user/password shown in hPanel, the actual HTTPS domain you are using (including a temporary hostingersite.com domain if applicable), and a unique random setup token of at least 32 characters. Generate that token with a password manager. Do not send database credentials in chat.

Visit `/admin/setup`, enter that private token, and create your administrator email and a strong unique password. Setup locks after the first administrator exists. Clear the setup token in the private configuration afterward. There is no default administrator password. Normal sign-in is `/admin/login`.

Make `_private/storage` and `uploads` writable by PHP using your hosting account's appropriate permissions. Do not use world-writable 777. The private folder must remain inaccessible by HTTP. Before adding credentials, visit `https://YOUR-DOMAIN/_private/config.example.php` and `https://YOUR-DOMAIN/_private/database/schema.sql`: they must return **403 Forbidden**. If either file is served, stop and ask Hostinger to enable the included access rules. Do not add credentials until that protection works. Do not use this in-root private layout on a server that ignores `.htaccess`.

## If you already configured an earlier package

The archive deliberately contains no private values or runtime data. Preserve your old files and backups. Copy an existing valid `config.local.php` into `_private/config.local.php` instead of re-entering credentials. If you used a local SQLite database, copy its consistent backup into `_private/storage/site.sqlite`. If SMTP credentials were saved, preserve the corresponding `storage/app.key` in `_private/storage/app.key`; do not replace it with a different key. Copy any existing uploaded images into the current `uploads` folder. A configured external MySQL database should be reused, not re-seeded.

Older misplaced `app`, `database`, `storage`, `templates`, `vendor`, and `emotional-spending-private` directories are additionally blocked by the new root rules, so extraction does not expose them. After the new site is working and you have verified backups, you can archive old unused files through File Manager. Do not delete files blindly to fix a 404.

## Security and launch status

Keep both root and `_private/.htaccess` files. The root rules deny HTTP access to private/legacy directories, config files, SQL/database files, keys, logs, backups, and uploaded ZIP archives. No passwords, paid PDFs, setup tokens, or live databases are included in this public GitHub download.

This package fixes file placement; database configuration is still required. The original workbook, genuine logo/cover, tested fillable PDF, live Whop checkout/delivery, and legal operator details still need to be supplied before launch. Checkout remains closed until the configured product requirements are met.

If there is an error after extraction, check the private PHP/hosting log rather than displaying credentials publicly. A 404 at `/index.php` usually means the files are in a different domain folder or an extra nested directory. If `/index.php` loads but other pages do not, check that the root `.htaccess` was extracted and its rewrite rules are enabled.
