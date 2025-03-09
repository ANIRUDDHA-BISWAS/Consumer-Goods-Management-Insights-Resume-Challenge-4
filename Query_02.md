### 2. What is the percentage of unique product increase in 2021 vs. 2020? 
#### The final output contains these fields,
- unique_products_2020
- unique_products_2021
- percentage_chg

#### STEP_1:
```
SELECT
COUNT(DISTINCT product_code) AS UNIQUE_PRODUCTS
FROM fact_sales_monthly; 
```

 <table>
        <tr>
            <th>UNIQUE_PRODUCTS</th>
        </tr>
        <tr>
            <td>347</td>
        </tr>
</table>

```
SELECT
COUNT(DISTINCT product_code) AS UNIQUE_PRODUCTS_2020,
fiscal_year
FROM fact_sales_monthly
WHERE fiscal_year = 2020; 
```

<table>
        <tr>
            <th>UNIQUE_PRODUCTS_2020</th>
        </tr>
        <tr>
            <td>245</td>
        </tr>
</table>


```
SELECT
COUNT(DISTINCT product_code) AS UNIQUE_PRODUCTS_2021,
fiscal_year
FROM fact_sales_monthly
WHERE fiscal_year = 2021;
```

<table>
        <tr>
            <th>UNIQUE_PRODUCTS_2021</th>
        </tr>
        <tr>
            <td>334</td>
        </tr>
</table>


```
SELECT 
T1.Y_2020 AS UNIQUE_PRODUCTS_2020,
T2.Y_2021 AS UNIQUE_PRODUCTS_2021,
ROUND((Y_2021-Y_2020)*100/Y_2020, 2) AS CHANGE_PERCENTAGE
FROM 
(
	(SELECT
	COUNT(DISTINCT product_code) AS Y_2020
	FROM fact_sales_monthly
	WHERE fiscal_year = 2020) AS T1

CROSS JOIN

    (SELECT
	COUNT(DISTINCT product_code) AS Y_2021
	FROM fact_sales_monthly
	WHERE fiscal_year = 2021) AS T2
);
```
<table>
        <tr>
            <th>UNIQUE_PRODUCTS_2020</th>
            <th>UNIQUE_PRODUCTS_2021</th>
            <th>CHANGE_PERCENTAGE</th>
        </tr>
        <tr>
            <td>245</td>
            <td>334</td>
            <td>36.33%</td>
        </tr>
</table>







