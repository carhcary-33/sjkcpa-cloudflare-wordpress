# sjkcpa-cloudflare-wordpress
Secure WordPress deployment using Cloudflare Tunnel (Zero Trust)

# Secure WordPress Deployment Behind Cloudflare Tunnel

## Overview
This project demonstrates deploying a production-style WordPress application on Linux and securely exposing it to the internet using **Cloudflare Tunnel (Zero Trust)** instead of traditional port forwarding.

The goal was to reduce attack surface, enforce HTTPS correctly behind a reverse proxy, and troubleshoot real-world infrastructure issues across DNS, TLS, web server, PHP, and database layers.

🔗 Live Site: https://sjkcpa.tax

---

## Architecture

User Browser  
↓ HTTPS  
Cloudflare Edge (DNS + Proxy)  
↓ Cloudflare Tunnel  
cloudflared (systemd service)  
↓ localhost  
Apache + PHP  
↓  
MariaDB  

---

## Key Features
- WordPress hosted on Linux using Apache, PHP, and MariaDB
- Cloudflare Tunnel used to expose the site without opening inbound firewall ports
- HTTPS terminated at Cloudflare with proper reverse-proxy handling
- Persistent tunnel via systemd service
- Least-privilege database user configuration
- Production-style troubleshooting and validation

---

## Technologies Used
- Linux (Debian-based)
- Apache
- PHP
- MariaDB
- WordPress
- Cloudflare Tunnel (cloudflared)
- Cloudflare DNS & Proxy
- systemd

---

## Implementation Highlights
- Configured Cloudflare Tunnel with CNAME-based DNS routing
- Eliminated inbound port exposure (no 80/443 open)
- Resolved HTTPS redirect loops caused by reverse proxy behavior
- Implemented `X-Forwarded-Proto` handling for WordPress behind Cloudflare
- Created and validated least-privilege MariaDB user for WordPress
- Diagnosed and fixed PHP parse errors causing HTTP 500 responses
- Corrected WordPress table prefix mismatches in the database

---

## Troubleshooting Highlights
- Resolved `ERR_TOO_MANY_REDIRECTS` caused by improper HTTPS detection
- Diagnosed HTTP 500 errors via Apache logs and PHP linting
- Fixed malformed `wp-config.php` causing PHP fatal errors
- Validated database schema and corrected WordPress options (`home`, `siteurl`)
- Ensured tunnel reliability via systemd auto-restart

---

## Security Considerations
- No inbound ports exposed to the public internet
- TLS handled at Cloudflare edge
- Secrets excluded from repository
- Principle of least privilege applied to database access
- Tunnel identity managed via Cloudflare Zero Trust

---

## Lessons Learned
- Reverse proxy HTTPS handling must be explicitly configured at the application layer
- Cloudflare Tunnel significantly reduces attack surface compared to port forwarding
- WordPress errors often originate from database or configuration mismatches
- Log-driven troubleshooting is essential for production systems

---

## Future Enhancements
- Protect `/wp-admin` with Cloudflare Access (SSO)
- Add Cloudflare WAF rules
- Implement automated backups
- Add monitoring and alerting
