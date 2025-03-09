### 5. Get the products that have the highest and lowest manufacturing costs. 
#### The final output should contain these fields:
- product_code
- product
- manufacturing_cost

```
WITH CostExtremes AS (

SELECT 
MAX(manufacturing_cost) AS max_cost, 
MIN(manufacturing_cost) AS min_cost 
FROM fact_manufacturing_cost
)

SELECT 
F.product_code, 
P.product, 
F.manufacturing_cost 
FROM fact_manufacturing_cost F 

JOIN dim_product P 
ON F.product_code = P.product_code

JOIN CostExtremes C 
ON F.manufacturing_cost = C.max_cost 
OR F.manufacturing_cost = C.min_cost

ORDER BY F.manufacturing_cost DESC;
```

<table>
        <tr>
            <th>Product Code</th>
            <th>Product</th>
            <th>Manufacturing Cost</th>
        </tr>
        <tr>
            <td>A6120110206</td>
            <td>AQ HOME Allin1 Gen 2</td>
            <td>240.5364</td>
        </tr>
        <tr>
            <td>A2118150101</td>
            <td>AQ Master wired x1 Ms</td>
            <td>0.8920</td>
        </tr>
</table>






