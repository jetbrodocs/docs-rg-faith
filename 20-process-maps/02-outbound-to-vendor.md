---
title: "Process 02 — Outbound to Vendor (REMOVED)"
status: removed
created: 2026-02-07
updated: 2026-02-11
tags: [process, outbound, vendor, removed]
---

# Process 02 — Outbound to Vendor (REMOVED)

> **This process has been removed from system scope.** The system does not track the outbound dispatch of greige cloth to vendor mills. The process begins at inbound receipt (Process 02 — Inbound Receipt in the updated flow).

## Why Removed

Per second client meeting (2026-02-11):
- The system does not need to track outbound dispatches
- The MRL number is generated at inbound receipt, not at outbound
- Pending greige balance is captured as a vendor-reported note on the Gate Pass when material returns
- The outbound reference (Greige Challan No / L.R. No) is a vendor-side reference only

## What Replaced It

- **Inbound Receipt** is now the first process in the system
- The MRL number is generated when the first GRN is recorded
- Vendor's Gate Pass carries a note of total greige metres sent and pending balance — this is captured at inbound, not tracked from outbound

## Historical Context

This file originally documented the process of sending grey woven cloth to external vendor mills for dyeing and assigning the MRL Number. That process still happens physically, but the system does not track it.
