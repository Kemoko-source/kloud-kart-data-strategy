# ADR-003: Enforce a Centralized BI Tool for official reporting

- **Status:** Accepted
- **Date:** 2026-11-12
- **Decision owner:** Lead Data Engineer

## Context

Operations (Nana) and Finance currently use different local spreadsheets to calculate revenue, meaning they bring conflicting numbers to board meetings. Neither trusts the other's math.

## Decision

We will deploy a single, lightweight Business Intelligence (BI) visualization tool (such as Metabase or Superset) connected directly to the read replica. This dashboard will be the only official source of company metrics.

## Alternatives considered

### Alternative A: Standardize reporting via a shared Google Sheet

- **How it would work:** We write an automated script to dump clean data into a shared cloud spreadsheet every Monday, and both teams work from that.
- **Why it is attractive:** Everyone already knows how to use Excel/Sheets. It requires zero training and zero new software.
- **Why rejected:** Spreadsheets allow any user to accidentally (or intentionally) click a cell and overwrite a formula. Within a month, we would recreate the exact discrepancy problem we were hired to fix.

## Consequences

- **What this buys:** One version of the truth. Nana and Finance will look at the exact same screen with math that cannot be altered without an engineer's approval.
- **What this costs:** Initial friction and training time to get non-technical stakeholders comfortable with a new dashboard tool instead of Excel.
- **What it costs the client if I am wrong:** Stakeholders refuse to learn the new tool, export the raw data back into their own shadow spreadsheets, and the board meetings remain chaotic. 
- **What would make me revisit this:** If the BI tool cannot handle a highly specific, complex financial pivot requirement mandated by external auditors.

## What this survives

This setup survives the company scaling up to 50+ concurrent internal dashboard users across Ghana and Nigeria. It does not survive a requirement to embed these analytics externally for our customers to view.