### 4. Follow-up: Which segment had the most increase in unique products in 2021 vs 2020?
#### The final output contains these fields,
- segment product_count_2020
- product_count_2021
- difference

```
WITH Y_2021 AS (
    SELECT 
        dp.segment,
        COUNT(DISTINCT dp.product_code) AS Product_Count_2021
    FROM dim_product dp
    JOIN fact_sales_monthly fsm
    ON fsm.product_code = dp.product_code
    WHERE fsm.fiscal_year = 2021
    GROUP BY dp.segment
),

Y_2020 AS (
    SELECT 
        dp.segment,
        COUNT(DISTINCT dp.product_code) AS Product_Count_2020
    FROM dim_product dp
    JOIN fact_sales_monthly fsm
    ON fsm.product_code = dp.product_code
    WHERE fsm.fiscal_year = 2020
    GROUP BY dp.segment
)

-- LEFT JOIN to include all segments from 2020 and their corresponding 2021 values
SELECT 
    COALESCE(Y_2020.segment, Y_2021.segment) AS segment,
    COALESCE(Y_2020.Product_Count_2020, 0) AS Product_Count_2020,
    COALESCE(Y_2021.Product_Count_2021, 0) AS Product_Count_2021,
    COALESCE(Y_2021.Product_Count_2021, 0) - COALESCE(Y_2020.Product_Count_2020, 0) AS difference
FROM Y_2020
LEFT JOIN Y_2021
ON Y_2020.segment = Y_2021.segment

UNION

-- LEFT JOIN to include all segments from 2021 and their corresponding 2020 values
SELECT 
    COALESCE(Y_2020.segment, Y_2021.segment) AS segment,
    COALESCE(Y_2020.Product_Count_2020, 0) AS Product_Count_2020,
    COALESCE(Y_2021.Product_Count_2021, 0) AS Product_Count_2021,
    COALESCE(Y_2021.Product_Count_2021, 0) - COALESCE(Y_2020.Product_Count_2020, 0) AS difference
FROM Y_2021
LEFT JOIN Y_2020
ON Y_2021.segment = Y_2020.segment
ORDER BY difference DESC;
```

<table>
        <tr>
            <th>Segment</th>
            <th>Product Count 2020</th>
            <th>Product Count 2021</th>
            <th>Difference</th>
        </tr>
        <tr>
            <td>Accessories</td>
            <td>69</td>
            <td>103</td>
            <td>34</td>
        </tr>
        <tr>
            <td>Notebook</td>
            <td>92</td>
            <td>108</td>
            <td>16</td>
        </tr>
        <tr>
            <td>Peripherals</td>
            <td>59</td>
            <td>75</td>
            <td>16</td>
        </tr>
        <tr>
            <td>Desktop</td>
            <td>7</td>
            <td>22</td>
            <td>15</td>
        </tr>
        <tr>
            <td>Storage</td>
            <td>12</td>
            <td>17</td>
            <td>5</td>
        </tr>
        <tr>
            <td>Networking</td>
            <td>6</td>
            <td>9</td>
            <td>3</td>
        </tr>
</table>
