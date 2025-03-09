### 7. Get the complete report of the Gross sales amount for the customer “Atliq Exclusive” for each month. This analysis helps to get an idea of low and high-performing months and take strategic decisions.
#### The final report contains these columns: 
- Month
- Year
- Gross sales Amount

```
SELECT 
    CONCAT(MONTHNAME(FS.date), ' (', YEAR(FS.date), ')') AS MonthYear,
    FS.fiscal_year,
    ROUND(SUM(G.gross_price * FS.sold_quantity), 2) AS Gross_sales_Amount
FROM fact_sales_monthly FS
JOIN dim_customer C 
    ON FS.customer_code = C.customer_code
JOIN fact_gross_price G 
    ON FS.product_code = G.product_code 
    AND FS.fiscal_year = G.fiscal_year
WHERE C.customer = 'Atliq Exclusive'
GROUP BY FS.fiscal_year, YEAR(FS.date), MONTH(FS.date), MonthYear
ORDER BY FS.fiscal_year, YEAR(FS.date), MONTH(FS.date);
```

<table>
  <thead>
    <tr style="text-align: right;">
      <th>MonthYear</th>
      <th>fiscal_year</th>
      <th>Gross_sales_Amount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>September (2019)</td>
      <td>2020</td>
      <td>4496259.67</td>
    </tr>
    <tr>
      <td>October (2019)</td>
      <td>2020</td>
      <td>5135902.35</td>
    </tr>
    <tr>
      <td>November (2019)</td>
      <td>2020</td>
      <td>7522892.56</td>
    </tr>
    <tr>
      <td>December (2019)</td>
      <td>2020</td>
      <td>4830404.73</td>
    </tr>
    <tr>
      <td>January (2020)</td>
      <td>2020</td>
      <td>4740600.16</td>
    </tr>
    <tr>
      <td>February (2020)</td>
      <td>2020</td>
      <td>3996227.77</td>
    </tr>
    <tr>
      <td>March (2020)</td>
      <td>2020</td>
      <td>378770.97</td>
    </tr>
    <tr>
      <td>April (2020)</td>
      <td>2020</td>
      <td>395035.35</td>
    </tr>
    <tr>
      <td>May (2020)</td>
      <td>2020</td>
      <td>783813.42</td>
    </tr>
    <tr>
      <td>June (2020)</td>
      <td>2020</td>
      <td>1695216.60</td>
    </tr>
    <tr>
      <td>July (2020)</td>
      <td>2020</td>
      <td>2551159.16</td>
    </tr>
    <tr>
      <td>August (2020)</td>
      <td>2020</td>
      <td>2786648.26</td>
    </tr>
    <tr>
      <td>September (2020)</td>
      <td>2021</td>
      <td>12353509.79</td>
    </tr>
    <tr>
      <td>October (2020)</td>
      <td>2021</td>
      <td>13218636.20</td>
    </tr>
    <tr>
      <td>November (2020)</td>
      <td>2021</td>
      <td>20464999.10</td>
    </tr>
    <tr>
      <td>December (2020)</td>
      <td>2021</td>
      <td>12944659.65</td>
    </tr>
    <tr>
      <td>January (2021)</td>
      <td>2021</td>
      <td>12399392.98</td>
    </tr>
    <tr>
      <td>February (2021)</td>
      <td>2021</td>
      <td>10129735.57</td>
    </tr>
    <tr>
      <td>March (2021)</td>
      <td>2021</td>
      <td>12144061.25</td>
    </tr>
    <tr>
      <td>April (2021)</td>
      <td>2021</td>
      <td>7311999.95</td>
    </tr>
    <tr>
      <td>May (2021)</td>
      <td>2021</td>
      <td>12150225.01</td>
    </tr>
    <tr>
      <td>June (2021)</td>
      <td>2021</td>
      <td>9824521.01</td>
    </tr>
    <tr>
      <td>July (2021)</td>
      <td>2021</td>
      <td>12092346.32</td>
    </tr>
    <tr>
      <td>August (2021)</td>
      <td>2021</td>
      <td>7178707.59</td>
    </tr>
  </tbody>
</table>
