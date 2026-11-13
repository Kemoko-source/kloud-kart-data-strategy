# Kloud Kart — Data Architecture & Strategy Lab

**Author:** Kemoko Foumba Traore  

**Context:** Operational Scaling, BI Centralization & Ghana Data Protection Act (Act 843) Compliance

## Overview
This repository contains the architectural diagnosis, decision records, strategic roadmap, and board presentation prepared for Nana and the Kloud Kart leadership team. The proposed architecture decouples analytical workloads from production transactions via a read replica, standardizes metrics through an SQL transformation layer, centralizes business intelligence, and enforces automated data deletion compliance under Ghana's Act 843.

## Repository Structure

```text
.
├── README.md
├── Kloud Kart Situation Diagnosis & Strategic Pivot.pdf
├── situation _diagnosis.md
├── recommendation_and_roadmap.md
├── recommendation-beyond-brief.md
└── decisions/
    ├── ADR-001-read-replica.md
    ├── ADR-002-sql-transformation.md
    ├── ADR-003-centralised-bi.md
    └── ADR-004-act843-deletion.md