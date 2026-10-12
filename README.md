# Customer Shopping Behavior Analysis
 
End-to-end analytics project on 3,900 retail purchases. Python cleans the data, MySQL answers 10 business questions, and Power BI presents the results.
It aims to show which customer segments, discounts, subscriptions and shipping options relate to revenue and loyalty.

![Dashboard](dashboard.png)

## Project Files

| File | Description |
|---|---|
| `customer_shopping_behavior.csv` | Raw dataset (3,900 rows, 18 columns) |
| `Customer_Shopping_Behaviour_Analysis.ipynb` | Python cleaning, feature engineering and MySQL load |
| `Customer_Shopping_Behavior.sql` | 10 business-question queries (CTEs, window function, subquery) |
| `Customer_Behavior_Dashboard.pbix` | Power BI dashboard (preview: `dashboard.png`) |
| `Business Problem  Document.pdf` | Business brief and deliverables |
| `Customer Shopping Behavior Analysis.pdf` | Written project report |
| `Customer Shopping Behavior Analysis PPT.pdf` | Presentation deck |
| `LICENSE` | MIT License |

## Dataset

One row per customer (`Customer ID` is unique, 1 to 3,900). No duplicate rows.

| Column(s) | Description |
|---|---|
| Age, Gender, Location | Age 18–70; Male/Female; 50 US states |
| Item Purchased, Category | 25 items in Clothing, Accessories, Footwear, Outerwear |
| Purchase Amount (USD) | Order value, $20–$100 |
| Size, Color, Season | 4 sizes (S–XL); 25 colors; Spring to Winter |
| Review Rating | 2.5–5.0 (37 missing) |
| Subscription Status, Discount Applied, Promo Code Used | Yes/No flags (discount and promo columns are identical) |
| Shipping Type | 6 types, e.g. Express, Standard, Store Pickup |
| Previous Purchases | Prior purchase count, 1–50 |
| Payment Method, Frequency of Purchases | 6 payment types; 7 frequency labels (Weekly to Annually) |
| `age_group`, `purchase_frequency_days` | Derived in the notebook |

## Approach

1. **Understand** – load the CSV, check `info()`, `describe()` and nulls.
2. **Clean and engineer** – fill 37 missing ratings with the category median; snake_case names; drop `promo_code_used`; add `age_group` (quartile bins) and `purchase_frequency_days`.
3. **Analyse** – load into MySQL table `shopping_behavior`; run 10 SQL queries.
4. **Report** – build the Power BI dashboard, the written report and the PPT.

## Key Insights (recomputed from the CSV)

| Topic | Finding |
|---|---|
| Overall | $233,081 revenue; average purchase $59.76; average rating 3.75 (matches dashboard KPIs) |
| Gender | Male $157,890 vs Female $75,191. Males are 68% of customers; average spend is similar ($59.54 vs $60.25) |
| Category | Clothing $104,264 (45%), Accessories $74,200, Footwear $36,093, Outerwear $18,524 |
| Age group | Young Adult (18–31) leads at $62,143; Senior (58–70) is lowest at $55,763 |
| Subscription | 1,053 subscribers (27%) spend $59.49 on average vs $59.87 for non-subscribers |
| Shipping | Express $60.48 vs Standard $58.46 (+$2.02) |
| Discounts | 43% of purchases (1,677); top: Hat 50.0%, Sneakers 49.7%, Coat 49.1%, Sweater 48.2%, Pants 47.4% |
| Top rated | Gloves 3.86, Sandals 3.84, Boots 3.82, Hat 3.80, Skirt 3.78 |
| Loyalty | Loyal (>10 prior) 3,116 (79.9%), Returning (2–10) 701, New (1) 83 |
| Repeat buyers | 3,476 have >5 prior purchases; 958 (27.6%) subscribe vs 27.0% overall |
| Top sellers | Jewelry 171 (Accessories), Blouse/Pants 171 (Clothing), Sandals 160 (Footwear), Jacket 163 (Outerwear) |

## Tech Stack

- **Python** – pandas, SQLAlchemy, PyMySQL, Jupyter; median imputation, quartile binning, feature engineering
- **MySQL** – aggregations, CASE segmentation, CTEs, `ROW_NUMBER()` window function, subqueries
- **Power BI** – interactive dashboard with slicers and KPI cards

## How to Use

1. **Dashboard:** open `Customer_Behavior_Dashboard.pbix` in Power BI Desktop (or view `dashboard.png`).
2. **Setup:** install `pandas sqlalchemy pymysql jupyter` and create the MySQL database `customer_analytics`.
3. **Notebook:** set your MySQL credentials in `Customer_Shopping_Behaviour_Analysis.ipynb` and run all cells.
4. **SQL:** run the queries in `Customer_Shopping_Behavior.sql` in any MySQL client.
