# RetailPulse — Master Project Knowledge Base

> **Purpose:** Canonical handoff for any AI assistant, coding agent, or collaborator joining RetailPulse. Read this before making recommendations or changing files.
>
> **Last updated:** 2026-10-13  
> **Project status:** Planning and repository/data setup. The end-to-end pipeline has not yet been verified as implemented.  
> **Important:** This document captures known decisions and plans from the conversation. It does not prove files have been committed to GitHub or that code/features exist. Inspect the current repository and local workspace first.

---

## 1. Executive Summary

**RetailPulse — Retail Sales Intelligence** is a portfolio project intended to demonstrate a realistic, end-to-end retail data engineering and business intelligence workflow.

The simulated business receives retail sales exports from CRM/ERP-style source systems. Python ingests, validates, cleans, and transforms the data; SQL Server stores analytical tables; and Power BI provides business dashboards.

The data should be realistic but not expose sensitive real customer/company information. The sales foundation comes from a public Superstore sample dataset, while additional operational data (such as suppliers) can be fictional and designed to fit the same simulated business.

The goal is not merely to build a dashboard. The project should demonstrate robust ingestion, data quality, dimensional modeling, incremental processing, SQL analytics, testing, documentation, and business-facing reporting.

**Guiding principle:** Make the engineering and business workflow realistic, while clearly documenting the provenance of sample and fictional data. Do not claim fictional data came from a real company.

## 2. Project Goals

1. Build a repeatable Python ETL/ELT-style pipeline.
2. Simulate recurring monthly retail data exports.
3. Validate source data and produce useful quality reports.
4. Transform raw records into well-defined fact and dimension tables.
5. Load data into SQL Server with sensible duplicate handling and incremental processing.
6. Provide SQL queries for business analysis.
7. Build a polished Power BI dashboard on top of SQL Server.
8. Include automated tests, setup instructions, architecture documentation, and data dictionary.
9. Make the GitHub repository understandable to recruiters and technical reviewers.
10. Keep implementation achievable and avoid adding tools only for buzzwords.

### Potential business questions

- How are sales and profit changing over time?
- Which products, subcategories, and categories contribute most to revenue and profit?
- Which regions and customer segments perform best?
- Are there high-revenue products with weak or negative profitability?
- How does supplier delivery performance or supplier risk vary?
- If a coherent inventory dataset is added, where might stock or replenishment concerns exist?

Only report metrics supported by actual data. Do not imply that historical order data alone supports inventory-on-hand or stockout claims.

## 3. Technology Stack

### Planned core stack

- **Python** — pipeline and data-quality logic
- **Pandas** — CSV processing and transformations
- **SQL Server** — relational storage and analytics
- **SQL** — schemas, constraints, incremental load logic, analytical queries
- **Power BI** — business intelligence dashboards
- **Git and GitHub** — version control and collaboration
- **Automated tests** — pipeline/data-model quality checks

Consider orchestration, cloud storage, or AI-based analytics only after the core workflow is working. Choose additions based on a clear use case, available time, and cost. Avoid unnecessary paid APIs and infrastructure.

## 4. Dataset and Provenance

A dataset pack was prepared earlier in the conversation:

`superstore_sales_intelligence_dataset_pack.zip`

The original conversation provided this link:

[Download the prepared dataset pack](sandbox:/mnt/data/superstore_sales_intelligence_dataset_pack.zip)

This link is tied to the original conversation/session and may not work in another AI conversation. If unavailable, locate the ZIP on the user's computer or reattach it. Do not assume another AI can access this file automatically.

### Expected pack contents

```text
data/
├── raw/
│   └── SuperStore_Orders_original.csv
├── processed/
│   ├── fact_sales.csv
│   ├── dim_product.csv
│   ├── dim_customer.csv
│   ├── dim_geography.csv
│   └── dim_date.csv
├── synthetic/
│   ├── dim_supplier_synthetic.csv
│   └── bridge_product_supplier_synthetic.csv
docs/
├── README.md
├── data_profile.json
└── data_dictionary.csv
```

These are the expected contents of the previously prepared pack, **not a verified inventory of the current GitHub repository**. Inspect actual files and schemas before implementation.

### Known provenance details

