# Incident List

The "Incident List" is used to retrieve incidents in batches.

### Dependency

No preceding function needs to be carried out.

### Endpoint
[https://sandbox.atriptech.com/event/getPageList.do](https://sandbox.atriptech.com/event/getPageList.do)

### Request

{% tabs %}
{% tab title="Schema" %}



**`eventId`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Incident ID

**`orderNo`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Order number

**`eventType`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Incident type

email.schedulechange: Schedule Change-Email Notification

abnormal.cancelled: Unacounted Cancellation

order.schedulechange: Schedule Change-API Notification.

**`eventStatus`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Incident status

0: Unconfirmed 
1: Confirmed

**`airlines`  **<mark style="color:blue;">**array**</mark>**  **<mark style="color:orange;">**Optional**</mark>

An array of IATA Codes of airlines

**`eventTimeStart`  **<mark style="color:blue;">**Date**</mark>**  **<mark style="color:green;">**Required**</mark>

Incident Receiving Time Start 

Format: yyyy-MM-dd HH:mm:ss UTC+08:00

**`eventTimeEnd`  **<mark style="color:blue;">**Date**</mark>**  **<mark style="color:green;">**Required**</mark>

Incident Receiving Time End 

Format: yyyy-MM-dd HH:mm:ss UTC+08:00

**`depTimeStart`  **<mark style="color:blue;">**Date**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Departure Time Start(Departure local time) 

Format: yyyy-MM-dd HH:mm:ss

**`depTimeEnd`  **<mark style="color:blue;">**Date**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Departure Time End(Departure local time) 

Format: yyyy-MM-dd HH:mm:ss

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
    "eventStatus":[0,1],
    "airline":"",
    "eventTimeStart":"2023-04-01 00:00:00",
    "eventTimeEnd":"2023-05-01 00:00:00",
    "depTimeStart":null,
    "depTimeEnd":null,
    "pageIndex":1,
    "pageSize":100
}
```

{% endtab %}
{% endtabs %}


## Response

{% tabs %}
{% tab title="Schema" %}
*   **eventId **<mark style="color:blue;">**string**</mark>**

    Incident Id.
*   **orderNo **<mark style="color:blue;">**string**</mark>**

    Order Number.

*   **eventType **<mark style="color:blue;">**string**</mark>**

    Incident type

    email.schedulechange: Schedule Change-Email Notification

    abnormal.cancelled: Unacounted Cancellation

    order.schedulechange: Schedule Change-API Notification

*   **eventStatus**<mark style="color:blue;">**int**</mark>**

    Incident staus

    0: Unconfirmed 
    1: Confirmed
    
*   **eventTime**<mark style="color:blue;">**string**</mark>**

    Incident recieving time.UTC+08:00
    
*   **confirmedResult**<mark style="color:blue;">**string**</mark>**

    Incident Reason. Schedule Change Type & Cancelled Type.

*   **confirmedRemark**<mark style="color:blue;">**string**</mark>**

    Remark.

*   **clientCode**<mark style="color:blue;">**string**</mark>**

    Client code.

*   **createTime**<mark style="color:blue;">**Date**</mark>**

    Incident create time.UTC+08:00

*   **updateIme**<mark style="color:blue;">**Date**</mark>**
    
    Update Time.UTC+08:00

*   **airline**<mark style="color:blue;">**string**</mark>**
    
    Airline IATA code.

*   **depTime**<mark style="color:blue;">**Date**</mark>**

    Flight depature time. Depature local time.

*   **confirmTime**<mark style="color:blue;">**Date**</mark>**

    Confirmed Time. UTC+08:00

*   **notified**<mark style="color:blue;">**int**</mark>**

    Send the notification or not. 1: YES. 0: No

*   **pnr**<mark style="color:blue;">**string**</mark>**

    Order's pnr.

*   **paxName**<mark style="color:blue;">**string**</mark>**

    Order's passenger names.

*   **paxEmail**<mark style="color:blue;">**string**</mark>**

    Order's passenger Email. Email address passed to the Airline.


    
{% endtab %}

{% tab title="Samples" %}
```
{
    "records": [
        {
            "eventId": "20230401003644225YJQGR",
            "orderNo": "HCNMN20230227142411968",
            "subOrderNo": "HCNMN20230227142411968_1",
            "eventType": "email.schedulechange",
            "eventStatus": 0,
            "eventTime": "Apr 1, 2023 12:36:44 AM",
            "extraInfo": "4775822",
            "confirmedResult": null,
            "confirmedRemark": null,
            "clientCode": "TAC00001",
            "createTime": "Apr 1, 2023 12:36:44 AM",
            "updateIme": "Apr 1, 2023 12:36:44 AM",
            "airline": "F9",
            "depTime": "Mar 31, 2023 11:12:00 AM",
            "confirmTime": null,
            "confirmUsr": null,
            "notified": 1,
            "pnr": "G7ZNW5",
            "paxName": "SOWERS/REBECCA MUSETTA,STEPHENS/DAVID JEROME",
            "paxEmail": "GeraldineDushkin2005@ttjipiao.top"
        },
    …
    ]
}
```
{% endtab %}
{% endtabs %}
