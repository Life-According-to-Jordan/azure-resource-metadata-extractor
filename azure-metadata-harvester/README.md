## Project Vision

Build a CLI-driven, extensible framework that can:

- **Extract** metadata from Azure “data stack” services (ADF, Logic Apps, Functions, Azure SQL, etc.)
- **Normalize** that metadata into consistent, queryable datasets
- **Analyze** metadata to identify redundancy, risk, and maintainability issues
- **Recommend actions** aligned with Microsoft best practices to support cleanup, standardization, and governance

The tool is intended to support both:
- **service-specific depth** (each Azure service has unique metadata semantics), and
- a **common evaluation model** that produces comparable outputs across services.

The project is **read-only by design** and does not deploy, mutate, or execute workloads.

---

## Project Goals

### Goal 1: Metadata Extraction (Foundation)

Establish a reliable, repeatable, and secure mechanism to harvest metadata from supported Azure services.

Initial focus is on **completeness and correctness**, not insight generation.

Canonical outputs include:
- `resources` — one row per Azure resource
- `objects` — service-specific child objects (pipelines, workflows, functions, databases, etc.)
- `relationships` — dependencies and references between resources and objects
- `raw_snapshots` (optional) — redacted JSON snapshots for audit and traceability

This stage provides the foundation required for all downstream analysis.

---

### Goal 2: Cross-Service Metadata Analysis

Once metadata extraction is stable, introduce a shared analysis layer capable of running across services using common detection patterns, such as:

- orphaned or unused components
- redundant or near-duplicate objects
- configuration drift and inconsistency
- missing operational controls (monitoring, tagging, ownership)
- standardization and consolidation opportunities

Analysis results are expressed as structured **findings**, not logs.

---

### Goal 3: Best-Practice Recommendations

Map analysis findings to **actionable recommendations** grounded in Microsoft guidance (e.g., service best practices, Well-Architected Framework).

Target outputs include:
- recommended action
- rationale and impact
- severity or priority
- evidence (the metadata that triggered the finding)
- references to Microsoft documentation (where applicable)

Recommendations are implemented per service but delivered through a consistent reporting model.

---

## Scope Strategy

### Why Azure Data Factory First

Azure Data Factory is the initial focus because it provides:
- consistent declarative definitions
- well-defined dependency graphs
- reusable components that enable meaningful analysis

ADF serves as the **reference implementation** for how deep metadata extraction and analysis should work.

The goal is not to build an ADF-only tool, but to establish a pattern that can be extended to other services.

---

## Progressive Service Expansion

Additional Azure services (Logic Apps, Azure Functions, Azure SQL, etc.) are incorporated using the same framework, with analysis depth tailored to what is structurally meaningful for each service.

Initial support for new services prioritizes:
- inventory and discovery
- configuration visibility (with secrets redacted)
- relationship mapping across services

Deeper analysis is introduced selectively as reusable patterns emerge.

---

## Design Principles

- Extraction before analysis
- Single framework, multiple service analyzers
- Service-aware logic with standardized outputs
- Explainable findings backed by concrete metadata
- Read-only and non-invasive
- Secure by default, with aggressive redaction

---

## Explicit Non-Goals

This project does **not** aim to:
- execute or orchestrate workloads
- replace Azure-native monitoring tools
- enforce policy or apply changes automatically
- ingest or store secrets
