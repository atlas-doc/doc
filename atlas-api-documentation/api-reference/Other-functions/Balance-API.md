# Get Balance

The "Balance API" is used to fetch the deposit balance from the ATRIP credentials of the customer.

The customer will need to send the header information and the respons ewill be received with the ATRIP deposit balance.

## Dependency

There is no dependency for this call.

## Endpoint

[https://sandbox.atriptech.com/balance](https://sandbox.atriptech.com/balance.do)

## Request

The "request" has to be only the header information consisting of 'x-atlas-client-id' and 'x-atlas-client-secret'

## Response

{% tabs %}
{% tab title="Schema" %}

**`accountBalance`  **<mark style="color:blue;">**string**</mark>

This element contavins the information regarding the amount and the currency of transaction of the customer.

**`amount`  **<mark style="color:blue;">**string**</mark>

The amount of balance in your deposit account.

**`currency`  **<mark style="color:blue;">**string**</mark>

The currency in which Atlas settles transactions with you.

**'status' **<mark style="color:blue;">**string**</mark>

0: success

9999: error (an error message will be displayed with the issue)

{% endtab %}

{% tab title="Samples" %}
```
{
    "accountBalance": {
        "amount": 12308007.89,
        "currency": "USD"
    },
    "status": 0
}
```
{% endtab %}
{% endtabs %}
