# KREDANSH CAPITAL ONLINE ERP V1

Server/PWA conversion of uploaded KREDANSH V64, using the Railway-safe Flask deployment pattern from uploaded GAUR CRM.

## Included now
Dashboard, Bank Master, Employee Master, Tehsil/Police Directory, Collection, Enforcement, smart filters, bold borrower/status colours, Excel upload, sample Excel, CSV export, bulk allocation/status/delete, Case 360, Collection Payment/PTP/Visit ledgers, case timeline, documents/photos, WhatsApp handoff, Google Maps, Recovery Intelligence, Daily Report, user IDs/roles, PWA install support, PostgreSQL cloud mode, Railway `/healthz`.

## Existing data
The uploaded V64 database is packaged at `seed/kredansh_erp.db`. When cloud PostgreSQL is empty, the app migrates the existing banks, employees, Collection cases, Enforcement cases, allocation/ledger and user data.

## Deploy on Railway
1. Create a new Railway service from this folder/repository.
2. Add Railway PostgreSQL, or set `DATABASE_URL` to a PostgreSQL/Supabase server connection string.
3. Variables: `KREDANSH_SECRET=<long random secret>`, `CLOUD_MODE=true`, `MAX_UPLOAD_MB=30`.
4. Deploy. Healthcheck: `/healthz`.
5. Generate Public Domain. That URL works on Windows, Mac, iPhone and Android.

## iPhone / Android
Open public URL in Safari/Chrome → Add to Home Screen. It behaves like an installed app while using the same central database.

## Documents/photos
For permanent cloud uploads, mount a Railway Volume and set `UPLOAD_DIR` to that volume path. Otherwise deployment filesystem can be ephemeral.

## Important
Keep original KREDANSH V64 ZIP as backup until cloud data and permissions are verified. This is the online foundation; desktop-only OCR/GPS-photo text extraction should be moved to a server-safe OCR/storage service in a later hardening release.
