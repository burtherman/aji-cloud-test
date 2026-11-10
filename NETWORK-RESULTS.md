# Network check results

Latest run: 2026-11-10, from the Claude Code cloud session container, using
`curl -sS -o /dev/null -w "%{http_code}" -m 20 https://<host>`.

| Host | Result |
| --- | --- |
| www.federalregister.gov | **Reachable**: HTTP 302 (redirect from the home page) |
| api.usaspending.gov | **Reachable**: HTTP 200 |
| opendata.dc.gov | **Reachable**: HTTP 200 |

The Federal Register API was also checked directly:
`GET https://www.federalregister.gov/api/v1/documents.json?per_page=5&order=newest`
returned HTTP 200 with five documents and `access-control-allow-origin: *`, so
browsers on other sites can load it. A headless browser loading `index.html`
showed all five live documents in the "Latest from the Federal Register" section.

## Earlier run (same day)

An earlier check from this session found all three hosts blocked by the cloud
environment's network policy (`CONNECT tunnel failed, response 403`). The
environment's network settings have since changed to allow them.
