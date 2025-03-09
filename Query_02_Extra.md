```
WITH CTE_T2020 AS (
    SELECT DISTINCT product_code FROM fact_sales_monthly WHERE fiscal_year = 2020
),
CTE_T2021 AS (
    SELECT DISTINCT product_code FROM fact_sales_monthly WHERE fiscal_year = 2021
)
SELECT 
    (SELECT COUNT(*) FROM CTE_T2020 T2020 INNER JOIN CTE_T2021 T2021 
        ON T2020.product_code = T2021.product_code) AS Retained_Products,
    (SELECT COUNT(*) FROM CTE_T2020 WHERE product_code NOT IN (SELECT product_code FROM CTE_T2021)) AS Discontinued_Products,
    (SELECT COUNT(*) FROM CTE_T2021 WHERE product_code NOT IN (SELECT product_code FROM CTE_T2020)) AS New_Products_2021;
```

<table>
        <tr>
            <th>Retained_Products</th>
            <th>Discontinued_Products</th>
            <th>New_Products_2021</th>
        </tr>
        <tr>
            <td>232</td>
            <td>13</td>
            <td>102</td>
        </tr>
  </table> 



  ```
WITH CTE_T2020 AS (
    SELECT DISTINCT product_code 
    FROM fact_sales_monthly
    WHERE fiscal_year = 2020
),
CTE_T2021 AS (
    SELECT DISTINCT product_code 
    FROM fact_sales_monthly
    WHERE fiscal_year = 2021
)
SELECT 
    product_code,
    'Discontinued in 2021' AS Product_Status
FROM CTE_T2020
WHERE product_code NOT IN (SELECT product_code FROM CTE_T2021)

UNION 

SELECT 
    product_code,
    'New in 2021' AS Product_Status
FROM CTE_T2021
WHERE product_code NOT IN (SELECT product_code FROM CTE_T2020)

UNION 

SELECT 
    product_code,
    'Retained in both years' AS Product_Status
FROM CTE_T2020
WHERE product_code IN (SELECT product_code FROM CTE_T2021)

ORDER BY Product_Status, product_code;
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>product_code</th>
      <th>Product_Status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>A0418150101</td>
      <td>Discontinued in 2021</td>
    </tr>
    <tr>
      <td>A0418150102</td>
      <td>Discontinued in 2021</td>
    </tr>
    <tr>
      <td>A0418150107</td>
      <td>Discontinued in 2021</td>
    </tr>
    <tr>
      <td>A0418150108</td>
      <td>Discontinued in 2021</td>
    </tr>
    <tr>
      <td>A3718150104</td>
      <td>Discontinued in 2021</td>
    </tr>
    <tr>
      <td>A4118110101</td>
      <td>Discontinued in 2021</td>
    </tr>
    <tr>
      <td>A4118110102</td>
      <td>Discontinued in 2021</td>
    </tr>
    <tr>
      <td>A4118110103</td>
      <td>Discontinued in 2021</td>
    </tr>
    <tr>
      <td>A4118110104</td>
      <td>Discontinued in 2021</td>
    </tr>
    <tr>
      <td>A5119110304</td>
      <td>Discontinued in 2021</td>
    </tr>
    <tr>
      <td>A5219110404</td>
      <td>Discontinued in 2021</td>
    </tr>
    <tr>
      <td>A5318110101</td>
      <td>Discontinued in 2021</td>
    </tr>
    <tr>
      <td>A5318110102</td>
      <td>Discontinued in 2021</td>
    </tr>
    <tr>
      <td>A0321150302</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A0321150303</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A0721150403</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A0721150404</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A0821150501</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A0821150502</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A0821150503</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A0821150504</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A0921150601</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A1420150502</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A1421150503</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A1521150601</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A1521150602</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A1919150401</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A1919150402</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A1919150403</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A1920150404</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A2020150501</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A2020150502</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A2021150503</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A2520150501</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A2520150502</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A2520150503</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A2520150504</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A2520150505</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A2520150506</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A2620150601</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A2620150602</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A2620150603</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A2620150604</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A2620150605</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A2620150606</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A2720150701</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A2721150702</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A2721150703</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A2721150704</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A2721150705</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A2721150706</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A2821150801</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A3320150505</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A3320150506</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A3420150601</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A3420150602</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A3421150603</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A3421150604</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A3421150605</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A3421150606</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A3521150701</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A3521150702</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A3521150703</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A3521150704</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A3521150705</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A4021150403</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A4021150404</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A4021150405</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A4520110505</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A4520110506</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A4520110507</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A4520110508</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A4620110601</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A4620110602</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A4620110603</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A4620110604</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A4620110605</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A4620110606</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A4620110607</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A4620110608</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A4720110701</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A4720110702</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A4721110703</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A4721110704</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A4721110705</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A5219110407</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A5220110408</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A5721110502</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A5721110503</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A5721110504</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A5721110505</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A5721110506</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A5820110101</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A5820110102</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A5820110103</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A5820110104</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A5820110105</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A5820110106</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A5820110107</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A5821110108</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A6019110108</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A6119110201</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A6119110202</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A6119110203</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A6119110204</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A6120110205</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A6120110206</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A6520160402</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A6520160403</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A6620160501</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A6818160202</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A6819160203</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A7321160301</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A7321160302</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A7321160303</td>
      <td>New in 2021</td>
    </tr>
    <tr>
      <td>A0118150101</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0118150102</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0118150103</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0118150104</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0219150201</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0219150202</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0220150203</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0320150301</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0418150103</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0418150104</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0418150105</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0418150106</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0519150201</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0519150202</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0519150203</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0519150204</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0519150205</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0519150206</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0519150207</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0519150208</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0619150301</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0619150302</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0620150303</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0620150304</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0620150305</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0620150306</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0621150307</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0621150308</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0721150401</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A0721150402</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A1018150101</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A1018150102</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A1018150103</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A1118150201</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A1118150202</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A1119150203</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A1219150301</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A1219150302</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A1219150303</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A1319150401</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A1320150402</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A1320150403</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A1420150501</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A1618150101</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A1618150102</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A1618150103</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A1618150104</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A1718150201</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A1718150202</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A1718150203</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A1718150204</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A1819150301</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A1819150302</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A1819150303</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A1819150304</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2118150101</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2118150102</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2118150103</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2118150104</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2118150105</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2118150106</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2218150201</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2218150202</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2219150203</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2219150204</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2219150205</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2219150206</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2319150301</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2319150302</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2319150303</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2319150304</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2319150305</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2319150306</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2419150401</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2419150402</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2419150403</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2419150404</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2419150405</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2420150406</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2918150101</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2918150102</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2918150103</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2918150104</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2918150105</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A2918150106</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3018150201</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3018150202</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3018150203</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3019150204</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3019150205</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3019150206</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3119150301</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3119150302</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3119150303</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3120150304</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3120150305</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3120150306</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3220150401</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3220150402</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3220150403</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3220150404</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3220150405</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3220150406</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3320150501</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3320150502</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3320150503</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3320150504</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3718150101</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3718150102</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3718150103</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3718150105</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3818150201</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3818150202</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3819150203</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3819150204</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3819150205</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3920150301</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3920150302</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3920150303</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3920150304</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A3920150305</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4020150401</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4020150402</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4118110105</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4118110106</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4118110107</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4218110201</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4218110202</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4218110203</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4218110204</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4218110205</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4218110206</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4218110207</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4218110208</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4318110301</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4319110302</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4319110303</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4319110304</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4319110305</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4319110306</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4419110401</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4419110402</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4419110403</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4419110404</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4419110405</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4419110406</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4419110407</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4419110408</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4519110501</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4519110502</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4519110503</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4520110504</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4918110101</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4918110102</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4918110103</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A4918110104</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5018110201</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5018110202</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5018110203</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5018110204</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5018110205</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5018110206</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5018110207</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5019110208</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5119110301</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5119110302</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5119110303</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5119110305</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5119110306</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5119110307</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5119110308</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5219110401</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5219110402</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5219110403</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5219110405</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5219110406</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5318110103</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5318110104</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5318110105</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5318110106</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5318110107</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5318110108</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5419110201</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5419110202</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5419110203</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5419110204</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5419110205</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5419110206</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5419110207</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5419110208</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5519110301</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5519110302</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5519110303</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5519110304</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5520110305</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5520110306</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5520110307</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5520110308</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5620110401</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5620110402</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5621110403</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5621110404</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5621110405</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5621110406</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5621110407</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5621110408</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A5721110501</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A6018110101</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A6018110102</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A6018110103</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A6018110104</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A6018110105</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A6018110106</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A6019110107</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A6218160101</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A6218160102</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A6219160103</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A6319160201</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A6319160202</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A6319160203</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A6419160301</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A6419160302</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A6419160303</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A6519160401</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A6720160103</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A6818160201</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A7118160101</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A7119160102</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A7119160103</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A7219160201</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A7220160202</td>
      <td>Retained in both years</td>
    </tr>
    <tr>
      <td>A7220160203</td>
      <td>Retained in both years</td>
    </tr>
  </tbody>
</table>

```
WITH CTE_T2020 AS (
    SELECT DISTINCT product_code 
    FROM fact_sales_monthly
    WHERE fiscal_year = 2020
),
CTE_T2021 AS (
    SELECT DISTINCT product_code 
    FROM fact_sales_monthly
    WHERE fiscal_year = 2021
),
Product_Status AS (
    SELECT 
        product_code,
        'Discontinued in 2021' AS Product_Status
    FROM CTE_T2020
    WHERE product_code NOT IN (SELECT product_code FROM CTE_T2021)

    UNION 

    SELECT 
        product_code,
        'New in 2021' AS Product_Status
    FROM CTE_T2021
    WHERE product_code NOT IN (SELECT product_code FROM CTE_T2020)

    UNION 

    SELECT 
        product_code,
        'Retained in both years' AS Product_Status
    FROM CTE_T2020
    WHERE product_code IN (SELECT product_code FROM CTE_T2021)
)
SELECT 
    ps.product_code,
    dp.product AS product_name,  -- Adding product name from dim_product
    ps.Product_Status
FROM Product_Status ps
LEFT JOIN dim_product dp ON ps.product_code = dp.product_code
ORDER BY ps.Product_Status, ps.product_code;
```



