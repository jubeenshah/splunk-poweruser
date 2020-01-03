# Lab 6

## Tasks

* **Task 1:** Analyze transactions in the online store during the last 60 minutes.

```
index=web sourcetype="access_combined"
| table _time, clientip, JSESSIONID, action
| sort action
| where action NOT NULL
```

![](./resources/01.png)