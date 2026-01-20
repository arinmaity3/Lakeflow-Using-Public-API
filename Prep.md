# Interview Prep — Lakehouse + Databricks (Condensed & Structured)

Goal: a compact, consistent daily plan you can use to prepare or interview others. Each day includes core topics, a focused 1-hour scenario exploration with explicit questions, and a short "interviewer trap" to practise a concise answer.

---

## How to use this file
- Read the "Existing Topics" to refresh fundamentals.
- Spend ~1 hour on the "Scenario Exploration" questions—answer out loud or write quick notes.
- Practice the "Interviewer trap" to prepare for concise, opinionated answers.

---

## Day 1 — Lakehouse, Delta Core & Reliability
Core topics
- Lakehouse architecture
- Delta Lake ACID guarantees
- _delta_log, checkpoints
- Managed vs external tables
- Time travel, RESTORE, VACUUM
- Idempotent writes
- Small file problem
- Optimistic concurrency control & isolation levels
- Delete vectors (conceptual)

Scenario Exploration (1h) — answer out loud
1. Two jobs run MERGE on the same Delta table concurrently.
   - What happens internally?
   - Which job fails and why?
   - How do you design retry logic?
2. A pipeline re-runs the next day and doubles the data (it succeeded yesterday).
   - Where did idempotency fail?
   - How do you fix it without deleting data?
3. Someone runs VACUUM aggressively.
   - What breaks?
   - How do you recover?

Interviewer trap
- "Why doesn’t Delta need locks?"

---

## Day 2 — Data Modeling on the Lakehouse
Core topics
- Fact vs dimension tables; star vs snowflake
- Bronze–Silver–Gold layering
- SCD Type 1 & Type 2
- Late-arriving dimensions
- Surrogate vs natural keys
- Snapshot vs transactional facts
- Accumulating snapshot tables
- Audit columns; backfills & historical corrections

Scenario Exploration (1h)
1. Business changes revenue logic 6 months later.
   - Do you backfill?
   - Which layers change?
   - What do dashboards show during backfill?
2. Late-arriving dimension arrives after fact is published.
   - Do you update facts?
   - How to avoid double counting?
3. Regulator asks for "data as of last year, exactly how it was."
   - Which tables help?
   - Which modeling decisions matter?

Interviewer trap
- "Why didn’t you just denormalize everything?"

---

## Day 3 — Lakeflow Declarative Pipelines (DLT)
Core topics
- Live vs streaming tables
- Pipeline DAG & dependencies
- Expectations: expect / drop / fail
- Triggered vs continuous modes
- DLT vs classic Spark jobs
- Reprocessing in DLT
- Error quarantine patterns
- Cost considerations & debugging failed pipelines

Scenario Exploration (1h)
1. Bronze table violates expectations suddenly.
   - Stop the pipeline or continue?
   - Drop records or fail?
   - Who gets alerted?
2. You need to backfill 3 months of data.
   - Rerun the pipeline or other options?
   - How to avoid duplicating Gold output?
3. Pipeline succeeds but downstream table is wrong.
   - Debugging steps for DLT

Interviewer trap
- "When would you avoid DLT entirely?"

---

## Day 4 — Structured Streaming
Core topics
- Micro-batch execution
- Checkpointing & offsets
- Exactly-once semantics
- Output modes
- Watermarking & late data
- Stateful vs stateless operations
- State store growth & trigger intervals
- Stream-stream joins

Scenario Exploration (1h)
1. Streaming job restarts after crash.
   - How does Spark know where to resume?
   - What happens to in-flight data?
2. Late data arrives after watermark.
   - Is it dropped? Can you recover it?
3. State store grows endlessly.
   - Why? How to fix?

Interviewer trap
- "Exactly-once sounds fake. Prove it."

---

## Day 5 — Autoloader & Schema Evolution
Core topics
- Autoloader internals: file notification vs directory listing
- Schema inference vs hints
- Schema evolution vs enforcement
- Column mapping modes
- Corrupt/bad record handling; schema drift detection
- Breaking vs non-breaking changes
- Contract-based ingestion

Scenario Exploration (1h)
1. Upstream adds a new column unexpectedly.
   - What happens today? What should happen ideally?
2. Column type changes INT → STRING.
   - Should the pipeline fail? How to handle?
3. Upstream deletes a column.
   - How to prevent silent corruption?

Interviewer trap
- "How do you prevent schema drift without blocking delivery?"

---

## Day 6 — Performance & Cost Optimization
Core topics
- OPTIMIZE & Z-ORDER
- Partitioning strategies & file size tuning
- Adaptive Query Execution (AQE)
- Data skew & salting
- Broadcast joins
- Cache vs persist
- DBU cost drivers; cost attribution & monitoring

Scenario Exploration (1h)
1. Job runtime doubles, data volume unchanged.
   - Where to look first?
2. One partition takes 80% of job time.
   - Why? How to fix?
3. Finance complains about the Databricks bill.
   - What metrics to show? What to change first?

Interviewer trap
- "Why not just add more executors?"

---

## Day 7 — Databricks Asset Bundles & SDLC
Core topics
- Databricks Asset Bundles
- Environment promotion & CI/CD
- Parameterization & secrets management
- Infra-as-code mindset
- Rollback vs forward-fix
- Feature flags

Scenario Exploration (1h)
1. Bad code reaches prod and corrupts data.
   - Rollback or forward fix? Why?
2. Same pipeline behaves differently in dev vs prod.
   - Possible root causes & prevention
3. Secrets accidentally committed.
   - Immediate response & remediation steps

Interviewer trap
- "Why not just edit the prod notebook?"

---

## Day 8 — Unity Catalog, Security & Governance
Core topics
- Unity Catalog architecture: catalogs, schemas, tables
- Ownership model
- Row/column-level security; PII tagging
- Lineage & auditing
- Multi-workspace strategy; compliance readiness

Scenario Exploration (1h)
1. Analyst can see PII they shouldn’t.
   - Where did governance fail? How to fix?
2. Two teams need the same table with different access.
   - Design approach (views, row/col policies, catalogs)
3. Audit asks: "Who accessed this table last month?"
   - Can you answer confidently? What to instrument?

Interviewer trap
- "How do you balance security with usability?"

---

## Day 9 — End-to-End Databricks System Design
Core topics
- Batch + streaming pipeline integration
- Backfills & reprocessing strategies
- SLA vs freshness trade-offs
- Monitoring & alerting
- Retry strategies; cost vs performance
- Disaster recovery & failure-first design

Scenario Exploration (1h)
1. SLA missed for 3 consecutive days.
   - Root-cause analysis steps
2. Streaming source replays old data.
   - How to protect downstream tables
3. Entire region goes down.
   - What survives? What doesn’t?

Interviewer trap
- "What fails first at 10× scale?"

---

## Quick checklist for answers
- State the assumptions first.
- Explain the visible symptoms, the root cause, and a short remediation.
- Give a short-term fix and a longer-term preventive design.
- When possible, reference transactional guarantees, metadata (e.g., _delta_log), or tooling (DLT, Autoloader, Unity Catalog).

---

End of file.
