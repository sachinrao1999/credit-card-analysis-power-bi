# Model and refresh guide

## Current model

| Object | Grain / purpose |
|---|---|
| `credit_card` | One stored row per Client_Num; aggregated card/transaction values assigned to a reporting week |
| `customer` | One stored row per Client_Num; demographic and customer attributes |
| `Measure's Table` | Home table for six explicit measures |
| Automatic date table | Supports the corrected date's hierarchy |

The active business relationship is `customer[Client_Num]` to `credit_card[Client_Num]`, 1:1, with filtering in both directions. Both tables contain 10,108 rows and distinct client IDs. All client IDs match between the two business tables in the saved data. This is the actual model, not an inferred many-to-one star schema.

The report package contains embedded model data. Power Query reads local CSV files. A stored Power BI Service connection manifest is also present, but no live Service URL or external workspace access is included as a prerequisite in this repository. Behaviour on a new machine should be checked in Power BI Desktop; this review did not open Desktop or run a refresh.

## Open without refreshing

Download `Report/Credit_Card_Report.pbix` and open it with a compatible Power BI Desktop version. The imported tables exist inside the file. If a version/sign-in/connection message appears, inspect it rather than overwriting the data sources or replacing the model.

## Refresh using the original CSVs

Expected names:

- `credit_card.csv`
- `customer.csv`

The existing source steps reference an author-specific local Windows folder. Another person's machine will not normally have that folder.

1. Obtain the original CSV files and verify the column contract in [the data dictionary](Data_Dictionary.md).
2. Save both in a local folder you control.
3. Open **Transform data** in Power BI Desktop.
4. Select `credit_card`, inspect its Source step and change the file path using the step settings if available, or Advanced Editor.
5. Repeat for `customer`.
6. Preserve the date-cleaning steps only if the new CSV still has the same date-text convention. Inspect ambiguous dates before conversion.
7. Apply changes and compare the control totals in [Validation.md](Validation.md). A changed source can legitimately change totals; record the source version and explain differences.

The current query specifies 18 source columns for credit_card and 15 for customer, comma delimiter and UTF-8 encoding. Avoid replacing these CSVs with an exported cleaned model table without adapting the queries: calculated/renamed columns and date layouts differ.

## Service publishing

Uploading the PBIX to GitHub stores a downloadable report file; it does not publish an interactive Power BI report. Publishing to Power BI Service is a separate step. Refreshing local CSV data from the Service normally needs an appropriate reachable source/gateway configuration. No gateway, scheduled-refresh process, RLS implementation or interactive Service link is delivered here.
