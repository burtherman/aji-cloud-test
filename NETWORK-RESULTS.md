# Network check results

Run on 2026-11-10 from the Claude Code cloud session container, using
`curl -sS -o /dev/null -w "%{http_code}" -m 20 https://<host>`.

| Host | Result |
| --- | --- |
| www.federalregister.gov | **Blocked**: the egress proxy refused the connection (`CONNECT tunnel failed, response 403`) |
| api.usaspending.gov | **Blocked**: the egress proxy refused the connection (`CONNECT tunnel failed, response 403`) |
| opendata.dc.gov | **Blocked**: the egress proxy refused the connection (`CONNECT tunnel failed, response 403`) |

None of the three hosts could be reached. The agent proxy's status endpoint
classed each failure as `connect_rejected`, which is a refusal by the cloud
environment's network policy. The sites themselves did not reject the request.

To allow them, edit the cloud environment's **Network access** setting: either
choose a broader access level, or add these hosts under **Allowed domains**.
See https://code.claude.com/docs/en/cloud-environments#network-access.

This limit applies only to the build container. The "Latest from the Federal
Register" section in `index.html` fetches from the reader's browser, so the
container's policy does not affect it.
