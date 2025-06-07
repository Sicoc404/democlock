# Telegram Clock Bot

A Telegram bot for managing employee clock-in/clock-out, OT, leave, expense claims, and monthly salary payments with PDF reporting.

## Features

### 👨‍💼 Employee Tools

* Clock in with live GPS location (uses Google Maps API)
* Clock out with worked-hour auto calculation
* Apply off-day (/offday)
* Submit expense claims with receipt upload
* Submit OT (overtime) entries

### 💰 Admin Management

* Set monthly salary for each worker
* Approve salary and claim payments (/paid)
* View monthly summaries (/checkstate, /previousreport)

### 📊 Reporting

* One-click PDF generation of:

  * Work Hours Summary
  * Salary Summary
  * All Clock-in/OT/Claims Data

### 🔐 Permissions

* Admin-only commands secured via `ADMIN_IDS`

## Deployment Instructions

### 1. Install dependencies:

```bash
pip install -r requirements.txt
```

### 2. Set environment variables (`.env`):

```env
# Required:
DATABASE_URL=your_postgresql_connection_string
TOKEN=your_telegram_bot_token
ADMIN_IDS=comma_separated_admin_ids

# Optional:
GOOGLE_API_KEY=your_google_maps_api_key
DEFAULT_HOURLY_RATE=20.0
DEFAULT_MONTHLY_SALARY=3500.0
```

### 3. Initialize database (only once):

```bash
python init_db.py
```

### 4. Run the bot locally:

```bash
python clock_bot.py
```

If deployed on Render, webhook will auto-configure from `RENDER_EXTERNAL_URL`.

## Telegram Commands

### 🧑 User Commands

* `/start` – Show welcome & command guide
* `/clockin` – Share location to clock in
* `/clockout` – End work and calculate hours
* `/offday` – Mark current day as leave
* `/claim` – Submit a photo claim
* `/OT` – Record overtime

### 👮 Admin Commands

* `/checkstate` – View daily stats
* `/salary` – Set salary per worker
* `/paid` – Approve salary & mark as paid
* `/topup` – Manually add balance
* `/viewclaims` – View 30-day claims
* `/PDF` – Export report
* `/previousreport` – View prior month data

## Database Schema

This bot uses PostgreSQL with tables:

* `drivers` – user & salary info
* `clock_logs` – daily clock in/out + leave
* `claims` – uploaded claims + photos
* `salary_payments` – salary issuance log
* `ot_logs` – overtime logs
* `monthly_reports` – worker summaries

## Security Checklist

* ✅ `.env` with restricted API key
* ✅ ADMIN\_IDS filters admin-only access
* ✅ Logs errors but hides sensitive info
* ✅ Can run behind Gunicorn for production

## Demo Deployment Tips

* Set `IS_DEMO=True` to limit commands (optional in code)
* Use Nominatim if no Google API is available
* Budget API usage with quota alerts

## License

MIT License — build freely, credit appreciated!

## Credits

Created by \[your name]. Contributions welcome!
