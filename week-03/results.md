# Week 3 Results Summary: Stock Balance and Branch Performance

## Goal
Detect overstock and understock, measure branch throughput, and score branch performance.

## 1. Stock status
Of [N] products, [X]% ([count] products) are understocked with less than 1 month
of cover, worth about ₹[value] in stock value. [Y]% ([count]) are overstocked with
6+ months of cover, worth about ₹[value]. The remainder ([count]) are healthy.
(Note: corrected to use current_stock rather than opening_stock after an initial
column-matching error was found during review.)

## 2. Branch throughput
Branch [top branch] moves the most stock ([units] units), while branch
[bottom branch] moves the least ([units] units).

## 3. Branch performance score
Branch CHN001 scores highest (1.000), driven by the highest revenue (₹519 crore)
and strongest revenue-to-stock ratio (62.5), with no dead stock detected.
Branch HYD001 scores lowest (0.300), due to the lowest revenue-to-stock ratio
(44.5) despite moderate revenue (₹345 crore), meaning its stock converts to
sales less efficiently than other branches.

Score = 40% revenue + 30% revenue-to-stock ratio + 30% (1 − dead stock %),
each normalised 0-1 across branches. Weights are a starting assumption and can
be adjusted (e.g. weighting dead stock higher if shrinkage is a bigger concern).

## 4. Recommendation
Review HYD001's stock allocation against CHN001's, since CHN001 generates
nearly 50% more revenue from a similar stock value. Dead stock showed 0%
across all branches at a 180-day threshold; days_since_last_movement ranged
from [min] to [max], so [confirm this reflects genuine fast turnover / note
if data coverage is too short to produce meaningful dead-stock values].

## Limitations
- Months-of-cover thresholds (1 and 6 months) and the dead-stock threshold
  (180 days) are assumptions and can be adjusted.
- [Add anything else you noticed, e.g. missing branch capacity data.]


 taking the  reference of this notes prepare readme and  sprint notes of week 3