- The source sales data is based on a public Superstore sample dataset.
- Its historical dates were shifted forward by 11 calendar years for demonstration.
- The original raw CSV was preserved unchanged in the prepared pack.
- Supplier records and product-supplier assignments are fictional/simulated.
- The original `sales` field contained commas and needed numeric parsing.
- `product_id` is not guaranteed to uniquely identify a product name. Product identity may require a composite or surrogate key based on `product_id`, `product_name`, `category`, and `sub_category`.
- The pack includes prepared fact/dimension CSVs, but those tables and their relationships must be validated from the actual files.
- The original sales data is not a complete real operational ERP database. Any new supplier, inventory, or operational data should be designed to relate coherently to the available sales data.

### Data-provenance practice

Use business-oriented folder names for operational structure, but transparently document which data is public sample data and which data is fictional. Do not misrepresent synthetic records as real observations.

## 5. Repository and Folder Design

Preferred business-oriented structure:

```text
retailpulse-sales-intelligence/
├── data/
│   ├── incoming/       # new monthly files awaiting ingestion
│   ├── raw/            # original source extracts
│   ├── processed/      # cleaned and modeled datasets
│   └── reference/      # master/reference data: suppliers, products, geography, etc.
├── src/
│   ├── collect_data.py
│   ├── validate_data.py
│   ├── transform_data.py
│   └── load_sql.py
├── sql/
│   ├── schema.sql
│   └── analytics_queries.sql
├── tests/
├── docs/
│   ├── architecture.md
│   ├── data_dictionary.md
│   └── data_quality.md
├── powerbi/
├── requirements.txt
├── .gitignore
└── README.md
```

This is proposed, not confirmation that all paths/files currently exist. Empty folders do not appear in GitHub until a file is added.

### Why these data folders?

- `incoming/`: files waiting to be processed.
- `raw/`: source files preserved as received.
- `processed/`: standardized/cleaned outputs and modeled tables.
- `reference/`: lookup and master data, such as supplier, product, or geography reference tables.

We decided not to make `synthetic/` a central operational folder name because the goal is a realistic business-oriented repository. However, documentation must still identify fictional data accurately. If the original prepared pack uses a `synthetic/` directory, move or copy the files into `data/reference/` in the project repo only after checking names, references, and scripts. Do not silently lose provenance.

### GitHub and data storage guidance

- Repository: https://github.com/shreshta714-polaris/retailpulse-sales-intelligence
- Owner: `shreshta714-polaris`
- Default branch: `main`
- It was originally empty when inspected earlier. Current contents must be rechecked.
- The user is a collaborator with push access; admin/maintain privileges were not reported.
- The user is working directly through GitHub web UI for now and plans to use Codex on another laptop for code implementation.
- Do not claim any file was uploaded or committed unless verified.
- GitHub browser uploads have a 25 MiB per-file limit. For larger files, use Git or another appropriate data storage approach.
- Do not commit credentials, passwords, real sensitive data, local database files, caches, virtual environments, or large recurring operational exports.
- GitHub should hold code, documentation, schemas, small sample/test data as appropriate, and reproducible setup instructions—not serve as the ongoing production ingestion drop zone.
- Do not repeatedly upload new monthly operational exports to GitHub. Keep runtime/incoming data local or in a future appropriate storage service.
- Include a `.gitignore` that excludes secrets, environment files, virtual environments, cache files, local logs, and large operational data as appropriate. Keep deliberately curated small demonstration fixtures only if useful.

## 6. Target Architecture

### Initial historical backfill

1. Use the prepared public Superstore dataset as the historical starting point.
2. Inspect its schema, row counts, date ranges, nulls, duplicates, types, and candidate keys.
3. Preserve the original raw source file.
4. Validate and transform data into documented analytical tables.
5. Load the tables into SQL Server.
6. Verify row counts, constraints, relationships, and analytical totals.

### Simulated monthly ingestion

1. New CSV exports are placed in `data/incoming/`.
2. The collector detects candidate files.
3. File-level checksums identify already processed files.
4. Validation checks required columns, data types, missing values, invalid values, and duplicate records.
5. Invalid records are reported and quarantined/rejected with reasons; the entire file should fail only when appropriate for the severity and agreed policy.
6. Transformation normalizes columns, types, dates, categories, and keys.
7. Valid data is loaded into SQL Server using transactions and a defensible idempotent/incremental strategy.
8. Processing metadata is recorded: filename, checksum, timestamps, status, row counts, accepted/rejected rows, and error summary.
9. Successfully processed raw files are archived or otherwise retained according to the agreed design.
10. Power BI refreshes from SQL Server when the environment supports it.

Monthly exports may contain only new records, cumulative records, or overlapping/updated records. Do not assume which model applies. File checksums prevent reprocessing an identical file, but they do not alone prevent duplicate business records across different files. Row-level keys and insert/update rules must be defined from actual source semantics.

