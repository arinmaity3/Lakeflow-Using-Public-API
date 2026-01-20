# Lakeflow - Using Public API

This project ingests data from publicly available APIs and implements a medallion (Bronze/ Silver/ Gold) architecture using Lakeflow declarative pipelines. It includes tooling to promote pipelines and assets to higher environments using Databricks Asset Bundles.

## Overview

- Ingest data from public APIs into a Bronze layer (raw landing) using Lakeflow declarative pipelines.
- Transform and cleanse data into a Silver layer for cleaned and standardized records.
- Aggregate and enrich into a Gold layer for analytics and downstream consumption.
- Manage and promote Databricks assets and notebooks using Databricks Asset Bundle for higher-environment deployments (e.g., staging, production).

## Key Concepts

- Lakeflow declarative pipeline: Define ingestion and transformation pipelines declaratively (YAML/JSON) so they can be executed reproducibly.
- Medallion architecture: Layered storage approach (Bronze -> Silver -> Gold) to separate raw ingestion from cleansing and business-level transformations.
- Databricks Asset Bundle: Package Databricks notebooks, jobs, and configurations for promotion across environments.

## Project Structure

- pipelines/ : Lakeflow pipeline declarations (ingest + transform jobs)
- connectors/ : API connector code and configuration
- notebooks/ : Databricks notebooks used for transformations and enrichment
- infra/ : Deployment scripts and Databricks Asset Bundle configuration
- docs/ : Additional documentation and runbooks

## Getting Started

1. Clone the repository

   git clone https://github.com/arinmaity3/Lakeflow-Using-Public-API.git
   cd Lakeflow-Using-Public-API

2. Configure API credentials and environment variables

   - Create a .env or use your secret manager to store API keys, Databricks token, workspace URL, and target storage path.
   - Example variables:
     - API_BASE_URL
     - API_KEY
     - DATABRICKS_HOST
     - DATABRICKS_TOKEN
     - TARGET_STORAGE_PATH

3. Define and run Lakeflow pipelines

   - Edit or create pipeline declarations under pipelines/ to configure ingestion schedules, target paths, and transformations.
   - Use the Lakeflow CLI or orchestration layer to run pipelines locally or in a CI/CD job.

4. Promote to higher environment with Databricks Asset Bundle

   - Use the asset bundle configuration in infra/ to package notebooks and job definitions.
   - Deploy bundles to staging and production Databricks workspaces with the Databricks CLI or CI/CD integration.

## Medallion Layers

- Bronze: Raw API payloads stored as-is (partitioned by ingestion date).
- Silver: Parsed, cleaned, and normalized records with schema enforcement and light transformations.
- Gold: Business-ready aggregates, enriched datasets, and tables for analytics or serving.

## Contributing

Contributions, issues, and feature requests are welcome. Please open an issue or submit a pull request.

## License

Specify project license here.
