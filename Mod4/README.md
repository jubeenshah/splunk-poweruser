# Lab 4

## Task 1

* Task 1: Display web server failures during the last 7 days in a timechart with a trendline.

```
index=security sourcetype=linux_secure fail*
| timechart span=1d count as "Failures"
| trendline sma2(Failures) as Trend
```

![L3S1](./resources/L3S1.png)

* Task 2: Display the sales count of strategy games per day at Buttercup Games physical sales locations (i.e., not online) during the previous week.

```
index=sales sourcetype=vendor_sales categoryId="STRATEGY"
| timechart span=1d count
```

![L3S2](./resources/L3S2.png)

* Task 3: Display a choropleth map of United States retail sales during the last 7 Days.

```
index=sales sourcetype=vendor_sales
| where VendorID < 3000
| chart count over VendorStateProvince
| geom geo_us_states featureIdField=VendorStateProvince
```

![L3S3](./resources/L3S3.png)

* Task 4: Display a map of online sales by country during the previous week.

```
index=web sourcetype=access_combined action=purchase status=200
| iplocation clientip
| geostats latfield=lat longfield=lon count by clientip
```

![L3S4](./resources/L3S4.png)

* Task 5: Count the retail sales units sold by country and include a grand total row.

```
index=sales sourcetype=vendor_sales 
| chart count by VendorCountry
| rename count as "Units Sold"
| addtotals col=t row=f labelfield=VendorCountry label=Total
```

![L3S5](./resources/L3S5.png)