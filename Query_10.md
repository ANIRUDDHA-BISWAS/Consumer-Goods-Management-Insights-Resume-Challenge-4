### 10. Get the Top 3 products in each division that have a high total_sold_quantity in the fiscal_year 2021? 

The final output contains these fields:
- division
- product_code
- product
- total_sold_quantity
- rank_order

```
WITH RankedSales AS (
    SELECT 
        dm.division,
        fsm.product_code,
        dm.product,
        SUM(fsm.sold_quantity) AS Total_sold_quantity,
        RANK() OVER (PARTITION BY dm.division ORDER BY SUM(fsm.sold_quantity) DESC) AS Rank_Order
    FROM fact_sales_monthly fsm
    JOIN dim_product dm 
        ON fsm.product_code = dm.product_code
    WHERE fsm.fiscal_year = 2021 
    GROUP BY dm.division, fsm.product_code, dm.product
)
SELECT 
    division, 
    product_code, 
    product, 
    Total_sold_quantity, 
    Rank_Order
FROM RankedSales
WHERE Rank_Order <= 3;  -- Get only top 3 products per division
```


