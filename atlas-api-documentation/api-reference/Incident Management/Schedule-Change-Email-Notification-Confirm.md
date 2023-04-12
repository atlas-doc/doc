# Schedule Change Email Notification Confirm

### Dependency

No preceding function needs to be carried out.

### Endpoint {% debug uid="search_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com//event/confirmEmailScheduleChangeEvent.do](https://sandbox.atriptech.com//event/confirmEmailScheduleChangeEvent.do)

### Request

{% tabs %}
{% tab title="Schema" %}

**`result`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

Schedule Change Type.

FLIGHT_CHANGE: Flight Change

FLIGHT_CANCELED: Flight Cancelled

NO_SCHEDULE_CHANGE: No Schedule Change

**`remark`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Remark.

**changedFlights Array<**<mark style="color:blue;">**changedFlightsElement**</mark>**> **<mark style="color:orange;">**Optional**</mark>

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

**`canceledFlights`  **<mark style="color:blue;">**array**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Canceled Flights No.



