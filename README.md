# Retail Store Sales — Data Cleaning & Performance Analysis

A Tableau Prep and Tableau Desktop project examining how data-quality decisions affect retail reporting.

## Project files

| File | Purpose |
| --- | --- |
| [retail_store_sales.csv](retail_store_sales.csv) | Source sales data |
| [DM_project.tflx](DM_project.tflx) | Packaged Tableau Prep flow |
| [Output.hyper](Output.hyper) | Saved output extract |
| [Retail Sales Performance Dashboard.twb](Retail%20Sales%20Performance%20Dashboard.twb) | Tableau workbook |
| [Setup instructions](README_Instructions.txt.md) | Reconnecting local data sources |

## Review and reproduce

1. Download the repository and open `DM_project.tflx` in Tableau Prep Builder.
2. Inspect the input connection and reconnect it to the included CSV if the original path cannot be resolved.
3. Review each transformation and its row counts before running the output step.
4. Open the `.twb` file in Tableau Desktop and reconnect it to the output extract if necessary.

The workbook is a `.twb`, not a packaged `.twbx`; local extract connections may need updating.

## Cleaning decisions

The original project report records the profiling findings, transformation assumptions, and dashboard outcomes. Revenue reconstruction assumes `Total Spent = Price Per Unit × Quantity`. Missing discount flags are treated as false, missing item identifiers as unknown, and spelling variants are grouped.

These are explicit modelling assumptions. Review them against the intended business rules before reusing the output. Reported counts and totals describe the original project run and have not been independently recalculated in this documentation update.

## Profiling findings

The original report identified missing financial values and item identifiers, inconsistent date types, category spelling variants, and ambiguous discount flags.

## Transformation approach

1. Reconstruct a missing financial value from the other available fields where the revenue identity permits it.
2. Standardise category spellings and trim surrounding whitespace.
3. Convert transaction dates to dates and discount flags to Boolean values.
4. Retain otherwise valid transactions with unknown item identifiers.
5. Export the cleaned extract for category and monthly-revenue reporting.

## Reported outcomes

The project report describes recovery of more than 600 revenue records, aggregation into eight categories, and a dashboard showing more than $1.5 million in total revenue. Those figures are reported outcomes, not independently reproduced measurements. The total dashboard revenue should not be confused with the amount recovered through imputation.

## Project previews

![Initial data profiling](https://github.com/user-attachments/assets/68e15b83-b798-4f83-a05c-4d9ddba221db)

![Tableau Prep cleaning flow](https://github.com/user-attachments/assets/4fc36a0a-3799-4fa5-a4d6-0cc9d8c9a707)

![Retail performance dashboard](https://github.com/user-attachments/assets/3ab39e8c-949f-4ab5-8df6-a3dc1e4acef5)
