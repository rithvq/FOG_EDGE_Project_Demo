# Dashboard Guide for Faculty

Five simulated devices send readings to a Fog system for checking, storage and alerts.

## 1. Architecture Page

**This page shows the components and the direction in which data travels.**

```text
Edge Devices -> Edge Gateway -> Data Diode -> Fog System -> Dashboard
```

| Component | What it does |
|---|---|
| Edge Devices | Generate sample temperature, CPU, network, security and industrial readings. |
| Edge Gateway | Collects readings, assigns importance and reduces repetitive data. |
| Data Diode | Forwards data towards Fog through the configured one-way application path. |
| Fog System | Checks received data and evidence, stores results and creates alerts. |
| Dashboard | Displays Fog-side information for review. |

**ACTIVE / HEALTHY** indicates recent activity or a successful check.
**STALE** means old information; **UNKNOWN** means insufficient status information.

The cards summarize traffic, delays, waiting messages and alerts.
**Inspect Edge node** shows an individual device's activity.

## 2. Evidence Coverage Page

**This page shows whether received evidence supports a monitoring decision.**

For example: "Did any accepted temperature reading reach 38 degrees Celsius in
this 10-second period?"

| Result | Meaning |
|---|---|
| TRUE | Evidence confirms a match, such as a reading of 40 degrees. |
| FALSE | Enough evidence confirms no match in the covered readings, not that the whole network is safe. |
| UNKNOWN | Evidence is insufficient, so Fog cannot decide. |

### Main Indicators

- **Evidence received:** Size of completed received summaries. **B means bytes**, not readings.
- **Evidence / forward bytes:** Sender-reported share of its forwarding budget used for evidence; separate from the page's filters, not confirmed receipt.
- **Definite-decision yield:** Percentage of selected results that are TRUE or FALSE, not accuracy.
- **UNKNOWN rate:** Percentage of selected results that cannot be decided.

**0 B and UNKNOWN rows can appear together:** Fog records "not enough evidence"
even when no complete summary arrives. The rows are decisions, not received readings.

**Device observation coverage** shows evidence availability and freshness, not
whether a device is switched on. **Inspect rule window** explains a chosen result.

## Main Research Idea

Before reducing routine readings, the Gateway preserves important rule facts and
reserves capacity to send their summary. This can support decisions despite raw
data loss. Missing evidence stays UNKNOWN rather than being treated as no incident.

This is a research prototype using synthetic readings and software separation,
not physical one-way hardware. Novelty and performance superiority are not established.

## What to Show During the Demo

1. Open **Architecture** and follow the arrows from devices to Fog.
2. Open **Evidence Coverage**. Choose the demo's time range and set filters to **All**.
3. Select a demo window and explain its TRUE, FALSE or UNKNOWN result.
4. Compare **raw-data loss with a supported TRUE** against **evidence loss producing UNKNOWN**.
5. Pause auto refresh to explain results; download JSON/CSV if needed.

Refreshing does not generate readings. Devices are idle between demo runs, so
idle periods may show UNKNOWN. See the [demo instructions](../novelty-roadmap/local-demo.md) for a fresh run.

