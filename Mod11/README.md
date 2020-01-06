# Lab 11

## Tasks

* **Task 1:** Write a basic macro to create a table displaying the total sales of each product sold in Europe.

```
index=sales sourcetype=vendor_sales ((VendorCountry="Germany") OR (VendorCountry="France") OR (VendorCountry="Italy"))
| stats sum(sale_price) as USD by product_name
| eval USD = "$" + tostring(USD,"commas")
```

![](./resources/01.png)

* **Task 2:** Use a basic macro.

```
index=sales sourcetype=vendor_sales ((VendorCountry="Germany") OR (VendorCountry="France") OR (VendorCountry="Italy"))
| stats sum(sale_price) as USD by product_name
|`europe_sales`
```

![](./resources/02.png)

* **Task 3:** Create a macro that enables users to specify currency when performing a search. This macro uses currency, currency symbol, and rate as variables (arguments).

```
sourcetype=vendor_sales VendorCountry=Germany OR VendorCountry=France OR VendorCountry=Italy
| stats sum(price) as USD by product_name
| eval euro = "€" + tostring(round(USD*0.79,2), "commas"), USD = "$" + tostring(USD, "commas")
```

![](./resources/03.png)


* **Task 4:** Use your macro with arguments in a search.

```
sourcetype=vendor_sales VendorCountry=Germany OR VendorCountry=France OR VendorCountry=Italy
| `convert_sales(euro,€,.79)`
```

![](./resources/04.png)