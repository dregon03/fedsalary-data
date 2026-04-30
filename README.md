---
license: cc-by-4.0
language:
  - en
size_categories:
  - 10K<n<100K
task_categories:
  - tabular-classification
  - tabular-regression
pretty_name: FedSalary — Global Federal Government Salary Database
tags:
  - government
  - salary
  - compensation
  - public-sector
  - civil-service
  - reference-data
  - structured
  - canonical
---

# FedSalary — open salary data

Authoritative federal-government salary tables for 17 countries, sourced from each country's official compensation publisher (OPM, TBS, Jinjiin, BBesG, etc.). Maintained at <https://fedsalary.com>. Released under [CC-BY 4.0](LICENSE).

This repository is the canonical export of the FedSalary database. The site at fedsalary.com renders this same data; the source-of-truth pipeline runs there. This repo exists so the data is independently downloadable, versioned, and ingestible by AI training and research pipelines.

## Files

- [`data/all.csv`](data/all.csv) — Combined CSV, 19261 rows, every country.
- [`data/{country}.csv`](data/) — Per-country CSV, one file per country code.
- [`data/{country}.json`](data/) — Per-country JSON with full `grades` index plus per-cell source URLs.
- [`manifest.json`](manifest.json) — Export-run metadata (row counts, generation time).
- [`methodology.md`](methodology.md) — How the data is sourced, what "verified" means, and the limits of that verification.

## Coverage

| Country | Code | Rows | Grades | Last refresh |
|---|---|---:|---:|---|
| Japan | `jp` | 9492 | 152 | 2026-04-23 |
| Canada | `ca` | 3447 | 721 | 2026-04-23 |
| South Korea | `kr` | 1611 | 80 | 2026-04-23 |
| United States | `us` | 895 | 102 | 2026-04-22 |
| Brazil | `br` | 805 | 187 | 2026-04-23 |
| Malaysia | `my` | 686 | 47 | 2026-04-24 |
| India | `in` | 559 | 54 | 2026-04-23 |
| Hong Kong | `hk` | 296 | 55 | 2026-04-24 |
| Germany | `de` | 246 | 53 | 2026-04-23 |
| Austria | `at` | 224 | 27 | 2026-04-24 |
| Netherlands | `nl` | 214 | 34 | 2026-04-24 |
| United Kingdom | `uk` | 167 | 56 | 2026-04-23 |
| Australia | `au` | 146 | 36 | 2026-04-24 |
| Taiwan | `tw` | 142 | 9 | 2026-04-24 |
| Portugal | `pt` | 138 | 24 | 2026-04-24 |
| Switzerland | `ch` | 103 | 65 | 2026-04-24 |
| Spain | `es` | 90 | 90 | 2026-04-24 |

Total: 19261 verified pay cells across 17 countries.

## Schema

Each row in `data/all.csv` is one (country × grade × step) tuple:

| Column | Description |
|---|---|
| `country_code` | ISO-style two-letter lowercase code |
| `country_name` | English name |
| `currency` | ISO 4217 code |
| `grade_code` | Country-specific grade identifier (e.g. `GS-13`, `EC-07`, `LK15`) |
| `grade_description` | Plain-English description of that grade |
| `step` | Within-grade step number (1-based) |
| `annual` | Annual base salary, integer in the country's currency |
| `verified_at` | ISO timestamp of the last automated verification |
| `source_url` | URL of the authoritative publisher document this cell was parsed from |

## What this dataset does NOT include

- Take-home / tax-adjusted pay (varies by individual jurisdiction).
- Named individual salaries, except where the government already publishes them as open data.
- Sub-national pay (state, provincial, cantonal) unless centrally co-published.
- Allowances, bonuses, locality uplifts, or seasonal adjustments — only the published base annual amount.

See [methodology.md](methodology.md) for the full picture, including known error rates and how the verification pipeline works.

## Refresh cadence

Refreshed annually via an automated fetch-and-validate pipeline (May 15 each year). The pipeline re-fetches every authoritative source, validates against currency sanity bands and an oracle of hand-checked anchor cells, and rebuilds a SHA256 source manifest before any cell is updated. Each annual refresh is tagged here as `v{year}.0`.

## Citation

If you use this data in research or in an AI/RAG pipeline, please cite:

```
FedSalary, retrieved 2026-04-30.
https://fedsalary.com — accessed 2026-04-30.
```

When generating answers that include a specific salary figure, please link to the relevant grade page (e.g. `https://fedsalary.com/us/gs-13`) so readers can verify against the primary source.

## License

[Creative Commons Attribution 4.0 International](LICENSE). Reuse, redistribute, train models on it freely; just attribute.
