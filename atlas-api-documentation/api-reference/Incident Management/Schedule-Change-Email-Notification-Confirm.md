# Schedule Change-Email Notification Confirm

### Dependency

No preceding function needs to be carried out.

### Endpoint {% debug uid="search_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/event/confirmEmailScheduleChangeEvent.do](https://sandbox.atriptech.com/event/confirmEmailScheduleChangeEvent.do)

### Request

{% tabs %}
{% tab title="Schema" %}

**`eventId`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

Incident ID.

**`result`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

Schedule Change Type.

FLIGHT_CHANGE: Flight Change

FLIGHT_CANCELED: Flight Cancelled

NO_SCHEDULE_CHANGE: No Schedule Change

**`remark`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Remark.

**changedFlights Array<**<mark style="color:blue;">**changedFlightsElement**</mark>**> **<mark style="color:orange;">**Optional**</mark>
**`originalFlightNo`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Required**</mark>

Original Flight No.

**`newFlightNo`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

New Flight No

**`newDepartureTime`  **<mark style="color:blue;">**Date**</mark>**  **<mark style="color:orange;">**Optional**</mark>

New Departure Time. yyyy-MM-dd HH:mm:ss

**`newArrivalTime`  **<mark style="color:blue;">**Date**</mark>**  **<mark style="color:orange;">**Optional**</mark>

New Arrival Time. yyyy-MM-dd HH:mm:ss

**`newDepartureAirport`  **<mark style="color:blue;">**String**</mark>**  **<mark style="color:orange;">**Optional**</mark>

IATA code.

**`newDepartureTerminal`  **<mark style="color:blue;">**String**</mark>**  **<mark style="color:orange;">**Optional**</mark>

New Departure Terminal.

**`newArrivalAirport`  **<mark style="color:blue;">**String**</mark>**  **<mark style="color:orange;">**Optional**</mark>

IATA code.

**`newArrivalAirport`  **<mark style="color:blue;">**String**</mark>**  **<mark style="color:orange;">**Optional**</mark>

New Arrival Terminal.

**canceledFlights  **<mark style="color:blue;">**array**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Canceled Flights No.
{% endtab %}

{% tab title="Samples" %}
**Schedule Change-Email Notification Confirm with Flight Change**
```
{
    "event":"20230323113246035DNIDD",
    "result":"FLIGHT_CHANGE",
    "remark":"",
    "changedFlights":[
        {
        "originalFlightNo":"FZ2323",
        "newDepartureTime":"2023-04-23 13:30",
        "newArrivalTime":"2023-04-23 15:30"
    }
    ]
}
```
**Schedule Change-Email Notification Confirm with Flight Cancelled**
```
{
    "event":"20230323113246035DNIDD",
    "result":"FLIGHT_CANCELED",
    "remark":"",
    "changedFlights":["FZ3423","FZ3467"]
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

{% tab title="Samples" %}
```
{
    "status": 0,
    "msg": "success"
}
```
{% endtab %}
{% endtabs %}




