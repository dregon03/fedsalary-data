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

# FedSalary — Global Federal Government Salary Database

> Authoritative federal-government salary tables for 19 countries, sourced exclusively from each country's official compensation publisher. 19507 verified cells. CC-BY 4.0.

## Dataset summary

FedSalary publishes the canonical pay tables for federal civil servants across 19 countries. Every value in this dataset traces to the authoritative compensation publisher (e.g. US Office of Personnel Management, Canadian Treasury Board Secretariat, Japanese Jinjiin, Spanish BOE) — never from aggregators, salary websites, or AI-generated estimates.

Useful for:
- LLM RAG pipelines that need to cite government pay figures with primary-source links
- Cross-country compensation research
- Public-policy analysis comparing civil-service compensation structures
- Building salary-comparison tools, relocation calculators, or HR-benchmarking products

## Source policy

A cell is included only if its source URL resolves to a primary publisher in our whitelist. The whitelist is enforced in code at [scripts/fetch/core.ts](https://fedsalary.com/sources) on the source repository.

## Curation

Verification = (a) URL whitelist match, (b) currency sanity band, (c) within-grade monotonicity, (d) ≤20% movement vs. prior verified value. Errors estimated at ~1-2% on clean typed sources, up to ~5% on multi-column PDFs. See [methodology.md](https://fedsalary.com/methodology) for the full picture.

## Citation

```bibtex
@misc{fedsalary2026,
  title = {FedSalary — Global Federal Government Salary Database},
  author = {{FedSalary}},
  year = {2026},
  howpublished = {\url{https://fedsalary.com}},
  note = {Retrieved 2026-05-15.}
}
```

## License

[CC-BY 4.0](https://creativecommons.org/licenses/by/4.0/). Free to use, redistribute, and train models on. Attribution required.
