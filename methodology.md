# FedSalary — methodology

For the canonical, always-up-to-date methodology page see <https://fedsalary.com/methodology>.

This summary is provided so the dataset is self-contained.

## Where the data comes from

Every cell traces to a primary publisher — the ministry, agency, or statute that has legal authority to set that pay rate. Aggregators, salary websites, and press summaries are excluded. Sources fall into three categories:

1. **Structured pay schedules** published as HTML/XML (e.g. OPM annual GS tables).
2. **PDF gazettes** published by a compensation ministry (e.g. DGAEP SRAP for Portugal, JPA Lampiran D for Malaysia).
3. **Statute texts** where pay is fixed directly in law (e.g. Malaysia Judges' Remuneration Act 1971, Spain Real Decreto 1314/2005).

## What "verified" means

A cell is verified when:
- (a) its source URL resolves to a publisher in the whitelist;
- (b) its value falls within the country's currency sanity band;
- (c) its step number is monotonically consistent with neighbouring steps in the same grade;
- (d) its movement from any prior verified value is within ±20%.

Verification does NOT mean a named human independently transcribed the number from the live source page on the date shown. Most cells were read once, by an automated parser against the cached source. Multi-column PDFs carry a small but non-zero risk of column-misalignment.

A plausible error rate, based on parser-quality across the dataset, is ~1-2% on clean typed sources and up to ~5% on multi-column PDFs.

## Anchor cells (regression detection)

For each country we ship a small set of hand-checked (grade, step, expected annual) tuples as "oracle" anchors. The audit script joins anchors against the live data and fails CI on drift. This catches both source-rate changes and parser regressions.

## Source provenance (content hashes)

Every source file cached during a pipeline run is SHA256-hashed and recorded in a manifest. The manifest lets any reader independently confirm that the specific bytes parsed match the ones whose hash was committed.

## Refresh cadence

Annual, May 15 each year, via an automated systemd timer.

## Errors and corrections

If a value here disagrees with the primary source you're citing, email <corrections@fedsalary.com> with the URL you checked, the expected value, and the date. Corrections within 48 hours or an inline explanation of the discrepancy.
