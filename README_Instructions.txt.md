# Opening the Tableau Project

1. Download the repository files to a local folder.
2. Open `DM_project.tflx` in Tableau Prep Builder.
3. If an input connection is unresolved, select its input step and browse to the included `retail_store_sales.csv`.
4. Inspect transformation results and choose a local output location before running the flow.
5. Open `Retail Sales Performance Dashboard.twb` in Tableau Desktop.
6. If its extract connection is unresolved, point it to `Output.hyper` or the extract you just generated.
7. Refresh the views and verify totals.

The committed files are a packaged Prep flow (`.tflx`) and an unpackaged Desktop workbook (`.twb`). Paths stored by the original author may need updating. Preserve the source CSV and use a separate output location when experimenting.
