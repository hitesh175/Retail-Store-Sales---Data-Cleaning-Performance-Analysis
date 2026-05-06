**Retail-Store-Sales---Data-Cleaning-Performance-Analysis**
_______________________________________
1. Project Objective and User Definition
The User: National Sales Director of a retail chain.
The Objective: The user requires a clean, reliable dataset to analyse monthly revenue trends, identify top-performing product categories, and understand customer payment preferences.
The Problem: The raw "Dirty Retail Store Sales" dataset contained severe inconsistencies, missing financial data, and incorrect data types, making it impossible to calculate accurate revenue or plot time-series data. The goal of this cleaning process in Tableau Prep was to recover missing data logically and standardize text inputs to ensure 100% of the transaction volume could be utilized in the final Tableau Desktop dashboards.
________________________________________
2. Data Profiling Results (The "Before" State)
Upon loading the raw CSV into Tableau Prep, we utilized the profile pane to identify the following critical data quality issues:
1.	Missing Financial Data: Approximately 12% of the dataset (over 1,200 rows) contained null values in critical financial columns: Price Per Unit, Quantity, or Total Spent.
2.	Missing Identifiers: 10% of the records lacked a specific Item ID.
3.	Inconsistent Data Types: The Transaction Date was recognized as a String (Text) format rather than a temporal Date format.
4.	Text Inconsistencies & Typos: The Category column contained manual entry errors, resulting in duplicated categorical dimensions (e.g., "Furniture" and "Furniturre", "Patisserie" and "Patissery").
5.	Ambiguous Boolean Values: The Discount Applied column contained 33% null values.

<img width="940" height="466" alt="image" src="https://github.com/user-attachments/assets/68e15b83-b798-4f83-a05c-4d9ddba221db" />

 
Figure 1: Initial Data Profiling revealing severe data sparsity in financial columns.
________________________________________
3. Assumptions and Rules
To clean the data without artificially skewing the business metrics, our team established the following logical assumptions:
•	Assumption 1 (Financial Imputation): We assumed that the business logic Total Spent = Price Per Unit * Quantity is an absolute truth. Therefore, if one of these three values was missing, we could mathematically derive it from the other two rather than deleting the row and losing valid sales data.
•	Assumption 2 (Discount Ambiguity): If the Discount Applied field was null, we assumed that no discount was requested or given, treating the null as FALSE.
•	Assumption 3 (Unknown Items): If a transaction lacked an Item ID but contained a valid Category and Total Spent, we assumed the revenue was valid. We retained the row but labelled the item as "Unknown Item" to preserve the total category revenue.
•	Assumption 4 (Category Typos): We assumed minor spelling variations in the Category field were human entry errors intended for the primary category.
________________________________________
4. Data Cleaning Measures and Methodology
Based on our profiling and assumptions, we executed the following workflow in Tableau Prep to reach our target state:
1.	Calculated Field Imputation: We created calculated fields to repair the missing numerical data. For example, to fix missing totals, we used the formula: IFNULL([Total Spent], [Price Per Unit] * [Quantity]). This successfully recovered over 600 revenue records.
2.	Text Standardization: We utilized the Tableau Prep Group Values > Pronunciation algorithm on the Category column. This automatically identified phonetic similarities and merged typos (e.g., "Electonrics") into their correct parent category ("Electronics").
3.	Data Type Conversion: We changed the Transaction Date from a String to a Date type. We also converted Discount Applied to a Boolean (True/False) type, replacing nulls with FALSE.
4.	String Cleaning: We applied the Trim Spaces function to categorical columns to remove trailing spaces that could cause duplicate categories in Tableau Desktop.

 <img width="940" height="474" alt="image" src="https://github.com/user-attachments/assets/4fc36a0a-3799-4fa5-a4d6-0cc9d8c9a707" />

Figure 2: The final Tableau Prep cleaning pipeline.
________________________________________
5. Visualizing the Impact (The "After" State)
The output (.hyper extract) was imported into Tableau Desktop to validate the cleaning measures. The impact is clearly visible in the resulting dashboard:
•	Category Accuracy: The "Total Revenue by Product Category" bar chart correctly aggregates the sales into 8 distinct categories. Without the text grouping, this chart would have displayed fragmented, duplicated bars for misspelled categories.
•	Temporal Trend Analysis: Converting the String date to a true Date format allowed us to generate a continuous "Monthly Revenue Trend" line chart, providing the user with actionable insights over a three-year period.
•	Recovered Revenue: Because we imputed the missing Total Spent values instead of filtering out the rows, the dashboard accurately reflects over $1.5M in total revenue that would have otherwise been underreported.

 <img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/3ab39e8c-949f-4ab5-8df6-a3dc1e4acef5" />

Figure 3: Post-cleaning dashboard demonstrating functional time-series and categorical analysis.
________________________________________

