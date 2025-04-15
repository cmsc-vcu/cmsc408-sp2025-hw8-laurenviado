# 📊 World Bank Data SQL Analysis

This project explores and analyzes data from the World Bank’s World Development Indicators (WDI) using SQL queries. The dataset includes country-level information, development indicators, and metadata. Tasks involved data cleaning, transformation, and aggregation across multiple dimensions including income groups, regions, and time.

---

## 📁 Tables in Use

- **`wdi_country`** – Country-level metadata (region, income group, codes, etc.)
- **`wdi_data`** – Yearly indicator values per country
- **`wdi_series`** – Definitions and metadata for each indicator

---

## ✅ Skills Demonstrated

- Writing complex `SELECT`, `WHERE`, and `JOIN` statements
- Creating new tables using `CREATE TABLE AS`
- Performing `GROUP BY` aggregations and filtering with `HAVING`
- Calculating percentages and totals using subqueries and CTEs
- Constructing pivot-style cross tabulations

---

## 🧠 Sample SQL Snippets

### Filter out non-countries:
```sql
SELECT *
FROM world_bank_data.wdi_country
WHERE `Region` IS NOT NULL AND `Income Group` IS NOT NULL;
```

### Count countries by income group:
```sql
SELECT `Income Group`, COUNT(*) AS country_count
FROM wdi_country
WHERE `Region` IS NOT NULL AND `Income Group` IS NOT NULL
GROUP BY `Income Group`;
```

### Region-income cross tabulation:
```sql
SELECT 
  `Region`,
  SUM(CASE WHEN `Income Group` = 'High income' THEN 1 ELSE 0 END) AS High_Income,
  SUM(CASE WHEN `Income Group` = 'Upper middle income' THEN 1 ELSE 0 END) AS Upper_Middle,
  SUM(CASE WHEN `Income Group` = 'Lower middle income' THEN 1 ELSE 0 END) AS Lower_Middle,
  SUM(CASE WHEN `Income Group` = 'Low income' THEN 1 ELSE 0 END) AS Low_Income,
  COUNT(*) AS Total
FROM wdi_country
WHERE `Region` IS NOT NULL AND `Income Group` IS NOT NULL
GROUP BY `Region`;
```

---

## 📌 Key Lessons

- Not every record in the metadata is an actual country — filters must be applied to avoid overcounting.
- Venezuela is a valid country with missing income group, which needs manual fixing for accurate totals.
- Creating clean versions of tables is crucial for accurate downstream analysis.
- SQL can be used to generate not only flat reports but also formatted summary tables and pivot tables with calculated fields.

---

## 📅 Tools Used

- MySQL / MariaDB with SQLAlchemy connector
- Python (Jupyter/Quarto backend for rendering HTML from SQL)
- PHPMyAdmin (for manual verification and browsing of the database)

---

## 🏁 Final Thoughts

This assignment gave hands-on experience with real-world messy data, reinforcing why proper filtering, validation, and grouping logic is essential in data science work. The process mirrored common data-wrangling tasks in analytics and business intelligence roles.

