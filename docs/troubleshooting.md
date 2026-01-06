## Troubleshooting Summary

- ERR_TOO_MANY_REDIRECTS:
  Caused by WordPress not detecting HTTPS behind Cloudflare.
  Fixed by handling X-Forwarded-Proto and correcting site URLs.

- HTTP 500 Errors:
  Caused by PHP parse errors in wp-config.php.
  Diagnosed using php -l and Apache error logs.

- Database Connection Issues:
  Caused by mismatched table prefixes.
  Resolved by validating schema and updating configuration.
