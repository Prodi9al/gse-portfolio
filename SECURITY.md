# Security Policy

## Reporting a vulnerability

Please **do not** open a public issue for security problems. Report privately
via [GitHub Security Advisories](https://github.com/Prodi9al/gse-portfolio/security/advisories/new)
or contact the maintainer (@Prodi9al).

## Secrets

Configured via a local `.env` (git-ignored); copy `.env.example`.

| Variable | Purpose |
|----------|---------|
| `SECRET_KEY` | session signing — the backend refuses to start without it |
| `BOT_TOKEN` | Telegram bot token (from @BotFather) |
| `BOT_USERNAME` | Telegram login widget |
| `ALLOWED_IDS` | comma-separated Telegram user IDs allowed in |

Generate `SECRET_KEY` with:

```bash
python -c "import secrets; print(secrets.token_hex(32))"
```

Never commit `.env`. If a token leaks, revoke it in @BotFather and rotate.

## Deployer checklist

- [ ] `.env` present, git-ignored, mode `600`.
- [ ] `SECRET_KEY` is a real random value (not the example).
- [ ] `ALLOWED_IDS` restricted to the intended accounts.
- [ ] `COOKIE_SECURE=true` in production (Caddy serves HTTPS).
- [ ] Backend runs as a dedicated user, not root.
