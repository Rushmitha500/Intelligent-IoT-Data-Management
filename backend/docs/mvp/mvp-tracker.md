## Dashboard live-data mapping

Updated: 2026-08-09

The backend live-data path is working in the configured team environment. ThingSpeak data was saved to PostgreSQL, and `GET /api/datasets/thingspeak-live/series` successfully returned 61 rows.

| Widget                     | AFI-15 source/status | Live replacement/status       |
| -------------------------- | ------------------------ | ----------------------------- |
| Dataset cards              | Live channel cards for `12397` and `1350261` | Route-specific dashboard links |
| Stream selector            | Fields discovered from selected live series | `GET /api/datasets/:name/series` |
| Chart                      | Selected live series; responsive with timestamp labels | Live series API |
| Time range and interval    | Browser filtering with invalid/no-data states | Backend contract pending |
| Statistics and correlation | Live rows, calculated in browser | Backend route blocked by BDAI-10 |
| Anomalies and insights     | Not falsely populated | Blocked by BDAI-10/BDAI-11 |
| Latest alerts and history  | Not falsely populated | Blocked by BDAI-11 |

`sensorData1.json` and mock-first loading have been removed from the demo path. The API base URL and both channel dataset names are configurable using Vite environment variables.

Frontend verification on 2026-08-09: `npm run build` passed and `npm run lint` passed. Browser proof remains dependent on access to the shared live backend.

Local API testing returned HTTP 500 because the PostgreSQL password was rejected and `THINGSPEAK_CHANNEL_ID` was missing. This is a local environment issue; the shared backend live-data test passed.
