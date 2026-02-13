# RZL Klientenportal Skill

An [OpenClaw](https://openclaw.ai) skill for automating [klientenportal.at](https://klientenportal.at) — a web portal by [RZL Software](https://www.rzl.at) for securely exchanging accounting documents between clients and their tax accountant.

## Features

- **Upload** receipts and invoices (Belegübergabe) by Belegkreis category
- **Download** released Kanzleidokumente (reports from your accountant)
- **List** released files with metadata
- **Session management** with automatic login/logout and restrictive file permissions

## Requirements

- Python 3
- [Playwright](https://playwright.dev/python/) with Chromium
- An [OpenClaw](https://openclaw.ai) installation

## Setup

```bash
python3 scripts/klientenportal.py setup \
  --portal-id 652 \
  --user-id YOUR_USER_ID \
  --password YOUR_PASSWORD
```

Or via environment variables:
- `KLIENTENPORTAL_PORTAL_ID` — your accountant's portal instance ID
- `KLIENTENPORTAL_USER_ID`
- `KLIENTENPORTAL_PASSWORD`

## Usage

```bash
# Login
python3 scripts/klientenportal.py login

# Upload documents
python3 scripts/klientenportal.py upload -f invoice.pdf --belegkreis KA

# List released files
python3 scripts/klientenportal.py released

# Download Kanzleidokumente
python3 scripts/klientenportal.py download

# Logout (clears browser session)
python3 scripts/klientenportal.py logout
```

## Belegkreis Categories

| Code | Name | Use for |
|------|------|---------|
| ER | Eingangsrechnungen | Incoming invoices |
| AR | Ausgangsrechnungen | Outgoing invoices |
| KA | Kassa | Credit card payments |
| SP | Sparkasse | Bank account receipts |

## License

MIT
