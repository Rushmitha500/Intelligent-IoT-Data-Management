### B-05 frontend cutover findings - 2026-08-04
### B-05 update – Dashboard live-data cutover

Status: Open

The frontend currently uses `sensorData1.json` through `useSensorData(true)`, causing sensor routes to depend on the same mock source. Time filtering, interval sampling, statistics and correlation are also calculated in the browser.

The shared environment successfully returned 61 `thingspeak-live` rows, but frontend integration and per-sensor differentiation are not yet verified. Statistics, correlation and anomalies depend on BDAI-10, while alerts and alert history depend on BDAI-11.

Exit evidence: Every sensor route must use an approved identifier, display distinct live data and remove supported mock dependencies.

