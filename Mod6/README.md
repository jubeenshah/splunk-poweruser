# Lab 6

## Tasks

* **Task 1:** Analyze transactions in the online store during the last 60 minutes.

```
index=web sourcetype="access_combined"
| transaction JSESSIONID
| table JSESSIONID,clientip, action
| search action=purchase
```

![](./resources/01.png)

* **Task 2:** Display the online store purchase transactions lasting more than one minute and include the number of events in each transaction.

```
index=web sourcetype="access_combined"
| transaction JSESSIONID
| table JSESSIONID,clientip, duration,eventcount, action
| eval durationMinutes = round(duration/60,1)
| search action=purchase
| where durationMinutes > 1
| fields - duration
```

![](./resources/02.png)

* **Task 3:** Search for online store transactions that begin with an addtocart action and end with a purchase action.

```
index=web sourcetype="access_combined"
| transaction clientip startswith="addtocart" endswith="purchase"
| table clientip, JSESSIONID, product_name, action duration,eventcount,price
```

![](./resources/03.png)

* **Task 4:** Report common HTTP status errors that occurred during the last 30 days on the online sales web servers and the internal web appliance within a proximity of 5 minutes or less. Only include days with more than 5 common errors.


```
(index=network sourcetype=cisco_wsa_squid) OR (index=web sourcetype=access_combined) status>399
| fields sourcetype, status
| transaction status maxspan=1m
| timechart count by status
| addtotals
| where Total > 4
| fields - Total
```

![](./resources/05.png)

