# Remote Job Salary Aggregates (US-dollar pay, by role and region)

Snapshot of salaries in remote job postings, aggregated by role and region. Each row is a count of open
postings plus the 10th, 50th and 90th percentile of their pay. There are no individual postings, companies, links
or job descriptions in this dataset.

Compiled by [Remote Landers](https://remotelanders.com), a remote job board. Postings are collected from employers'
own careers pages.

## Files

`job_salary_aggregate_<YYYY-MM>.csv`, one file per snapshot. UTF-8, comma separated, one header row.

## Columns

| Column | Description |
| --- | --- |
| `snapshot_date` | Month of the snapshot, `YYYY-MM`. |
| `category` | Job role, e.g. `Software Engineer`, `Nursing`, `Account Executive`. |
| `region_scope` | Where applicants may be based: `US-only`, `Canada-only`, `Other-restricted` (any other country, or a list of several countries) or `Unspecified` (the posting does not say). Worldwide postings exist but are too few per role to form a row, so the value does not appear yet. |
| `listing_count` | Number of open postings in this row: same role, region scope and `salary_unit`. |
| `salary_p10`, `salary_p50`, `salary_p90` | 10th, 50th (median) and 90th percentile of pay, in US dollars. Empty when the row does not have enough independent pay data (see "Employer concentration" below). |
| `salary_unit` | `annual_usd` (yearly pay of full-time roles) or `hourly_usd` (hourly pay, any employment type). Hourly figures are not converted to yearly. |

## How the numbers are built

- **Population:** postings listed as open on Remote Landers on the snapshot date that state pay in US dollars.
  Postings in other currencies are left out, with no conversion. Internships are left out.
- **Pay per posting:** the midpoint of the stated minimum and maximum (or the single figure, if only one is given).
- **Units:** `annual_usd` covers yearly pay of full-time roles; full-time monthly pay is multiplied by 12 and
  counted here. Yearly or monthly pay of contract, part-time and temporary roles is left out, because a
  part-time monthly fee is not a yearly salary. `hourly_usd` covers hourly pay of any employment type.
- **Role:** one of the posting's role tags. A posting with several tags is counted once under each. Postings without
  a role tag are not in the file.
- **Outliers:** pay outside 12,000 to 1,000,000 USD a year, or 5 to 500 USD an hour, is excluded from the
  percentiles (not from `listing_count`).
- **Employer concentration:** some employers post many near-identical roles with the same pay. Postings from the
  same employer with the same pay count once in the percentiles, so one employer cannot set the market figure.
  Percentiles are published only when, after that, the row has at least 10 pay figures from at least 5
  employers and no single employer holds more than half of them. Otherwise they are left empty.
  `listing_count` still counts every posting.
- **Percentiles:** linear interpolation between sorted values.
- **Small groups:** rows with fewer than 5 postings are not published.

## Things to keep in mind

- **Only postings that state pay are included, so this is not a sample of all remote jobs.** Pay-transparent
  employers are more common in some places and sectors, and the data leans heavily towards US-only roles.
- **Stated pay is a posted range, not what people end up earning.** The midpoint of a range is not an offer or a
  salary.
- **Coverage is partial.** About 4 in 10 US-dollar postings are left out: no role tag, no pay period, an
  internship, or yearly/monthly pay on a non-full-time role (2,628 of 5,972 in the 2026-10 snapshot).
- **An empty percentile is not missing data by accident.** It means the row's pay comes from too few employers to
  stand for the market; `listing_count` is still accurate.
- **Small rows are noisy.** Check `listing_count` before reading anything into a percentile; rows with few postings
  move a lot between snapshots.
- **`Unspecified` is not the same as remote-anywhere.** It means the employer did not say where applicants can be
  based.
- **Roles are tagged automatically** from posting titles and text, so some postings will sit under the wrong role.
- **Rows are not additive.** A posting with several role tags appears in each of their rows, so summing
  `listing_count` over roles overcounts postings.

## Snapshots

| Snapshot | Rows | Rows with percentiles |
| --- | --- | --- |
| 2026-10 | 134 | 65 |

This is the first snapshot; later snapshots may be added. Rows can be compared across snapshots by `category`, `region_scope` and `salary_unit`.
A role/region that is missing from a snapshot was below the thresholds at that time.

## License and contact

This dataset is licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).
You may share and adapt it for any purpose, including commercially, as long as you credit "Remote Landers" and
link to https://remotelanders.com.

Suggested citation: Remote Landers, *Remote Job Salary Aggregates*, 2026-10 snapshot. https://remotelanders.com

Questions or corrections: contact@remotelanders.com
