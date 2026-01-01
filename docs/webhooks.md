# Flag Webhooks

Proctorme can notify your system in real‑time whenever a suspicious event occurs.

## Retry Policy
- Up to 3 delivery attempts
- Exponential backoff
- Receivers must be idempotent

## Security
- Always use HTTPS
- Verify request authenticity
- Restrict IPs if possible