# Data dictionary

The fields below were observed in the supplied semantic model. Types describe the decoded values and are grouped into readable semantic categories; original source types and business definitions should be confirmed before a rebuild.

## credit_card

| Field | Type | Meaning |
|---|---|---|
| `Client_Num` | Integer | Client identifier; unique in each business table in this snapshot. |
| `Card_Category` | Text | Card category: Blue, Silver, Gold or Platinum. |
| `Annual_Fees` | Integer | Recorded annual card fees; component of the project revenue metric. |
| `Activation_30_Days` | Integer | Source activation indicator; confirm its 0/1 business definition with the dataset. |
| `Customer_Acq_Cost` | Integer | Recorded customer acquisition cost; not subtracted in the current revenue metric. |
| `Week_Num` | Text | Original source week label. |
| `Qtr` | Text | Original source quarter label. |
| `current_year` | Integer | Source year field. |
| `Credit_Limit` | Decimal number | Recorded credit limit. |
| `Total_Revolving_Bal` | Integer | Recorded revolving balance. |
| `Total_Trans_Amt` | Integer | Aggregated transaction amount per client record. |
| `Total_Trans_Vol` | Integer | Aggregated number of transactions per client record. |
| `Avg_Utilization_Ratio` | Decimal number | Recorded utilisation ratio; source averaging rules are not supplied. |
| `Use Chip` | Text | Usage mode category: Swipe, Chip or Online. |
| `Exp Type` | Text | Expenditure category. |
| `Interest_Earned` | Decimal number | Recorded interest earned; component of revenue. |
| `Delinquent_Acc` | Integer | Delinquency flag used as 1=delinquent in the report measure. |
| `Revenue` | Decimal number | DAX column: Annual_Fees + Total_Trans_Amt + Interest_Earned. |
| `Week_num 2` | Integer | DAX WEEKNUM of the corrected date, using the default week convention. |
| `Corrected date's` | Date/time | Imported date produced by splitting/reassembling source Week_Start_Date. |

## customer

| Field | Type | Meaning |
|---|---|---|
| `Client_Num` | Integer | Client identifier; unique in each business table in this snapshot. |
| `Customer_Age` | Integer | Recorded customer age. |
| `Gender` | Text | Source gender category. |
| `Dependent_Count` | Integer | Recorded number of dependants. |
| `Education_Level` | Text | Education category. |
| `Marital_Status` | Text | Marital-status category. |
| `state_cd` | Text | US state abbreviation used for mapping. |
| `Zipcode` | Integer | Postal code stored numerically in the current model; leading-zero handling may need review. |
| `Car_Owner` | Text | Source car-ownership category/flag. |
| `House_Owner` | Text | Source home-ownership category/flag. |
| `Personal_loan` | Text | Source personal-loan category/flag. |
| `contact` | Text | Source contact-method category; not a customer name field. |
| `Customer_Job` | Text | Occupation category; source labels retained. |
| `Income` | Integer | Recorded customer income; time-basis definition was not supplied. |
| `Cust_Satisfaction_Score` | Integer | Recorded satisfaction score; no external scale definition was supplied. |
| `AgeGroup` | Text | DAX age band; see Metric_Definitions.md for exact boundaries. |
| `Income Group` | Text | DAX income band: Low, Med or High. |

## Original versus derived fields

Original card input includes `Week_Start_Date`; the stored business table instead exposes the corrected date, plus DAX Revenue and Week_num 2. Customer input contains 15 columns; AgeGroup and Income Group are calculated columns. Original source files should not be replaced by these cleaned model columns without adapting Power Query.
