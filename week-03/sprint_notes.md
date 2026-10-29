# Sprint Notes: Week 3

**Theme:** Stock balance and branch performance
**Status:** Results drafted, pending data checks noted below

## Sprint goal

Detect overstock and understock, measure branch throughput, and score branch performance.

## What was done

- Classified products by months of cover (understocked under 1 month, overstocked at 6 months or more).
- Calculated stock value for each group.
- Ranked branches by units moved.
- Built a branch performance score from revenue, revenue-to-stock ratio, and dead stock.
- Checked dead stock at a 180-day threshold.

## Results

### Stock status

The summary shows the share of products and stock value in each group, using the same thresholds as the README. Fill in the final counts from the stock summary table before sharing.

### Branch throughput

Branch with the most units moved and branch with the fewest are listed in the summary. Fill in the branch names and unit counts from the throughput table.

### Branch performance

| Branch | Score | Revenue | Revenue-to-stock ratio | Dead stock |
|---|---|---|---|---|
| CHN001 | 1.000 | ₹519 crore | 62.5 | 0% |
| HYD001 | 0.300 | ₹345 crore | 44.5 | 0% |

CHN001 leads on revenue and conversion. HYD001 trails on conversion: its stock turns into sales less efficiently, even with moderate revenue.

## Decisions

- Use `current_stock` (not `opening_stock`) for all stock status and value calculations.
- Keep the score weights at 40% revenue, 30% revenue-to-stock ratio, and 30% dead stock as a starting point.
- Keep the 1-month and 6-month cover thresholds and the 180-day dead stock threshold for now.

## Issues found

- **Column mismatch:** The first pass used `opening_stock` for stock status. Caught in review and corrected to `current_stock`. Earlier figures from that pass should not be reused.
- **Zero dead stock everywhere:** 0% dead stock across all branches may be real, or it may mean the movement data window is too short. Needs a check.

## Recommendation

Review HYD001's stock allocation against CHN001's. CHN001 generates about 50% more revenue (₹519 crore vs ₹345 crore) from a similar stock value, so HYD001 may be holding stock that does not sell.

## Action items

| Item | Owner | Status |
|---|---|---|
| Confirm the min and max days since last movement across products | | Open |
| Confirm the 0% dead stock result reflects real turnover | | Open |
| Fill in stock status counts and values in the summary | | Open |
| Fill in top and bottom throughput branches and units | | Open |
| Review HYD001 allocation against CHN001 | | Open |
| Add branch capacity data if available | | Open |
| Decide whether to raise the dead stock weight | | Open |

## Risks

- Scores rest on assumed weights and thresholds. A different weighting could change the ranking of the middle branches.
- A single period cannot show whether HYD001's gap is growing or shrinking.

## Next sprint

- Validate the movement data window and the dead stock result.
- Add a second period to check whether the branch ranking holds.
- Test the score under two or three alternative weightings.
- Bring in branch capacity data to compare throughput against capacity.

## Limitations

- Months-of-cover and dead stock thresholds are assumptions and can be adjusted.
- Branch capacity data is not yet available.
