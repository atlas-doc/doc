# Incident List

The "Incident List" is used to batch query incidents.

### Dependency

No preceding function needs to be carried out.

### Endpoint {% debug uid="search_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/event/getPageList.do](https://sandbox.atriptech.com/event/getPageList.do)

### Request

{% tabs %}
{% tab title="Schema" %}

**`eventId`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

Incident ID.



**`eventId`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Incident ID.

**`orderNo`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Order number.

**`eventType`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Incident type.

email.schedulechange: Schedule Change-Email Notification

abnormal.cancelled: Unacounted Cancellation

order.schedulechange: Schedule Change-API Notification. 

**`eventStatus`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Incident status.

0: Unconfirmed 
1: Confirmed

**`airlines`  **<mark style="color:blue;">**array**</mark>**  **<mark style="color:orange;">**Optional**</mark>

An array of IATA Codes of airlines.

**`eventTimeStart`  **<mark style="color:blue;">**Date**</mark>**  **<mark style="color:green;">**Required**</mark>

Incident Receiving Time Start. yyyy-MM-dd HH:mm:ss UTC+08:00

**`eventTimeEnd`  **<mark style="color:blue;">**Date**</mark>**  **<mark style="color:green;">**Required**</mark>

Incident Receiving Time End. yyyy-MM-dd HH:mm:ss UTC+08:00

**`depTimeStart`  **<mark style="color:blue;">**Date**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Departure Time Start(Departure local time). yyyy-MM-dd HH:mm:ss

**`depTimeEnd`  **<mark style="color:blue;">**Date**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Departure Time End(Departure local time). yyyy-MM-dd HH:mm:ss

**`pageIndex`  **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

Pagination

**`pageSize`  **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

Number of records per page

{% endtab %}


{% tab title="Samples" %}
**Unaccounted Cancellation Confirm **
```
{
    "eventId":"",
    "orderNo":"",
    "eventType":"",
    "eventStatus":0,
    "airlines":"",
    "eventTimeStart":"2023-04-01 00:00:00",
    "eventTimeEnd":"2023-05-01 00:00:00",
    "depTimeStart":"",
    "depTimeEnd":"",
    "pageIndex":1,
    "pageSize":100,
}
```

{% endtab %}
{% endtabs %}


## Response

{% tabs %}
{% tab title="Schema" %}
*   **status **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

    0: success

    2: System error
*   **msg **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Error message.
    
    The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to check the result.
{% endtab %}

*   **count **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Incident count.
    
*   **eventList Array**<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Incident List, the same format as the Notification.

{% tab title="Samples" %}
```
{
    "status": 0,
    "msg": "success"
}
```
{% endtab %}
{% endtabs %}







