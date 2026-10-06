# e2e provider outage, October 2026

**Dates:** 2026-10-05 – 2026-10-06
**Scope:** why `e2e` went red on every model-issuing test, and what that showed
about the CI key, the free tier and the pinned agy.

## Observed

- Every model-issuing e2e turn failed with Gemini `503 UNAVAILABLE` ("This
  model is currently experiencing high demand") across the
  `gemini-3.{6,7,8}-flash-low` roster, for more than a day. `error_paths`, which
  calls no model, passed.
- On 2026-10-05, 3.7 Flash also hit
  `GenerateRequestsPerDayPerProjectPerModel-FreeTier` (limit 20/day) although
  no CI turn on it succeeded that day, so failed attempts most likely count
  toward the daily quota. agy retried each turn internally (errors reached
  "attempt 4"), multiplying requests. The 429's `retryDelay` pointed at a reset
  around 00:00 UTC.
- agy stays silent while it retries a 503 and ends the turn at its 5-minute
  print-mode timeout, so a harness deadline shorter than that reported a bare
  "Timed out" instead of agy's error.
- The last successful e2e run before the outage was 2026-09-11; none ran in
  between, so the start date of the outage is unknown.

## Direct API check (2026-10-06, same project's key, no agy)

- The key authenticates: listing models returns 200 and generation returns 200
  on some models. It is not a retired standard key.
- Availability was per model: 3.6 Flash answered 3 of 4 requests and 3.5
  Flash-Lite 4 of 4, while 3.7 Flash, 3.8 Flash and 3.1 Flash-Lite returned 503
  on every request.
- The Gemini API serves Flash-Lite models to this key; the `agy models` list
  captured in September offered none under an API key.

## Pinned agy is not fully pinned

CI installs agy CLI 1.1.26, but the language server it reports matched the
newest antigravity-cli release on each day: 1.2.17 on 2026-10-05 and 1.3.0 on
2026-10-06, both released those days. Releases from 1.2.12 stop retrying when
the Gemini API reports a daily or billing quota cap, which would avoid burning
quota during an outage.
