# City Pairs API

The "City pairs API" can be used to download the city pairs supported by Atlas as well as by the airlines. The customer can use this structured data and transfer the city pair information into their mid-back office systems.

**This API is only available in the production environment.**

## Dependency

There is no dependency for this call.

## Endpoint

[https://xxxx.xxxxxxxx.com/route/export.do](https://xxxx.xxxxxxxx.com/route/export.do)

## Request

{% hint style="info" %}
**Points to note**

* The maximum and default limit of the city pair API response is 10000 records.
* If the objective is to retrieve all the routes, then the tags "pageSize" and "pageNumber" should be used.
  Sample:
```
  {
    "routeType": 2,
    "pageSize": 10000,
    "pageNumber": 1
  }
```
{% endhint %}

{% tabs %}
{% tab title="Schema" %}
*   **routeType **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Mandatory**</mark>

    Type code: 

    1 = Airline routes

    2 = Atlas routes 

*   **airlines **<mark style="color:blue;">**array**</mark>**  **<mark style="color:green;">**Optional**</mark>

    An array of IATA Codes of airlines. 

*   **fromCity **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    IATA Code of departure city or airport

*   **toCity **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    IATA Code of arrival city or airport

*   **fromCountry **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    IATA Code of departure country.

*   **toCountry **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    IATA Code of arrival country.

{% endtab %}

{% tab title="Samples" %}
```
{ 

    "routeType": 1, 

    "airlines": [ 

        "EI" 

    ], 

    "fromCity": "DUB", 

    "fromCountry": "IE", 

    "toCity": "SAN", 

    "toCountry": "IE" 

} 
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
*   **airlines **<mark style="color:blue;">**array**</mark>**  **<mark style="color:orange;">**Mandatory**</mark>

    An array of IATA Codes of airlines. 

*   **fromCity **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Mandatory**</mark>

    IATA Code of departure city or airport

*   **toCity **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Mandatory**</mark>

    IATA Code of arrival city or airport

*   **fromCountry **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Mandatory**</mark>

    IATA Code of departure country.

*   **toCountry **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Mandatory**</mark>

    IATA Code of arrival country.

*   **isDirect **<mark style="color:blue;">**boolean**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    True: Direct Flight 

    False: Transfer Flight 

    This data will only be available when the "routeType" = 2 (Atlas Routes)

*   **scheduleStart **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    The start date of the booking window. The format is YYYYMMDD.

*   **scheduleEnd **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    The end date of the booking window. The format is YYYYMMDD.

*   **updateDate **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    The date when the routing data was updated. The format is YYYYMMDD.
    
{% endtab %}

{% tab title="Samples" %}
```
{ 

    "data": [ 

        { 

            "airlines": [ 

                "EI" 

            ], 

            "fromCity": "DUB", 

            "fromCountry": "IE", 

            "toCity": "SAN", 

            "toCountry": "IE", 

            "isDirect": false, 

            "scheduleStart": "20241024", 

            "scheduleEnd": "20250428", 

            "updateDate": "20241031" 

        }, 

], 

    "status": 0, 

    "msg": null 

} 
```
{% endtab %}
{% endtabs %}
