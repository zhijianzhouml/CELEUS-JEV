# Results JSON — schema 1.0

The canonical all-zero example is `data.json`. Keep all required fields. This version expects exactly four benchmark entries and USD-denominated costs.

## Top level

| Field | Meaning |
|---|---|
| `schemaVersion` | Keep `"1.0"`. |
| `isPlaceholder` | `true` for the supplied all-zero preview; set `false` for actual results. |
| `title` | Report title metadata. |
| `targetModel`, `targetVersion` | Target model and pinned model version. |
| `surrogateModel` | Cheap predictor identifier / version. |
| `runId`, `updatedAt` | Human-readable provenance for the reported run. |
| `confidenceLevel` | Interval confidence setting, e.g. 0.95; not a control that recomputes intervals. |
| `coverageScope` | Explain whether intervals are per metric or simultaneously valid. |
| `intervalMethod` | Name / version of the actual estimator and interval construction. |
| `costCurrency` | `"USD"` in this version. |
| `timeAggregation` | Explain aggregation; default is sum of separate benchmark-run wall times. |
| `links` | Valid HTTP(S) `paper`, `code`, and `documentation` links. |
| `benchmarks` | Four entries following the layout below. |

## Benchmark identity and counts

`id`: unique lowercase slug, up to 40 characters; use letters, digits, hyphens or underscores, starting with a letter.

`shortName`, `name`, `domain`, `icon`, `caseUnit`, `split`, `metric`, `notes`: strings. Supported icon names include `message`, `terminal`, `shield`, `card`; unknown icons use a generic grid.

`poolSize`, `evaluated`, `stoppingSample`: nonnegative integers, with `stoppingSample <= evaluated <= poolSize`.

`targetCIWidth`: prespecified target interval width. Initial 0 means not configured in this preview, not a recommended stopping threshold.

## Performance

```json
{
  "estimate": 0,
  "lower": 0,
  "upper": 0,
  "fullReference": 0,
  "referenceAvailable": false,
  "certified": false
}
```

Require `0 <= lower <= estimate <= upper <= 1`. The chart assumes a normalized [0,1] primary score. Do not pass an AUROC / F1 / other nonlinear metric interval under a CELEUS mean-score label without the corresponding valid construction and an explicit metric definition.

`fullReference` is an optional full-pool result; only shown for actual results when `referenceAvailable` is true. For the all-zero preview it is rendered as a placeholder reference marker.

## Resource estimates

Both `resources.costPerPoolCase` and `resources.secondsPerPoolCase` contain `celeus` and `full` objects:

```json
{
  "estimate": 0,
  "lower": 0,
  "upper": 0,
  "intervalKind": "pending"
}
```

Require nonnegative, finite values with `lower <= estimate <= upper`.

- `pending`: no validated result yet.
- `certified`: interval supplied by a justified certification procedure.
- `empirical`: an explicitly labeled empirical or repeated-run interval.
- `measured`: an exact observed reference point; set `lower == estimate == upper`.

**Units:** USD / full-pool case and seconds / full-pool case, respectively. Values are supplied by the upstream estimator. The UI never constructs these intervals from run totals.

These fields are distinct from total observed run costs and times. For a measured full-pool baseline, its per-case point should agree with the appropriate observed total divided by N. For a repeated-run / expected-cost analysis, explain the estimand and how it differs from the displayed particular run totals.

## Totals

| Field | Meaning |
|---|---|
| `fullCost` | Measured or explicitly estimated full-evaluation cost in USD. |
| `targetCost` | CELEUS-selected target inference costs, including billable retries under the chosen policy. |
| `surrogateCost` | Entire surrogate-pool inference cost, including appropriately priced local compute where applicable. |
| `overheadCost` | Additional evaluation / orchestration cost. |
| `fullSeconds` | Full-evaluation wall-clock time under a stated execution policy. |
| `celeusSeconds` | End-to-end CELEUS wall-clock time; include surrogate preparation and overhead. |
| `baselineKind` | `pending`, `measured`, or `estimated`. |
| `runKind` | `pending`, `measured`, or `offline_replay`. |

The dashboard computes the CELEUS total as the sum of the three cost components. It sums independent benchmark times for the overview; it does not infer concurrent suite runtime. Negative savings are displayed as negative.

## Run metadata

`apiCalls`, `retryAttempts`, `cacheHits`, `concurrency`, `randomSeeds`: nonnegative integers. They describe the reported experiment, not API limits or suggested configuration.

One case may cause multiple requests or multiple decisions. Do not replace `evaluated` with request count without redefining the evaluation unit.

## Export behavior

- JSON exports the entire dataset and configuration, even when a filter is active.
- CSV exports the currently filtered benchmark rows, with all precision, provenance, and accounting fields, regardless of the All metrics display toggle.
- Zero-placeholder exports retain an explicit placeholder flag.
- Undefined actual savings percentages are empty in CSV rather than invented percentages.
- Imported values are rendered as escaped text. External links are limited to HTTP(S).

## Publishing on GitHub Pages

`data.json` at the repository root is the public source of truth. After deployment,
this page reads it once on each page load using a relative same-site URL.
Update and commit `data.json` to publish new results without a build command.

Import JSON is a local browser preview only; it never modifies the repository.
Download JSON exports `data.json`, which the site owner may then upload to GitHub.
Do not put API keys, private datasets, or raw customer traces in this file.

Opening `index.html` with a file:// URL uses the embedded all-zero preview, not the
neighboring data.json. Use Import JSON for a local preview, or visit the deployed site.
