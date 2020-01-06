# Lab 10

## Tasks

* **Task 1:** Create tags to identify all admin accounts.

```
index=security sourcetype=linux_secure failed tag=privileged_user
```

![](./resources/01.png)

* **Task 2:** Use tags in a search.

```
index=security failed tag=privileged_user
```

![](./resources/02.png)

* **Task 3:** Create an event type for status errors greater than 500 on web servers/devices.

```
index=web OR index=sales status>500 eventtype=web_error
```

![](./resources/03.png)