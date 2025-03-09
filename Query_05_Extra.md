
```
SELECT 
    fmc2020.product_code,
    fmc2020.manufacturing_cost AS manufacturing_cost_2020,
    fmc2021.manufacturing_cost AS manufacturing_cost_2021,
    (fmc2021.manufacturing_cost - fmc2020.manufacturing_cost) AS cost_difference
FROM fact_manufacturing_cost fmc2020
JOIN fact_manufacturing_cost fmc2021
ON fmc2020.product_code = fmc2021.product_code
AND fmc2020.cost_year = 2020
AND fmc2021.cost_year = 2021
ORDER BY fmc2020.product_code;
```
