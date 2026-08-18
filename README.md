# KREDANSH CAPITAL ERP — CLEAN REBUILD V1

This is a fresh server-first rebuild. It does not reuse the old monolithic online app.

## Design goals
- Railway + PostgreSQL/Supabase
- One central database for Windows, Mac, Android and iPhone
- Modular Flask blueprints
- Dedicated `kredansh_v2` PostgreSQL schema, so old broken/public tables are not overwritten
- Automatic versioned schema migrations
- Login intentionally disabled during portal construction through `KREDANSH_DEV_NO_LOGIN=true`
- Official Kredansh logo included as a normal static asset using Flask `url_for`
- Bank Master, Employee Master, Collection, Enforcement, Directory, Dashboard
- Enforcement rule: Loan Number mandatory
- Rescheduled enforcement rule: New Physical Possession Date + Reason mandatory

## Deploy as NEW Railway project/repository
Do not overwrite the old repository. Keep it as backup.

1. Create a new PRIVATE GitHub repository: `Kredansh-ERP-Rebuild`
2. Upload the contents of this ZIP.
3. Railway -> New Project -> Deploy from GitHub.
4. Add environment variables:
   - `DATABASE_URL` = your Supabase Session Pooler URI
   - `SECRET_KEY` = a long random value
   - `KREDANSH_DEV_NO_LOGIN` = `true`
5. Railway redeploys automatically.
6. Open `/healthz`.
7. Expected build: `KREDANSH_REBUILD_V1_2026_08_18`
8. Open `/` for Dashboard.

## Important
The new application writes only to PostgreSQL schema `kredansh_v2`.
Your current Supabase public tables remain untouched until we deliberately migrate verified data.

## Next phases
1. Validate Masters + Case screens
2. Excel import/export
3. Case 360 + activity timeline
4. Collection PTP/payment/visit ledgers
5. Enforcement workflow engine + follow-up engine
6. Document/photo storage
7. MIS, Recovery Intelligence and reports
8. Reintroduce secure role-based authentication only after operational portal is stable


## V1.1 Health / Migration Architecture Fix

- `/healthz` is a pure liveness endpoint and always returns HTTP 200 while the web process is alive.
- `/readyz` separately checks PostgreSQL readiness.
- The migration ledger is bootstrapped before numbered migrations are queried.
- A temporary database/migration failure can no longer kill the Railway web deployment.
- Expected build marker: `KREDANSH_REBUILD_V1_1_2026_08_18`.

After deploy:
1. Open `/healthz` — must return status `ok`.
2. Open `/readyz` — should return `ready`.
3. If `/readyz` is degraded, fix DATABASE_URL/database only; the deployment itself remains online.
