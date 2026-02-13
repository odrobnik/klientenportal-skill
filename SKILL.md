---
name: klientenportal
description: "Automate RZL Klientenportal.at — a web-based portal by RZL Software for exchanging receipts, invoices, and reports with your tax accountant. Login/logout, upload documents (Belegübergabe), list released files, and download Kanzleidokumente via Playwright."
summary: "RZL Klientenportal automation: upload receipts, download reports."
version: 1.2.0
homepage: https://github.com/odrobnik/klientenportal-skill
metadata:
  openclaw:
    emoji: "📋"
    requires:
      bins: ["python3", "playwright"]
      python: ["playwright"]
---

# RZL Klientenportal

Automate [klientenportal.at](https://klientenportal.at) — a web portal by [RZL Software](https://www.rzl.at) for securely exchanging accounting documents between clients and their tax accountant. Upload receipts and invoices, download reports and Kanzleidokumente, all via Playwright browser automation.

**Entry point:** `{baseDir}/scripts/klientenportal.py`

## Prerequisites

Requires Playwright with Chromium. If not installed:
```bash
pip install playwright
playwright install chromium
```

## Configuration

Run setup with your portal ID, user ID, and password:

```bash
python3 {baseDir}/scripts/klientenportal.py setup --portal-id 652 --user-id YOUR_USER_ID --password YOUR_PASSWORD
```

Or via env vars: `KLIENTENPORTAL_PORTAL_ID`, `KLIENTENPORTAL_USER_ID`, `KLIENTENPORTAL_PASSWORD`.

The portal ID identifies your accountant's portal instance (e.g. `652`). The URL `https://klientenportal.at/prod/{portal_id}` is derived automatically.

Config is saved to `{workspace}/klientenportal/config.json` with restrictive file permissions.

## Belegkreis Categories

| Code | Name | Use for |
|------|------|---------|
| ER | Eingangsrechnungen | Incoming invoices |
| AR | Ausgangsrechnungen | Outgoing invoices |
| KA | Kassa | Credit card payments |
| SP | Sparkasse | Bank account receipts |

## Commands

```bash
python3 {baseDir}/scripts/klientenportal.py login
python3 {baseDir}/scripts/klientenportal.py upload -f invoice.pdf --belegkreis KA
python3 {baseDir}/scripts/klientenportal.py upload -f *.xml --belegkreis SP
python3 {baseDir}/scripts/klientenportal.py released
python3 {baseDir}/scripts/klientenportal.py download
python3 {baseDir}/scripts/klientenportal.py logout
```

## Recommended Flow

```
login → upload / released / download → logout
```

Always call `logout` after completing all operations to clear the stored browser session.

## Notes
- Session state stored in `{workspace}/klientenportal/` with restrictive permissions (dirs 700, files 600).
- Download output defaults to `/tmp/openclaw/klientenportal/` (override with `-o`), sandboxed to workspace or `/tmp`.
- Credentials in `config.json` only — no `.env` file loading.