The sample dataset may not have a stable unique order-line ID. Inspect it and propose a defensible key/reconciliation approach before coding.

### Suggested audit table

Consider a SQL table such as `etl_file_audit` with fields for:
- `file_name`
- `file_checksum`
- `received_at`
- `processed_at`
- `status`
- `rows_read`
- `rows_loaded`
- `rows_rejected`
- `error_summary`

Choose final names and types based on the SQL style and implementation design.

## 7. Data Model and SQL Server

Expected prepared analytical tables:
- `fact_sales`
- `dim_product`
- `dim_customer`
- `dim_geography`
- `dim_date`

Potential future tables:
- `dim_supplier`
- `bridge_product_supplier`
- inventory snapshots or transactions, only if a coherent inventory source is created
- ETL/file audit and data-quality results

### Modeling principles

- Inspect every CSV header and data type before writing a schema.
- Identify grain for each fact table.
- Identify candidate keys and verify uniqueness rather than assuming it.
- Use primary/foreign keys and constraints where appropriate.
- Prefer a documented dimensional model that Power BI can consume clearly.
- Avoid creating relationships merely because two columns have similar names.
- Define treatment for nulls, unknown members, invalid dates, negative quantities, discounts, returns, and duplicate records from the actual source semantics.
- Validate that fact-to-dimension joins do not unexpectedly multiply rows.
- Reconcile key business totals before and after transformation.
- Document surrogate keys and natural/composite keys.
- Use parameterized SQL and environment-based credentials. Never hardcode passwords.

### Analytics SQL

Create and document useful queries such as:
- monthly/annual sales and profit
- revenue and margin by category/subcategory/product
- regional performance
- customer segment performance
- top and bottom products by supported measures
- data quality and ETL audit summaries
- supplier delivery/risk metrics only where supported by the fictional data

## 8. Python Code Components

### `src/collect_data.py`
- Discover supported incoming files.
- Validate file type and basic readability.
- Compute checksum.
- Check processing history.
- Register the ingestion attempt.
- Move/archive originals only after the appropriate processing state is reached.

### `src/validate_data.py`
- Required-column checks.
- Type and parsing checks.
- Null and domain validation.
- Duplicate checks at file and business-key level.
- Invalid-row report and reason codes.
- Clear severity policy for warnings versus fatal errors.

### `src/transform_data.py`
- Normalize names and data types.
- Parse numeric and date fields safely.
- Standardize dimensions and keys.
- Produce outputs with documented grain and schema.
- Preserve source lineage where practical.

### `src/load_sql.py`
- Connect to SQL Server using environment variables/configuration.
- Load staging data.
- Validate row counts and constraints.
- Insert/update in a transaction.
- Support safe retries and idempotent behavior.
- Record outcomes in audit tables.

### Tests

Include tests for:
- valid input
- missing required columns
- malformed numeric/date values
- nulls in critical fields
- duplicate files/checksums
- duplicate business records across files
- partial invalid rows
- SQL load failure/rollback behavior where test infrastructure allows
- expected fact/dimension key uniqueness
- reconciliation of source versus loaded counts/totals

Do not implement all components in one huge change. Build, run, and review one milestone at a time.

## 9. Power BI Dashboard

Planned report pages:

1. **Executive Overview:** sales, profit, margin, valid order count, trend over time.
2. **Product Performance:** category/subcategory, top/bottom products, profitability and discount analysis.
3. **Customer & Geography:** customer segments, regional performance, trends and drill-downs.
4. **Supplier Performance:** only after the fictional supplier model is validated; define simulated measures clearly.
5. **Data Operations / Quality:** optional but useful; files processed, latest successful load, accepted/rejected rows, data-quality trend, pipeline status.

### Dashboard standards

- Define all measures and business terminology.
- Use consistent formatting and sensible slicers.
- Ensure totals match SQL.
- Avoid misleading inventory claims unless inventory data is actually built.
- Clearly state reporting period and sample-data provenance.
- Keep `.pbix` and other assets in Git only if size and repo policy permit; otherwise document how to obtain/build them.

## 10. README and Documentation Requirements

The repository README should include:
- Project overview and business problem
- Architecture diagram
- Technology stack
- Data sources and provenance
- Setup prerequisites
- Environment configuration without secrets
- How to run historical backfill
- How to place and process a monthly file
- SQL Server schema/setup steps
- How to connect/refresh Power BI
- Tests and validation steps
- Screenshots or demo, once available
- Current project status and limitations

