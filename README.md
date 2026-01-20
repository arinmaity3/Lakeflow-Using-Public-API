# Orchestrating Lakeflow Declarative Pipeline - Using Public API data source

This project ingests data from publicly available APIs and implements a medallion architecture (Bronze / Silver / Gold) using Lakeflow declarative pipelines. It also includes tooling and guidance to promote pipelines and Databricks assets to higher environments using Databricks Asset Bundles.

## Overview

- Ingest data from public APIs into a Bronze layer (raw landing) using Lakeflow declarative pipelines.
- Transform and cleanse data into a Silver layer for cleaned and standardized records.
- Aggregate and enrich into a Gold layer for analytics and downstream consumption.
- Package and promote Databricks notebooks, jobs, and configurations with Databricks Asset Bundle for deployment to staging/production.

## Key Concepts

- Lakeflow declarative pipeline: Define ingestion and transformation pipelines declaratively (YAML/JSON) so they can be executed reproducibly and tracked.
- Medallion architecture: Layered storage approach (Bronze → Silver → Gold) to separate raw ingestion from cleansing and business-level transformations.
- Databricks Asset Bundle: Package Databricks notebooks, jobs, clusters, and configurations for consistent promotion across environments.
- Promotion workflow: Use CI/CD and the Databricks CLI (or equivalent tooling) to move bundles from development → staging → production.

## Project Structure

- pipelines/ : Lakeflow pipeline declarations (ingest + transform job manifests).
- connectors/ : API connector code and configuration (clients, rate-limit handling, retries).
- notebooks/ : Databricks notebooks used for transformations, validation, and enrichment.
- infra/ : Deployment scripts and Databricks Asset Bundle configuration (bundle manifests, environment overlays).
- docs/ : Additional documentation, runbooks, and architecture diagrams.
- tests/ : Unit and integration tests for connectors and transformation logic.

## Getting Started

1. Clone the repository

```bash
git clone https://github.com/arinmaity3/Lakeflow-Using-Public-API.git
cd Lakeflow-Using-Public-API
```

2. Configure credentials and environment variables

- Store API keys, Databricks token, workspace URL, and target storage path in a `.env` or your secret manager.
- Example environment variables:

```env
API_BASE_URL=https://api.example.com
API_KEY=your_api_key
DATABRICKS_HOST=https://adb-xxxx.azuredatabricks.net
DATABRICKS_TOKEN=your_databricks_token
TARGET_STORAGE_PATH=abfss://container@storage.dfs.core.windows.net/lake
```

3. Define Lakeflow pipelines

- Edit or create pipeline declarations under `pipelines/` to configure ingestion schedules, target paths, and transformations.
- Pipelines should describe source connector, target Bronze/Silver/Gold destinations, schema expectations, and retry/backoff behavior.

4. Run pipelines

- Use the Lakeflow CLI (or your orchestration layer) to run pipelines locally or in CI/CD. See `docs/` for examples and runbooks.

5. Build and promote Databricks Asset Bundles

- Use the configuration in `infra/` to package notebooks and job definitions as an asset bundle.
- Deploy bundles to staging and production Databricks workspaces using the Databricks CLI or CI/CD pipelines.

## Medallion Layers

- Bronze: Raw API payloads stored as-is (partitioned by ingestion date). Minimal processing; store original payload + ingestion metadata.
- Silver: Parsed, cleaned, and normalized records with schema enforcement and light transformations (type casts, deduplication, standardized column names).
- Gold: Business-ready aggregates, enriched datasets, and curated tables optimized for analytics and downstream consumers.

## Best Practices

- Record raw payload and metadata in Bronze so data lineage and replayability are preserved.
- Keep transformations modular and idempotent; prefer declarative pipeline steps where possible.
- Validate schemas at Silver to catch API changes early.
- Use small, focused Databricks notebooks for transformations and orchestrate them via bundles/jobs.
- Automate promotion with CI/CD and use environment overlays for config differences (e.g., storage paths, cluster sizes).
- Implement observability: ingestion metrics, error alerts, and data quality checks.

## Testing & CI

- Unit test connectors and parsers.
- Integration test pipelines against a sandbox environment or mocked API endpoints.
- Validate Databricks asset bundles in a staging workspace before promoting to production.

## Contributing

Contributions, issues, and feature requests are welcome. Please open an issue or submit a pull request. Follow the repository's contribution guidelines when adding functionality or changing defaults.

## License

Specify project license here (e.g., MIT, Apache-2.0).

## Contact / Maintainer

- Maintainer: Arin Maity
- GitHub: https://github.com/arinmaity3/Lakeflow-Using-Public-API
