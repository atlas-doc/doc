# Schedule Change-API Notification

### Dependency

No preceding function needs to be carried out.

### Endpoint

[https://sandbox.atriptech.com/event/confirmEvent.do](https://sandbox.atriptech.com/event/confirmEvent.do)

### Request

{% tabs %}
{% tab title="Schema" %}

**`eventId`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

Incident ID

**`remark`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Remark
{% endtab %}


{% tab title="Samples" %}

**Unaccounted Cancellation Confirm **
```
{
    "eventId":"20230323113246035DNIDD",
    "remark":""
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

    Error message
    
    The 'msg' element is for the description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to check the result.
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




