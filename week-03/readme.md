# Stock Balance and Branch Performance Analysis

## Purpose

This project checks whether stock is balanced across branches and scores how well each branch turns its stock into revenue. It flags products that are likely to run out (understock) or sit too long (overstock), measures how much stock each branch moves, and ranks branches on a combined performance score.

## Questions answered

1. Which products are understocked, overstocked, or healthy, and what is the stock value in each group?
2. Which branches move the most and least stock?
3. Which branches convert stock into revenue most efficiently?
4. Where should stock allocation be reviewed?

## Inputs

- Product-level stock records with `current_stock` and `opening_stock` columns
- Branch-level sales and revenue figures
- Days since last stock movement, per product

Note: `current_stock` is the correct column for stock status. An earlier pass used `opening_stock` by mistake; this was caught in review and corrected.

## Method

### Stock status

Months of cover is calculated for each product. Products are grouped as follows:

| Status | Rule | Threshold |
|---|---|---|
| Understocked | Less than 1 month of cover | < 1 month |
| Healthy | Between the two thresholds | 1 to 6 months |
| Overstocked | 6 or more months of cover | >= 6 months |

Dead stock is any product with no movement for 180 days or more.

### Branch throughput

Units moved per branch, ranked from highest to lowest.

### Branch performance score

Each branch receives a score from 0 to 1, made from three components, each normalised across branches:

| Component | Weight | Meaning |
|---|---|---|
| Revenue | 40% | Total revenue for the branch |
| Revenue-to-stock ratio | 30% | How efficiently stock turns into sales |
| Dead stock | 30% | 1 minus the branch's dead stock percentage |

Score = 0.40 × revenue score + 0.30 × ratio score + 0.30 × dead stock score

The weights are a starting assumption. If shrinkage is a bigger concern, increase the dead stock weight.

## Current results (Week 3)

- Highest scoring branch: CHN001, score 1.000. Revenue ₹519 crore, revenue-to-stock ratio 62.5, no dead stock.
- Lowest scoring branch: HYD001, score 0.300. Revenue ₹345 crore, revenue-to-stock ratio 44.5.
- Dead stock was 0% across all branches at the 180-day threshold.

See `sprint-notes-week3.md` for the full summary and recommendations.

## Outputs

- Stock status summary (understocked, overstocked, healthy counts and values)
- Branch throughput ranking
- Branch performance score table
- Week 3 results summary

## Assumptions

- Months-of-cover thresholds (1 and 6 months) are assumptions and can be changed.
- The dead stock threshold (180 days) is an assumption and can be changed.
- Score weights (40/30/30) are a starting point, not validated against outcomes.
- Stock value is calculated from `current_stock`.

## Limitations

- Days since last movement are not yet verified against the full data range, so dead stock results may not reflect genuine slow movement. The minimum and maximum values should be checked before relying on the 0% result.
- Branch capacity data is not included, so throughput cannot be judged against capacity.
- Only one period is covered, so trends cannot be shown.

## Open items

- Confirm the range of days-since-last-movement values across all products.
- Add branch capacity data if available.
- Decide whether dead stock should carry a higher weight in the score.
- Add a second period to show trends.
