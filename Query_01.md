### Q1. Provide the list of markets in which customer "Atliq Exclusive" operates its business in the APAC region.

```
SELECT * FROM dim_customer;

SELECT 
DISTINCT(market),
customer,
region
FROM dim_customer
WHERE customer = "Atliq Exclusive" AND region = "APAC"; 
```



<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>market</th>
      <th>customer</th>
      <th>region</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>India</td>
      <td>Atliq Exclusive</td>
      <td>APAC</td>
    </tr>
    <tr>
      <td>Indonesia</td>
      <td>Atliq Exclusive</td>
      <td>APAC</td>
    </tr>
    <tr>
      <td>Japan</td>
      <td>Atliq Exclusive</td>
      <td>APAC</td>
    </tr>
    <tr>
      <td>Philiphines</td>
      <td>Atliq Exclusive</td>
      <td>APAC</td>
    </tr>
    <tr>
      <td>South Korea</td>
      <td>Atliq Exclusive</td>
      <td>APAC</td>
    </tr>
    <tr>
      <td>Australia</td>
      <td>Atliq Exclusive</td>
      <td>APAC</td>
    </tr>
    <tr>
      <td>Newzealand</td>
      <td>Atliq Exclusive</td>
      <td>APAC</td>
    </tr>
    <tr>
      <td>Bangladesh</td>
      <td>Atliq Exclusive</td>
      <td>APAC</td>
    </tr>
  </tbody>
</table>



