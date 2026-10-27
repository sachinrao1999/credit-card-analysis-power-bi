# Source data

## Availability

The original source CSV files were not provided with the uploaded PBIX and screenshots, so they are not bundled in this repository package. The PBIX contains an imported snapshot of its business tables for the saved report.

To reproduce the source refresh, obtain the original:

- `credit_card.csv` — 18 source columns.
- `customer.csv` — 15 source columns.

See [the data dictionary](../docs/Data_Dictionary.md) and [refresh guide](../docs/Model_and_Refresh.md).

## Expected inputs

`credit_card.csv` headers:

```text
Client_Num,Card_Category,Annual_Fees,Activation_30_Days,Customer_Acq_Cost,Week_Start_Date,Week_Num,Qtr,current_year,Credit_Limit,Total_Revolving_Bal,Total_Trans_Amt,Total_Trans_Vol,Avg_Utilization_Ratio,Use Chip,Exp Type,Interest_Earned,Delinquent_Acc
```

`customer.csv` headers:

```text
Client_Num,Customer_Age,Gender,Dependent_Count,Education_Level,Marital_Status,state_cd,Zipcode,Car_Owner,House_Owner,Personal_loan,contact,Customer_Job,Income,Cust_Satisfaction_Score
```

The field inventory is reconstructed from the saved query/model metadata. Confirm the original files' exact header order before reuse; the query expects the documented field names and number of source columns. The original Week_Start_Date text was transformed during import, so retain/verify its original convention instead of guessing from the displayed date.

## Attribution and sharing

The original dataset publisher, download link and redistribution licence have not been established from the supplied files. Add the correct source attribution and licence terms before distributing separate CSVs. Do not describe these inputs as a verified public or synthetic dataset without confirming their origin.

The PBIX itself contains customer-level data. Sharing only PBIX does not remove the embedded data. Review whether the provided data is suitable and authorised for public sharing before making the repository public.
