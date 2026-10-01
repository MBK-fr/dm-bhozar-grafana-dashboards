# Darkmoon — Security Posture (Grafana)

A Grafana dashboard that visualises findings from [Darkmoon](https://github.com/ASCIT31/Dark-Moon),
an open-source (GPL-3.0) autonomous AI penetration-testing platform. Point it at your
Darkmoon data and get a security-posture overview: findings by severity, status and category,
new findings over time, and your most recent pentest campaigns.

![Darkmoon severity distribution](https://raw.githubusercontent.com/ASCIT31/darkmoon-grafana/main/docs/screenshots/severity-distribution.png)

## What it shows

| Panel | Source endpoint |
| --- | --- |
| Estate (projects / targets / campaigns / findings) | `/api/v1/dashboard/overview.json` |
| Findings by severity (donut) | `/api/v1/dashboard/overview.json` |
| Findings by status (exploited / confirmed / unconfirmed / remediated) | `/api/v1/dashboard/overview.json` |
| Findings over time by severity | `/api/v1/metrics/timeseries.severity.json` |
| Findings by category | `/api/v1/dashboard/overview.json` |
| Recent campaigns | `/api/v1/dashboard/overview.json` |

Every value is **safe metadata only** (severity, status, category, ids) — no evidence, secrets or tokens.

## Requirements

- Grafana 10.4+
- [Infinity datasource](https://grafana.com/grafana/plugins/yesoreyeram-infinity-datasource/)
  (`yesoreyeram-infinity-datasource`) — reads the Darkmoon JSON over HTTP.

## Setup

1. Install the Infinity datasource and add an instance (no auth needed for a static export;
   add your API token as a header for the live API).
2. Import `darkmoon-security-posture.json`.
3. When prompted, pick your Infinity datasource for **Darkmoon (Infinity)**.
4. Set the **Darkmoon API base URL** dashboard variable:
   - **Open-source CLI:** run a pentest with `FORMAT=json`, serve (or publish as a CI artifact)
     the exported findings JSON, and point the variable at that location. The open-source edition
     is the local CLI; it emits findings as JSON.
   - **Darkmoon Pro:** point the variable at your Darkmoon Pro API base. The live security-posture
     API and web dashboard are part of the paid Pro edition.

## Links

- Source & docs: https://github.com/ASCIT31/Dark-Moon
- Project site: https://dark-moon.org
