### Q3. Provide a report with all the unique product counts for each segment and sort them in descending order of product counts.

#### The final output contains 2 fields:
- segment
- product_count

```
SELECT 
segment, 
COUNT(DISTINCT(product_code)) AS Product_Count 
FROM dim_product
GROUP BY segment
ORDER BY product_count DESC ;
```

 <table>
        <tr>
            <th>Segment</th>
            <th>Product_Count</th>
        </tr>
        <tr>
            <td>Notebook</td>
            <td>129</td>
        </tr>
        <tr>
            <td>Accessories</td>
            <td>116</td>
        </tr>
        <tr>
            <td>Peripherals</td>
            <td>84</td>
        </tr>
        <tr>
            <td>Desktop</td>
            <td>32</td>
        </tr>
        <tr>
            <td>Storage</td>
            <td>27</td>
        </tr>
        <tr>
            <td>Networking</td>
            <td>9</td>
        </tr>
 </table>
