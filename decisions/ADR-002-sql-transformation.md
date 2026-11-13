# ADR-002: Transform data using in-database SQL over managed SaaS

- **Status:** Accepted
- **Date:** 2026-11-12
- **Decision owner:** Lead Data Engineer

## Context

We need to clean our data and standardize the definition of "revenue." The current developer wants to buy BigQuery or Snowflake. We only have 40 GB of data and a strict budget for two data hires. 

## Decision

We will write our data transformations (cleaning and business logic) in standard SQL directly on the read replica, managed via scheduled, version-controlled scripts. We will not purchase a separate cloud data warehouse or managed ETL tool.

## Alternatives considered

### Alternative A: Buy a Modern Data Stack (e.g., Snowflake + Fivetran)

- **How it would work:** We pay a SaaS vendor to extract our MySQL data, load it into a cloud data warehouse, and transform it there. 
- **Why it is attractive:** It provides a slick web interface, automated alerts, and looks great on a developer's resume.
- **Why rejected:** Massive overkill for 40 GB of data. It introduces unpredictable consumption-based monthly bills that Finance will hate, and our two-person data team cannot reasonably operate and debug a multi-vendor stack if something breaks at 3:00 AM.

## Consequences

- **What this buys:** Zero software licensing fees and full control over our transformation logic using skills our team already has.
- **What this costs:** Manual oversight. We have to build our own scheduling scripts (cron jobs) and alerting if a query fails.
- **What it costs the client if I am wrong:** A SQL script fails silently, and Nana receives an empty or outdated report on Monday morning because we didn't have commercial alerting tools in place.
- **What would make me revisit this:** If Marketing asks us to ingest data from 10+ different external advertising APIs (like Meta or Google Ads) where writing custom extraction scripts becomes too time-consuming.

## What this survives

This plan survives typical e-commerce schema changes and the addition of internal operational tables. It does not survive a pivot to analyzing millions of unstructured clickstream log files.