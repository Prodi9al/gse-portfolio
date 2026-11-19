# Contributing to GH₵ Portfolio

Tracks Ghana Stock Exchange buys/sells and shows P&L over time. Backend is
**FastAPI** + SQLite; the Telegram bot lives in `bot/`.

## Setup

```bash
cp .env.example .env          # set SECRET_KEY, BOT_TOKEN, ALLOWED_IDS
python -m venv .venv && source .venv/bin/activate
pip install -r backend/requirements.txt
./install.sh                  # or ./reinstall.sh to reset
```

## Layout

| Path | Purpose |
|------|---------|
| `backend/main.py` | FastAPI app + routes |
| `backend/db.py` | SQLite schema/init |
| `backend/portfolio.py` | holdings + P&L reconstruction |
| `backend/auth.py` | Telegram login / session |
| `backend/price_poller.py`, `snapshot_job.py` | price polling + snapshots |
| `backend/tests/` | pytest suite |
| `bot/` | Telegram bot |

## Tests

```bash
cd backend && pytest -q
```

CI (`.github/workflows/ci.yml`) runs the suite on Python 3.11 and 3.12.

## Rules

- **Never commit secrets.** Use `.env` (git-ignored) and `.env.example`.
- Keep position math in `portfolio.py`; add tests for any change there.
- The GSE API has no history — don't introduce code that assumes it does.
- Match the existing FastAPI + pytest style.

## License

Contributions are MIT-licensed (see [LICENSE](LICENSE)).
