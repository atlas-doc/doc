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



**`canceledFlights`  **<mark style="color:blue;">**array**</mark>**  **<mark style="color:orange;">**Optional**</mark>
