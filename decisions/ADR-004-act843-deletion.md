# ADR-004: Build an automated Act 843 Data Deletion Pipeline

- **Status:** Accepted
- **Date:** 2026-11-12
- **Decision owner:** Lead Data Engineer

## Context

We have 90 days to respond to a Data Protection Commission (DPC) complaint regarding a deleted customer. Currently, Marketing exports CSV lists of 300,000 customers onto local laptops, making it impossible to guarantee a customer’s data is fully deleted from our company under Ghana's Data Protection Act (Act 843).

## Decision

We will strictly ban the export of unmanaged PII (Personally Identifiable Information) to local CSV files. We will build an automated pipeline that permanently purges or anonymizes a requesting customer's data across all analytical systems within 5 working days.

## Alternatives considered

### Alternative A: Manual database SQL deletes upon request

- **How it would work:** Whenever Legal gets a deletion request, they email the developer, who manually writes and runs a `DELETE` SQL script against the database.
- **Why it is attractive:** It requires zero upfront engineering time to build an automated system. 
- **Why rejected:** It relies entirely on human memory. The developer might delete the customer from the main table but forget a backup table or a marketing list. This leaves us legally exposed and fails to generate the audit trail the DPC requires.

## Consequences

- **What this buys:** Ironclad legal compliance, protection from statutory DPC fines, and the closure of the active legal complaint.
- **What this costs:** Engineering time to build, test, and log the automated scrubbing routines, plus the loss of some historical customer attribute data for long-term analytics.
- **What it costs the client if I am wrong:** If the automated script fails silently, we lie to a regulator, exposing the board to severe statutory fines and potential criminal prosecution under Act 843.
- **What would make me revisit this:** If Ghanaian statutory data retention laws change (e.g., a new tax law that legally mandates we hold transaction records for 7 years, superseding privacy deletion requests).

## What this survives

This process survives standard customer churn and regular right-to-be-forgotten audits by the regulator. It does not survive a scenario where law enforcement legally mandates the preservation of a specific user's data for a fraud investigation.