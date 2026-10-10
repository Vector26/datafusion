# Project Map

## Purpose
Apache DataFusion: an extensible SQL/DataFrame query engine in Rust, columnar (Apache Arrow), with planners and vectorized execution. This clone tracks `https://github.com/Vector26/datafusion` (upstream-style Apache DataFusion).

## Requirements
- Learn usage patterns, not necessarily contribute core engine changes first
- Work with realistically large **dummy** data (volume/stress), without production secrets
- Prefer paths that match how users embed DataFusion (SessionContext, file formats, SQL/DataFrame)

## Components
- `datafusion/` — core crates (engine, optimizer, physical plan, etc.)
- `datafusion-examples/` — runnable examples (`examples/dataframe/`, `data_io/`, `sql_ops/`, …)
- `datafusion-cli/` — interactive SQL CLI (if present in tree)
- Docs: https://datafusion.apache.org/ user guide + https://docs.rs/datafusion

## Main Flow
User code / CLI → `SessionContext` → register tables (CSV/Parquet/JSON/…) or in-memory batches → SQL or DataFrame API → logical plan → optimized physical plan → streaming Arrow results

Heavy dummy data likely path: generate Parquet/CSV on disk (or object store) → `register_parquet` / listing table → run aggregations/joins → optional EXPLAIN / metrics

## Data and Trust Boundaries
- Local files or in-memory Arrow; examples also show S3/HTTP object stores
- No auth in basic local learning path
- “Heavy” data = size/row-count stress; keep synthetic (no PII)

## Build and Deployment
- Rust toolchain (repo documents MSRV on crates.io badge)
- Examples: `datafusion-examples` crate (see repo README / contributor guide for `cargo run --example`)
- Full workspace build can be large; heavy generation/query benchmarks better on a machine with more RAM than 8GB local Mac

## Unknowns
- Learner’s preferred interface: Rust examples vs `datafusion-python` vs CLI only
- Target scale for “heavy” (rows, GB on disk, join width)
- Whether Vector26 fork differs from upstream for the learning path (remote shows recent upstream-style commits)
