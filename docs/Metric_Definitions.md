# Metric definitions

This document describes the supplied PBIX as it exists. It does not silently replace measures with proposed alternatives.

## Financial and volume metrics

| Report label | Actual model calculation / visual aggregation | Unfiltered result |
|---|---|---:|
| Total Revenue | SUM of the calculated `credit_card[Revenue]` column | 55,315,410.23 |
| Total Transaction Amount | SUM of `credit_card[Total_Trans_Amt]` | 44,522,013 |
| Total_Trans_Count | SUM of `credit_card[Total_Trans_Vol]` | 655,651 |
| Total interest earned | SUM of `credit_card[Interest_Earned]` | 7,843,382.23 |
| Total customer | `DISTINCTCOUNT(customer[Client_Num])` | 10,108 |
| Income | SUM of `customer[Income]` | 575,914,439 |
| Satisfaction_Score | AVERAGE of `customer[Cust_Satisfaction_Score]` | 3.1892560348 |

`Revenue = Annual_Fees + Total_Trans_Amt + Interest_Earned` at the client-record level. Sum of annual fees is 2,950,015; adding this to transaction amount and interest reconciles to the revenue metric. Income describes customers' recorded income, not bank income. The source definition of income's time basis was not supplied.

Several headline visuals use implicit field aggregations rather than separate named measures. The DAX files therefore contain only the explicit measures and calculated columns actually present, not invented `Total Revenue` measure definitions.

## Delinquency rate

The actual measure filters `credit_card[Delinquent_Acc] = 1`, counts distinct related `customer[Client_Num]`, and divides by the visible distinct customer count. The active 1:1 relationship filters in both directions.

Under the current unfiltered one-row-per-client data, 614 / 10,108 = 6.0743965%, displayed as 6.07%. A 1 flag is treated as delinquent and 0 as non-delinquent for this project.

This is a client-level flag rate in the saved dataset. If future data contains repeated clients, account-level history or multiple records per week, first define the entity, reporting date and flag policy. The present measure is not automatically a historical delinquency-rate solution.

## Segmentation rules

| Field | Actual rule |
|---|---|
| AgeGroup `20-30` | Age < 30; the label is broader/narrower than a strict 20–30 inclusive band, so validate the source age domain |
| `30-40` | 30 <= age < 40 |
| `40-50` | 40 <= age < 50 |
| `50-60` | 50 <= age < 60 |
| `60+` | Age >= 60 |
| Income Group `Low` | Income < 35,000 |
| `Med` | 35,000 <= income < 70,000 |
| `High` | Income >= 70,000 |

Current decoded tables contain no null cells. The existing SWITCH expressions do not include an explicit leading blank-value test; review missing-value behaviour if future inputs contain blanks.

## Weekly calculations

- `Week_num 2` uses `WEEKNUM(credit_card[Corrected date's].[Date])` without an explicit return type.
- Current / previous / next week measures filter `ALL(credit_card)` to the maximum visible week number, that number minus one, or that number plus one.
- `WOW Change %` divides current-minus-previous revenue by previous revenue and uses the literal `"NA"` as the stored fallback expression.

The extracted expressions are preserved. They have not been reevaluated in a Power BI DAX engine during this documentation review. The full-fact-table ALL filter can clear more context than a narrow date filter; inspect slicer behaviour before relying on the weekly measures for a particular segment. Week-number arithmetic alone is not year-safe. There is no dedicated hand-authored calendar in this version; an automatic local date table supports date hierarchies.

The weekly line chart uses SUM of Revenue, `Week_num 2` and Gender; it does not directly plot the named current/previous/next-week measures.
