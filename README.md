# Revenue Concentration Risk — E-Commerce Channel Analysis
## The business question

Which marketing channels account for a disproportionate share of
total revenue-generating orders — and how concentrated is customer
acquisition across channels — so the CMO can approve a diversification
strategy before a single channel failure creates structural risk?

## Key finding

Social is the only channel breaching the 1.5× concentration threshold:
**36.1% of revenue** against a 20% fair share — 1.8× over-indexed.
$43.7M of revenue is tied to a single acquisition channel.

## Database & schema

E-Commerce database (SQLite). Join path:
`campaigns → campaign_touches → customers → orders → order_items`

## SQL techniques used

- CTEs (multi-step query chains)
- `SUM() OVER()` window function for revenue share %
- `NTILE(4)` for acquisition quartile ranking
- `CASE WHEN` with 1.5× threshold for concentration flagging
- `COALESCE` for NULL safety
- Anti-join pattern (`LEFT JOIN ... WHERE NULL`) for orphan detection

## Repo structure

```
sql/ annotated SQL queries (audit + 3 business queries)
results/ CSV output from each query
deliverables/ CMO deck, intelligence brief, executive summary
```

## Validation approach (Tier 3)

Every SQL file contains inline annotations:
AI prompt used · predicted output · clause-by-clause explanation
· actual result · any catches · confidence rating.

## Results summary

| Channel | Rev Share | Acq Share | Fair Share | Flag |
|---------|-----------|-----------|------------|------|
| Social | 36.1% | 23.9% | 20% | Monitor |
| Paid Search | 20.2% | 21.3% | 20% | Healthy |
| Direct Mail | 19.9% | 21.4% | 20% | Healthy |
| Display | 15.9% | 19.8% | 20% | Healthy |
| Email | 7.9% | 13.6% | 20% | Healthy |

## Recommendation

CMO should approve a channel diversification initiative: cap social
dependency to ≤25% of revenue within two quarters and reallocate
acquisition investment toward email (currently 7.9%) and display.
