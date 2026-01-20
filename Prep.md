Day 1 – Lakehouse, Delta Core & Reliability
Existing Topics (unchanged)

Lakehouse architecture

Delta Lake ACID guarantees

_delta_log, checkpoints

Managed vs external tables

Time travel, RESTORE, VACUUM

Idempotent writes

Small file problem

Optimistic concurrency control

Isolation levels

Delete vectors (conceptual)

Scenario Exploration (NEW – 1h)

You must answer out loud:

Two jobs run MERGE on the same Delta table at the same time.

What happens internally?

Which one fails?

How do you design retry logic?

A pipeline ran successfully yesterday. Today it re-runs and doubles the data.

Where did idempotency fail?

How do you fix it without deleting data?

Someone runs VACUUM aggressively.

What breaks?

How do you recover?

Interviewer trap:
“Why doesn’t Delta need locks?”

Day 2 – Data Modeling on the Lakehouse
Existing Topics (unchanged)

Fact vs dimension tables

Star schema vs snowflake

Bronze–Silver–Gold modeling

SCD Type 1 & Type 2

Late-arriving dimensions

Surrogate vs natural keys

Snapshot vs transactional facts

Accumulating snapshot tables

Audit columns

Backfills & historical corrections

Scenario Exploration (NEW – 1h)

Business changes logic for revenue calculation 6 months later.

Do you backfill?

Which layers change?

What do dashboards show during backfill?

Late-arriving dimension arrives after fact is published.

Do you update facts?

How do you avoid double counting?

Regulatory audit asks for “data as of last year, exactly how it was.”

Which tables help?

Which modeling decisions matter?

Interviewer trap:
“Why didn’t you just denormalize everything?”

Day 3 – Lakeflow Declarative Pipelines (DLT)
Existing Topics (unchanged)

Live vs streaming tables

Pipeline DAG & dependencies

Expectations (expect, drop, fail)

Triggered vs continuous mode

DLT vs classic Spark jobs

Reprocessing in DLT

Error quarantine patterns

Cost considerations

Debugging failed pipelines

Scenario Exploration (NEW – 1h)

Bronze table violates expectations suddenly.

Do you stop the pipeline?

Do you drop records?

Who gets alerted?

You need to backfill 3 months of data.

Do you rerun the pipeline?

How do you avoid duplicating Gold?

Pipeline succeeds but downstream table is wrong.

How do you debug DLT?

Interviewer trap:
“When would you avoid DLT entirely?”

Day 4 – Structured Streaming
Existing Topics (unchanged)

Micro-batch execution

Checkpointing & offsets

Exactly-once semantics

Output modes

Watermarking & late data

Stateful vs stateless operations

State store growth

Trigger intervals

Stream-stream joins

Scenario Exploration (NEW – 1h)

Streaming job restarts after crash.

How does Spark know where to resume?

What happens to in-flight data?

Late data arrives after watermark.

Is it dropped?

Can you recover it?

State store grows endlessly.

Why?

How do you fix it?

Interviewer trap:
“Exactly-once sounds fake. Prove it.”

Day 5 – Autoloader & Schema Evolution
Existing Topics (unchanged)

Autoloader internals

File notification vs directory listing

Schema inference vs hints

Schema evolution vs enforcement

Column mapping modes

Corrupt/bad record handling

Schema drift detection

Breaking vs non-breaking changes

Contract-based ingestion

Scenario Exploration (NEW – 1h)

Upstream adds a new column unexpectedly.

What happens today?

What should happen ideally?

Column type changes from INT → STRING.

Does the pipeline fail?

Should it?

Upstream deletes a column.

How do you prevent silent corruption?

Interviewer trap:
“How do you prevent schema drift without blocking delivery?”

Day 6 – Performance & Cost Optimization
Existing Topics (unchanged)

OPTIMIZE & Z-ORDER

Partitioning strategies

File size tuning

AQE

Data skew & salting

Broadcast joins

Cache vs persist

DBU cost drivers

Cost attribution & monitoring

Scenario Exploration (NEW – 1h)

Job runtime doubles, data volume unchanged.

Where do you look first?

One partition takes 80% of job time.

Why?

How do you fix it?

Finance complains about Databricks bill.

What metrics do you show?

What do you change first?

Interviewer trap:
“Why not just add more executors?”

Day 7 – Databricks Asset Bundles & SDLC
Existing Topics (unchanged)

Databricks Asset Bundles

Environment promotion

CI/CD

Parameterization

Secrets management

Infra-as-code mindset

Rollback vs forward-fix

Feature flags

Scenario Exploration (NEW – 1h)

Bad code reaches prod and corrupts data.

Rollback or forward fix?

Why?

Same pipeline behaves differently in dev vs prod.

Root causes?

How do you prevent this?

Secrets accidentally committed.

What’s your response?

Interviewer trap:
“Why not just edit the prod notebook?”

Day 8 – Unity Catalog, Security & Governance
Existing Topics (unchanged)

Unity Catalog architecture

Catalogs, schemas, tables

Ownership model

Row/column-level security

PII tagging

Lineage & auditing

Multi-workspace strategy

Compliance readiness

Scenario Exploration (NEW – 1h)

Analyst can see PII they shouldn’t.

Where did governance fail?

Two teams need same table, different access.

How do you design this?

Audit asks: “Who accessed this table last month?”

Can you answer confidently?

Interviewer trap:
“How do you balance security with usability?”

Day 9 – End-to-End Databricks System Design
Existing Topics (unchanged)

Batch + streaming pipelines

Backfills & reprocessing

SLA vs freshness

Monitoring & alerting

Retry strategies

Cost vs performance

Disaster recovery

Failure-first design

Scenario Exploration (NEW – 1h)

SLA missed for 3 consecutive days.

Root cause analysis steps?

Streaming source replays old data.

How do you protect downstream tables?

Entire region goes down.

What survives?

What doesn’t?

Interviewer trap:
“What fails first at 10× scale?”