Supporting docs:
- `docs/architecture.md`
- `docs/data_dictionary.md`
- `docs/data_quality.md`
- Key design decision records, especially source extract behavior, key strategy, and incremental loading semantics.

Keep documentation accurate to what is implemented. Label planned features as planned, not completed.

## 11. Project Status and Collaboration Workflow

### Known status at handoff

- Project name and core architecture are established.
- The dataset pack was prepared and a download link was provided in the original conversation.
- A README draft was provided in chat, but this does **not** prove it was committed.
- GitHub repo exists at the URL above.
- The user said they had downloaded the dataset pack.
- The user intends to use Codex on another laptop and wants to conserve Codex usage.
- The user is considering GPT-5.6 Sol in Codex if available; verify the actual model selector rather than assuming availability.
- The user wants ChatGPT to act as technical mentor/planner and Codex as the local coding agent.
- Current repository contents, local files, installed software, SQL Server setup, and Power BI state must be checked, not assumed.
- No working ETL pipeline, SQL Server model, or Power BI dashboard has been verified as complete in this conversation.

### Recommended collaboration cycle

1. User opens the local repository in Codex.
2. Codex inspects files only and returns a factual report.
3. User shares the report with ChatGPT.
4. ChatGPT reviews findings and gives prioritized recommendations.
5. User approves a small implementation milestone.
6. Codex implements that milestone and runs tests.
7. User shares diff, logs, and results.
8. ChatGPT reviews, helps debug, and updates this knowledge document if decisions materially change.

### Initial Codex instruction

> Inspect the RetailPulse repository and all available dataset files. Do not modify anything yet. Read the README, data dictionary, data profile, and CSV schemas. Report actual file inventory, column names, data types, row counts, date ranges, candidate keys, data-quality problems, and table relationships. Identify mismatches between the sales dataset and proposed supplier/inventory data. Recommend an implementation plan for Python ingestion → validation → SQL Server → Power BI. Do not invent columns or business rules. Wait for approval before implementing changes.

## 12. Cost and Tool-Usage Strategy

The user wants to conserve Codex usage.

- Use a lower-cost/mini model for straightforward inspection, documentation, and small SQL edits when suitable.
- Use a stronger coding/reasoning model for difficult architecture decisions, multi-file implementation, or complex debugging.
- Keep tasks scoped and ask for one milestone at a time.
- Avoid repeatedly asking an agent to reread or regenerate the entire project.
- Ask Codex to summarize findings, changed files, tests run, and unresolved issues.
- Prefer reproducible commands and focused diffs.
- Do not rely on model names in this document as a guarantee of availability; inspect the actual Codex model selector and current limits.

## 13. Definition of Done

- [ ] Repository structure is clean and documented.
- [ ] Data provenance is clear.
- [ ] Source CSV schema and quality are profiled.
- [ ] Historical backfill runs from documented instructions.
- [ ] Monthly file ingestion works repeatably.
- [ ] Duplicate-file and duplicate-record behavior is tested.
- [ ] Validation errors are reported and handled predictably.
- [ ] SQL Server schema and load logic work.
- [ ] Data model keys and relationships are validated.
- [ ] Business totals reconcile between source, SQL, and Power BI.
- [ ] Automated tests cover core success and failure cases.
- [ ] Power BI dashboard includes meaningful business insights.
- [ ] Setup, runbook, architecture, and data dictionary are complete.
- [ ] No credentials or sensitive data are committed.
- [ ] README clearly separates completed functionality from planned enhancements.
- [ ] A reviewer can clone the repo and understand how to reproduce the project.

## 14. Rules for Any Future AI Joining the Project

1. Read this document first.
2. Inspect the current repository and local files before assuming state.
3. Separate verified facts, plans, and recommendations.
4. Do not claim a file, commit, table, feature, or dashboard exists without evidence.
5. Do not fabricate schemas, business rules, source behavior, or test results.
6. Preserve public sample-data provenance and clearly disclose fictional operational data.
7. Do not start over unless there is a concrete reason.
8. Do not modify files before the user approves a plan when the task is inspection-only.
9. Prefer small, testable, reviewable changes.
10. Explain the reasoning behind important engineering choices.
11. Ask only for missing information that materially blocks progress.
12. Keep this document updated as architecture, decisions, and project status change.

**First action:** establish the actual state of the GitHub repository and local dataset, then inspect the data before writing implementation code.
