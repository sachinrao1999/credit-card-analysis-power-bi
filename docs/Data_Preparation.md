# Data preparation performed in the supplied file

## credit_card query

1. Read `credit_card.csv` as comma-delimited UTF-8 data with 18 source columns.
2. Promote the first row to headers.
3. Assign initial types, including integer client IDs, annual fees, acquisition cost, activation and delinquency flags; keep `Week_Start_Date` as text initially.
4. Split `Week_Start_Date` on the hyphen into three parts.
5. Reassemble the parts in order 2, 1, 3 with `/` separators into the column named `Corrected date's`.
6. Apply final text/numeric types and parse the corrected date using `en-US`.
7. Add DAX calculated columns Revenue and Week_num 2 in the model.

This is the actual split-and-reassemble workflow in the file. Do not assume it is a universal date fix: it depends on the source layout. For a future version, an explicit confirmed locale conversion can be more maintainable.

## customer query

1. Read `customer.csv` as comma-delimited UTF-8 data with 15 source columns.
2. Promote headers.
3. Assign types for client ID, age, dependants, location, ownership flags, contact category, job, income and satisfaction.
4. Add DAX calculated columns AgeGroup and Income Group.

## Measures table

The file creates a dedicated `Measure's Table` through a small entered-data query with its placeholder column removed. Explicit measures are organised under that home table.

## What is not claimed

No SQL transformation script, source deduplication workflow, customer-history construction, production ETL pipeline, custom fiscal calendar or RLS role was established by the provided evidence. This documentation describes observable work rather than adding unverified tools to the portfolio.
