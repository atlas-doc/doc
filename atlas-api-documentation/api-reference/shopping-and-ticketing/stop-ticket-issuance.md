---
description: Tentative stopping ticket issuance.
---

# Stop Ticket Issuance

### Dependency

`Payment` function should be called in prior to this call.

### Endpoint {% debug uid="queryOrderDetails_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/topTicket.do](https://sandbox.atriptech.com/topTicket.do)

## Request

{% tabs %}
{% tab title="Schema" %}
*   **cid **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Identifier of client and user.
    
*   **orderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Order number. It must be an paid and ticketing order.
{% endtab %}

{% tab title="Samples" %}
```
{
    "cid": "XXXXXXXX",
    "orderNo": "ZNMKU20220119160129691"
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

    Success does not mean that the ticket issuance has been stopped successfully, it only means that the system will attempt to stop the ticket issuance.

    The result of stopping ticket issuance needs to be obtained by querying the order status of `Retrieve Booking` after 8 minutes.

    orderStatus: -3, means stop issuance successfully.
    
    orderStatus: 2, means stop issuance failed, the order is issued.


*   **msg **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Error message
    
    The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to check the result.

{% endtab %}

{% tab title="Samples" %}
```
{
    "status": 0,
    "msg": "We are trying to intercept the ticket issuance. Please check the order status for result after 8 minutes"
}
```
{% endtab %}
{% endtabs %}
