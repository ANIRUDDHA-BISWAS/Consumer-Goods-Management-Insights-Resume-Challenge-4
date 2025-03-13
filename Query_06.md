### Generate a report which contains the top 5 customers who received an average high pre_invoice_discount_pct for the fiscal year 2021 and in the Indian market. 
#### The final output contains these fields,
- customer_code
- customer
- average_discount_percentage


```
SELECT 
customer_code,
pre_invoice_discount_pct,
fiscal_year
FROM fact_pre_invoice_deductions
WHERE fiscal_year = 2021; 
```

```
SELECT 
AVG(pre_invoice_discount_pct),
fiscal_year
FROM fact_pre_invoice_deductions
WHERE fiscal_year = 2021; 
```

<table>
  <thead>
    <tr style="text-align: right;">
      <th>AVG_discount</th>
      <th>fiscal_year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0.233964</td>
      <td>2021</td>
    </tr>
  </tbody>
</table>



```
SELECT 
pid.customer_code,
pid.pre_invoice_discount_pct,
dc.market,
dc.customer,
pid.fiscal_year
FROM fact_pre_invoice_deductions pid
JOIN dim_customer dc
ON pid.customer_code = dc.customer_code
WHERE fiscal_year = 2021
AND pre_invoice_discount_pct > (SELECT 
								AVG(pre_invoice_discount_pct)
								FROM fact_pre_invoice_deductions
								WHERE fiscal_year = 2021)
AND dc.market = 'India'
ORDER BY pre_invoice_discount_pct DESC
LIMIT 5;
```

<table>
  <thead>
    <tr style="text-align: right;">
      <th>customer_code</th>
      <th>pre_invoice_discount_pct</th>
      <th>market</th>
      <th>customer</th>
      <th>fiscal_year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>90002009</td>
      <td>0.3083</td>
      <td>India</td>
      <td>Flipkart</td>
      <td>2021</td>
    </tr>
    <tr>
      <td>90002006</td>
      <td>0.3038</td>
      <td>India</td>
      <td>Viveks</td>
      <td>2021</td>
    </tr>
    <tr>
      <td>90002003</td>
      <td>0.3028</td>
      <td>India</td>
      <td>Ezone</td>
      <td>2021</td>
    </tr>
    <tr>
      <td>90002002</td>
      <td>0.3025</td>
      <td>India</td>
      <td>Croma</td>
      <td>2021</td>
    </tr>
    <tr>
      <td>90002016</td>
      <td>0.2933</td>
      <td>India</td>
      <td>Amazon</td>
      <td>2021</td>
    </tr>
  </tbody>
</table>



```
WITH avg_discount AS (
    SELECT AVG(pre_invoice_discount_pct) AS avg_pct
    FROM fact_pre_invoice_deductions
    WHERE fiscal_year = 2021
)

SELECT 
    pid.customer_code,
    pid.pre_invoice_discount_pct,
    dc.market,
    dc.customer,
    pid.fiscal_year
FROM fact_pre_invoice_deductions pid

JOIN dim_customer dc
ON pid.customer_code = dc.customer_code

CROSS JOIN avg_discount

WHERE pid.fiscal_year = 2021
AND pid.pre_invoice_discount_pct > avg_discount.avg_pct
AND dc.market = 'India'

ORDER BY pid.pre_invoice_discount_pct DESC
LIMIT 5;
```
