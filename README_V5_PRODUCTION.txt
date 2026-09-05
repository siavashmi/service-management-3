SERVICE USAGE MANAGER V5 — PRODUCTION / RENDER

Architecture
- FastAPI web application
- Render paid Web Service
- Render managed PostgreSQL
- SQLAlchemy + psycopg
- Persistent database storage
- Production HTTPS session cookies
- CSRF protection
- Login + admin/user roles
- Audit logs
- Excel import/export
- Search, pagination, edit, delete
- /health health check

RENDER BLUEPRINT
The included render.yaml creates:
1) service-usage-manager-v5 web service
2) service-usage-manager-db PostgreSQL database
3) DATABASE_URL automatically wired from the database to the web service

Before first Blueprint sync, Render will ask for:
- INITIAL_ADMIN_USERNAME
- INITIAL_ADMIN_PASSWORD

Use a strong password. Do not commit credentials to GitHub.

REGION
The web service and database are configured for Frankfurt to keep the application/database on the same Render region and use Render's internal database connection.

DATABASE
The Blueprint provisions a paid PostgreSQL database with 15 GB initial storage and storage autoscaling enabled. You can change the compute/storage settings in Render later if needed.

DEPLOY
1. Extract this ZIP.
2. Put the files in a GitHub repository.
3. In Render choose New -> Blueprint.
4. Select the repository.
5. Review the resources and charges shown by Render.
6. Enter INITIAL_ADMIN_USERNAME and INITIAL_ADMIN_PASSWORD when prompted.
7. Sync/apply the Blueprint.
8. Wait until the database and web service are healthy.
9. Open the generated Render URL.
10. Log in with the initial admin credentials.

IMPORTANT
Do not deploy V5 on top of an existing Render service that is managed by another Blueprint. A Render resource should be managed by only one Blueprint.

LOCAL TEST
The application still falls back to SQLite when DATABASE_URL is not set, so it can be tested locally with run_windows.bat.

For production, DATABASE_URL is automatically supplied by Render and PostgreSQL is used.


V5.1 deployment fix: app.py now creates the static directory automatically, preventing Starlette startup failure if the static folder is missing from the Git repository. Ensure the full project (including templates/) is committed and pushed to GitHub.
