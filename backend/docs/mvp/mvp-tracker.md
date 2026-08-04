## Dashboard live-data mapping

Updated: 2026-08-04

The backend live-data path is working in the configured team environment. ThingSpeak data was saved to PostgreSQL, and `GET /api/datasets/thingspeak-live/series` successfully returned 61 rows.

| Widget                     | Current source           | Live replacement/status       |
| -------------------------- | ------------------------ | ----------------------------- |
| Dataset cards              | No confirmed integration | `GET /api/datasets`           |
| Stream selector            | Mock JSON fields         | Live `thingspeak-live` series |
| Chart                      | `sensorData1.json`       | Live series API               |
| Time range and interval    | Browser calculations     | Backend contract pending      |
| Statistics and correlation | Browser calculations     | Blocked by BDAI-10            |
| Anomalies and insights     | No live integration      | Blocked by BDAI-10/BDAI-11    |
| Latest alerts and history  | No live integration      | Blocked by BDAI-11            |

The frontend currently forces mock mode through `useSensorData(true)`. It also performs filtering, interval sampling, statistics and correlation locally. B-05 remains open until every sensor route uses an approved identifier and displays distinct live data.

Local API testing returned HTTP 500 because the PostgreSQL password was rejected and `THINGSPEAK_CHANNEL_ID` was missing. This is a local environment issue; the shared backend live-data test passed.
