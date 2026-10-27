# Validation of the supplied snapshot

The following checks were computed from decoded embedded tables and compared with the provided screenshots and report definitions. The PBIX was read, not modified. This review did not evaluate DAX in Power BI Desktop, execute the Power Query refresh or test interactions in a live report.

## Structure checks

| Check | Result |
|---|---:|
| credit_card rows | 10,108 |
| customer rows | 10,108 |
| Distinct Client_Num in credit_card | 10,108 |
| Distinct Client_Num in customer | 10,108 |
| Card-side clients missing from customer | 0 |
| Customer-side clients missing from card table | 0 |
| Null cells in decoded business tables | 0 |
| Minimum corrected reporting date | 2023-01-01 |
| Maximum corrected reporting date | 2023-12-24 |

Uniqueness supports the existing 1:1 relationship for this snapshot. It is not a guarantee about later data.

## Financial reconciliation

```text
Transaction amount       44,522,013.00
Annual fees               2,950,015.00
Interest earned           7,843,382.23
-------------------------------------
Project revenue metric   55,315,410.23
```

Transaction volume totals 655,651. Average customer satisfaction is 3.1892560348. The delinquency flag identifies 614 clients, or 6.0743965% of the matched 10,108-client population.

## Revenue by card category

| Category | Revenue |
|---|---:|
| Blue | 46,139,397.74 |
| Silver | 5,586,332.28 |
| Gold | 2,454,072.16 |
| Platinum | 1,135,608.05 |
| Total | 55,315,410.23 |

## Revenue by quarter

| Quarter | Revenue |
|---|---:|
| Q1 | 13,964,362.77 |
| Q2 | 13,820,566.72 |
| Q3 | 14,235,479.69 |
| Q4 | 13,295,001.05 |
| Total | 55,315,410.23 |

These quarters use the stored Qtr field. The report's quarter slicer uses a date hierarchy; validate their alignment after replacing or changing the date source.

## Display notes

The screenshots show rounded cards such as $55M, $45M, $8M, 656K, 10K and 3.19. They also use Indian-style digit grouping in a table despite dollar symbols. The README uses comma grouping and explicit two-decimal values for clearer comparison.

The supplied customer screenshot contains a week-51 hover tooltip. It is a screenshot state, not a filter definition or a report defect. A clean canvas export is a presentation improvement to make before a final portfolio launch.

## Checks for future changes

After a refresh, recheck key uniqueness, matching client sets, row counts, source/derived dates and control totals. If clients become repeated over time, revisit relationship cardinality, income aggregation, satisfaction weighting and delinquency rules before reusing the existing measures unchanged.
