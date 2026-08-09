### B-05 frontend cutover findings - 2026-08-04
### B-05 update – Dashboard live-data cutover

Status: Frontend implemented and locally verified

AFI-15 removed `sensorData1.json` from the demo path and introduced a shared live API client. Dashboard routes now resolve channel `12397` to `thingspeak-live` and channel `1350261` to `thingspeak-1350261` by default. Both dataset names can be overridden with Vite environment variables.

The dashboard now includes loading, no-data, invalid-range and API error states, responsive charts, readable timestamps, channel identity and unit hints. Login and registration use the approved backend `username` contract; Remember Me and cross-tab logout are implemented. Social login is disabled and MFA/reset are not presented as functional until AFI-14/AFI-16 provide approved routes.

Remaining verification/blockers:

- BDAI-10 remains the owner of backend statistics, correlation and anomaly routes.
- BDAI-11 remains the owner of live alerts and alert-history routes.
- AFI-14/AFI-16 must approve password-reset and MFA endpoints before those actions can be enabled.
