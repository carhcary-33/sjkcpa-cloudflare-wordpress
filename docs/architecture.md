## Architecture Notes

This deployment uses Cloudflare Tunnel to securely expose a local WordPress instance without opening inbound firewall ports.

Benefits:
- Eliminates NAT and port forwarding
- Prevents direct IP exposure
- Allows Cloudflare to handle TLS and DDoS protection
