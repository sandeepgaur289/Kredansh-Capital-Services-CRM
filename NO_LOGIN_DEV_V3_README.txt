KREDANSH CAPITAL ERP - V3 NO LOGIN DEVELOPMENT BUILD

Purpose:
- Temporarily bypass all login/session gates.
- Open Dashboard directly.
- Allow unrestricted development/testing of Collection, Enforcement,
  Masters, Excel Import, Reports, Documents, Allocation and Case Updates.
- User Management and Logout are hidden from the sidebar.
- /login and /logout redirect to the Dashboard.

Build marker:
KREDANSH_NO_LOGIN_DEV_V3_2026_08_18

IMPORTANT:
This is a DEVELOPMENT BUILD. Do not treat it as final production security.
Once the operational portal is complete, role-based Login Panels will be
reintroduced with Admin / Manager / Collection / Enforcement / Viewer access.

Deployment:
1. Replace GitHub root app.py with this package's app.py.
2. Replace templates/base.html with this package's templates/base.html.
   Easiest option: upload this package structure over the current repository.
3. Commit changes.
4. Railway will redeploy automatically.
5. Check /healthz and confirm build marker.
6. Open the root URL; it should go directly to Dashboard.
