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

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>division</th>
      <th>product_code</th>
      <th>product</th>
      <th>Total_sold_quantity</th>
      <th>Rank_Order</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>N &amp; S</td>
      <td>A6720160103</td>
      <td>AQ Pen Drive 2 IN 1</td>
      <td>701373</td>
      <td>1</td>
    </tr>
    <tr>
      <td>N &amp; S</td>
      <td>A6818160202</td>
      <td>AQ Pen Drive DRC</td>
      <td>688003</td>
      <td>2</td>
    </tr>
    <tr>
      <td>N &amp; S</td>
      <td>A6819160203</td>
      <td>AQ Pen Drive DRC</td>
      <td>676245</td>
      <td>3</td>
    </tr>
    <tr>
      <td>P &amp; A</td>
      <td>A2319150302</td>
      <td>AQ Gamers Ms</td>
      <td>428498</td>
      <td>1</td>
    </tr>
    <tr>
      <td>P &amp; A</td>
      <td>A2520150501</td>
      <td>AQ Maxima Ms</td>
      <td>419865</td>
      <td>2</td>
    </tr>
    <tr>
      <td>P &amp; A</td>
      <td>A2520150504</td>
      <td>AQ Maxima Ms</td>
      <td>419471</td>
      <td>3</td>
    </tr>
    <tr>
      <td>PC</td>
      <td>A4218110202</td>
      <td>AQ Digit</td>
      <td>17434</td>
      <td>1</td>
    </tr>
    <tr>
      <td>PC</td>
      <td>A4319110306</td>
      <td>AQ Velocity</td>
      <td>17280</td>
      <td>2</td>
    </tr>
    <tr>
      <td>PC</td>
      <td>A4218110208</td>
      <td>AQ Digit</td>
      <td>17275</td>
      <td>3</td>
    </tr>
  </tbody>
</table>

