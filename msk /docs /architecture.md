# Technical Implementations & Optimizations

## 1. SQL Query Engineering
Legacy Kafka Connect queries often failed due to the way MSK appends incremental filters. I implemented a **Subquery Extraction Pattern** to ensure SQL syntax validity:
- **Legacy**: `SELECT * FROM table WHERE u_date > ...` (Failed on complex views)
- **Optimized**: `SELECT * FROM (SELECT <fields> FROM view ORDER BY id DESC) as t` (Successfully isolated the base data from the MSK pulse filter).

## 2. Staggered Pulse Ingestion
(Keep the existing description of the 5-minute stagger script here)
