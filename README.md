# Emotional Spending — extract directly into public_html

**[Download emotional-spending-public-html.zip](downloads/emotional-spending-public-html.zip)**

**[Read the direct-upload instructions](HOSTINGER-DIRECT-SETUP.md)**

In Hostinger File Manager, open the domain's **public_html**, upload this ZIP, and extract **in the current folder**. Allow replacement of the packaged index.php and .htaccess after backing up existing files. Do not create another public_html subfolder. No folder needs to be moved above public_html.

The ZIP opens directly to:

```
index.php
.htaccess
START-HERE.txt
assets/
uploads/
_private/
```

The protected _private folder contains the application, configuration example, database schema, templates, and production dependencies. Keep both .htaccess files. Before entering credentials, confirm that /_private/config.example.php returns 403 Forbidden. Configure the actual database in _private/config.local.php using the included guide. Never overwrite an existing database with starter content. Existing configuration and data are not included or overwritten by the ZIP.

Validated on Apache 2.4.69 and PHP 8.4.27: all 17 browser-test groups, root loading, clean-URL rewrites, media uploads, and 13 protected private/config/legacy URLs returning HTTP 403. No actual Hostinger account or migration screen was accessed. Use File Manager, not a backup-migration tool.

The original workbook PDF, genuine logo/cover, tested fillable PDF, real legal operator details, and live Whop checkout/delivery are still required before commercial launch. Checkout stays closed by default.

SHA-256: `dbdd95674b0249cc31338549f38f412e0b6c65c14e647f24e818ecbb28744b2e`

## Alternative layouts

- [Earlier two-directory Hostinger package](downloads/emotional-spending-hostinger.zip) — requires extraction above public_html; not the direct-upload package.
- [Original public-directory layout](downloads/emotional-spending-website.zip) — for hosting whose document root can point to public/.
