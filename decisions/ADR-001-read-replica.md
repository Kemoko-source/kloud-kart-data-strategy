# ADR-001: Route all reporting to a dedicated Read Replica

- **Status:** Accepted
- **Date:** 2026-11-12
- **Decision owner:** Lead Data Engineer

## Context

Orders, inventory, and customer accounts all live in one MySQL database that shares a server with the live website. When Operations runs heavy weekly reports on Monday mornings, it locks the database and slows the customer-facing shop to a crawl. We have a pre-approved second server available.

## Decision

All analytical reporting and data extraction will run exclusively against a dedicated MySQL read replica on the second server, permanently decoupling reporting from the live e-commerce shop.

## Alternatives considered

### Alternative A: Keep one database and schedule extracts at 02:00 AM

- **How it would work:** We rate-limit the CSV exports and schedule them to run automatically in the middle of the night when Ghanaian traffic is lowest.

- **Why it is attractive:** It requires zero new server setup, no replication monitoring, and no changes to the current architecture.

- **Why rejected:** We are piloting in Nigeria and plan to grow 15-20% YoY. As we expand across time zones and volumes increase, 02:00 AM will no longer be a safe "quiet zone." We need a physical boundary between analytics and the live shop, not just a time boundary.

## Consequences

- **What this buys:** Immediate stability for the live website. Nana can run a massive report at 09:00 AM on a Monday and customers won't notice a thing.

- **What this costs:** The monthly hosting fee for one extra server, and the engineering time to monitor replication health.

- **What it costs the client if I am wrong:** If replication lags behind production and we use the replica for stock counts, we will sell items we don't have, resulting in refund processing and angry customers. (Mitigation: Live stock verification remains on the primary database).

- **What would make me revisit this:** If replication lag consistently exceeds 5 seconds under peak Nigeria pilot load, or if the database grows past 500 GB.

## What this survives

This architecture survives order volumes doubling and the immediate launch of the Nigeria pilot within the same database topology. It buys us at least 1-2 years of runway before we need a true distributed cloud data warehouse.
