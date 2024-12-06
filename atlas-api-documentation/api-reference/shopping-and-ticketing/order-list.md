# Order List

To get a list of orders as per the parameters entered.

### Dependency

No preceding function needs to be called before 'orderList' API.

### Endpoint {% debug uid="orderList_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/orderList.do](https://sandbox.atriptech.com/orderList.do)

{% hint style="info" %}
The "Order List" API is a feature which lists the orders which have been created on the Atlas platform. After receiving the response, the customer can access individual order by using the queryOrderDetails.do API.

Points to note:

•	All the parameters are optional.

•	Orders in all statuses can be queried.

•	Orders with departure time within 1 year can be retrieved.

•	The time format which is UTC.
{% endhint %}

## Request

{% tabs %}
{% tab title="Schema" %}
*   **orderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    Atlas order number. E.g.: TESTA20241122090710695
*   **airlinePNRs **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    The airline PNR received in the querryOrderDetails.do response. Please note that this is different from the "PNRCode" element. E.g.: ["FT759J", "8HFT67"]
*   **paxName **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    The name of the passenger as entered in the order.do request. E.g.: last name/first name
*   **contactEmail **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    The email as entered in the order.do request. E.g.: xxxxxxx@xmail.com
*   **fromCity **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    Departure city E.g.: SIN
*   **toCity **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    Arrival city E.g.: JKT
*   **depDate **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    Date of departure. Format: YYYYMMDD E.g.: 20241115
*   **createTimeRangeFrom **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    The start time of order creation. This is in UTC. Format: yyyy-MM-dd'T'HH:mm:ss'Z' E.g.: 2024-10-31T19:57:46Z
*   **createTimeRangeTo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    The end time of order creation. This is in UTC. Format: yyyy-MM-dd'T'HH:mm:ss'Z' E.g.: 2024-10-31T19:57:46Z
*   **orderStatus **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    The status in which the order is.

    Options:

    0: Unpaid

    1: Ticketing

    2: Ticketed

    3: Cancelled
*   **airlines **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    The airline code of one of the airline in the order. E.g.: ["FR"]
*   **page **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    Start from. Default: 1
*   **pageSize **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    Number of records to be displayed on each page. Default: 20 Maximum: 100
    
{% endtab %}

{% tab title="Samples" %}
```
{
  "orderNo": "",
  "airlinePNRs": [
    "FT759J",
    "8HFT67"
  ],
  "paxName": "",
  "contactEmail": "",
  "fromCity": "",
  "toCity": "",
  "depDate": "20240101",
  "createTimeRangeFrom": "2024-10-31T19:57:46Z",
  "createTimeRangeTo": "2024-11-01T19:57:46Z",
  "orderStatus": [
    0,
    1,
    2,
    -3
  ],
  "airlines": [
    "FR"
  ],
  "page": 1,
  "pageSize": 20
}
```
{% endtab %}
{% endtabs %}


## Response

{% tabs %}
{% tab title="Schema" %}
*   **orderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    Atlas order number. E.g.: TESTA20241122090710695
*   **PNRCode **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    Atlas internal reference code. E.g.: "Z44IPS"
*   **airlinePNRs **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    The airline PNR received in the querryOrderDetails.do response. Please note that this is different from the "PNRCode" element. E.g.: ["FT759J", "8HFT67"]
*   **paxNames **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    The name of the passenger. E.g.: last name/first name
*   **contactEmail **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    The email as entered in the order.do request. E.g.: xxxxxxx@xmail.com
*   **fromCity **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    Departure city E.g.: SIN
*   **toCity **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    Arrival city E.g.: JKT
*   **depDate **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    Date of departure. Format: YYYYMMDD E.g.: 20241115
*   **orderCreateTimestamp **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    The time of order creation. This is in UTC. Format: yyyy-MM-dd'T'HH:mm:ss'Z' E.g.: 2024-10-31T19:57:46Z
*   **paymentTimestamp **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    The time payment was made. This is in UTC. Format: yyyy-MM-dd'T'HH:mm:ss'Z' E.g.: 2024-10-31T19:57:46Z
*   **orderStatus **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    The status in which the order is.

    Options:

    0: Unpaid

    1: Ticketing

    2: Ticketed

    3: Cancelled
*   **airlines **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    The airline code of one of the airline in the order. E.g.: ["FR"]
*   **errorCode **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    The error code returned for a cancelled order. This will only be displayed for cancelled orders.
*   **errorMessage **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    The error description.
    
{% endtab %}

{% tab title="Samples" %}
```
{
    "orders": [
        {
            "orderNo": "TESTA20241122090710695",
            "pnrCode": "Z27T5B",
            "airlinePNRs": [
                "S86745"
            ],
            "orderStatus": 2,
            "travelStartDate": null,
            "airlines": [
                "SL"
            ],
            "orderCreateTimestamp": "2024-11-22T01:07:10Z",
            "paymentTimestamp": "2024-11-22T01:07:11Z",
            "paxNames": [
                "YIJING/tFGo"
            ],
            "contactEmail": "test@test.com",
            "fromCity": "CNX",
            "toCity": "BKK",
            "errorCode": null,
            "errorMessage": null
        },
        {
            "orderNo": "TESTA20241122080618700",
            "pnrCode": "LLQNYJ",
            "airlinePNRs": [
                "S79170|S79170"
            ],
            "orderStatus": 2,
            "travelStartDate": null,
            "airlines": [
                "TF"
            ],
            "orderCreateTimestamp": "2024-11-22T00:06:18Z",
            "paymentTimestamp": "2024-11-22T00:06:19Z",
            "paxNames": [
                "YIJING/gAMM",
                "JIXING/gAMM"
            ],
            "contactEmail": "test@test.com",
            "fromCity": "VBY",
            "toCity": "STO",
            "errorCode": null,
            "errorMessage": null
        }
    ],
    "page": 1,
    "pageSize": 20,
    "totalRecords": 2,
    "status": 0,
    "msg": null
}
```
{% endtab %}
{% endtabs %}
