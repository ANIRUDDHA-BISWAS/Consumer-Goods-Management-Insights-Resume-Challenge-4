### 9. Which channel helped to bring more gross sales in the fiscal year 2021 and the percentage of contribution? 
The final output contains these fields,
- channel 
- gross_sales_mln 
- percentage

```
WITH total_sales AS (
    SELECT SUM(fsm.sold_quantity * fgp.gross_price) AS total_gross_sales
    FROM fact_sales_monthly fsm
    JOIN fact_gross_price fgp 
        ON fsm.product_code = fgp.product_code
        AND fsm.fiscal_year = fgp.fiscal_year
    WHERE fsm.fiscal_year = 2021
)
SELECT 
    dc.channel,
    CONCAT(FORMAT(SUM(fsm.sold_quantity * fgp.gross_price) / 1e6, 2), 'M') AS gross_sales_million,
    CONCAT(FORMAT((SUM(fsm.sold_quantity * fgp.gross_price) / (SELECT total_gross_sales FROM total_sales)) * 100, 2), '%') AS percentage_contribution
FROM fact_sales_monthly fsm
JOIN dim_customer dc 
    ON dc.customer_code = fsm.customer_code
JOIN fact_gross_price fgp 
    ON fsm.product_code = fgp.product_code
    AND fsm.fiscal_year = fgp.fiscal_year
WHERE fsm.fiscal_year = 2021
GROUP BY dc.channel
ORDER BY SUM(fsm.sold_quantity * fgp.gross_price) DESC;
```
