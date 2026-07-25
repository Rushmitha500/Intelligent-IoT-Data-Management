# AFIR-04 – MVP Operations Runbook

## 1. Purpose

This runbook records the local setup and startup assumptions verified during AFIR-04 for the Intelligent IoT Data Management project.

## 2. Environment

Validated local environment:

- Node.js and npm
- PostgreSQL 18
- Database: `IoTDatabase`
- Backend: Node.js + Express
- Frontend: React + Vite
- Python 3.12 available for Python components

Default ports:

- Backend: `3000`
- Frontend: `5173`
- PostgreSQL: `5432`

## 3. Database Setup

Create the PostgreSQL database:

`IoTDatabase`

Apply the existing schema from:

`backend/src/db/schema.sql`

Configure local database values in:

`backend/.env`

Required database configuration includes:

- `DB_USER`
- `DB_PASSWORD`
- `DB_HOST`
- `DB_PORT`
- `DB_NAME`

Credentials and secrets must not be committed to Git.

During AFIR-04, PostgreSQL connectivity was successfully validated through backend dataset read and write operations.

## 4. Backend Setup

From the repository root:

```powershell
cd backend
npm install
npm start
```

Expected startup:

```text
Server running on http://localhost:3000
ThingSpeak polling started. Interval: 60000 ms
```

Verify the backend by opening:

`http://localhost:3000`

Expected response:

`Backend is running`

The backend currently starts even when ThingSpeak polling fails.

## 5. ThingSpeak Configuration

ThingSpeak polling starts automatically with the backend.

The current local environment is missing:

`THINGSPEAK_CHANNEL_ID`

Therefore, polling currently retries and fails while the Express backend continues running.

The code provides defaults for polling interval, retry count, retry delay, and dataset name.

A valid project ThingSpeak channel configuration is required before live ingestion can be validated.

## 6. Frontend Setup

Open a separate terminal from the repository root:

```powershell
cd new-frontend\frontend
npm install
npm run dev
```

The frontend was successfully validated at:

`http://localhost:5173`

The login interface renders successfully.

The backend should remain running on port `3000` during frontend integration testing.

## 7. Known Startup and Test Issues

The AFIR-04 baseline identified the following current issues:

- `GET /health` is defined in `app.js` but is not exposed by the normal `server.js` startup path.
- The existing smoke test references a stale `../BackendCode/app` path.
- The active backend `npm test` command is a placeholder.
- `GET /api/stream-names` currently fails because asynchronous PostgreSQL access is consumed synchronously by the service layer.
- `timeseries_long` contained no baseline data during validation.
- ThingSpeak cannot complete polling without a configured channel ID.
- Frontend and backend authentication flows are not currently aligned.
- Development JWT fallback secrets exist and should not be used for production configuration.

See `test-plan.md` for detailed validation results.

## 8. Recommended Startup Order

1. Start PostgreSQL.
2. Confirm `IoTDatabase` exists and the schema is applied.
3. Confirm local `backend/.env` database configuration.
4. Start the backend with `npm start`.
5. Confirm `http://localhost:3000` responds.
6. Start the frontend with `npm run dev`.
7. Open `http://localhost:5173`.
8. Monitor the backend terminal for integration errors.

Do not commit `.env`, passwords, JWT secrets, or API keys.