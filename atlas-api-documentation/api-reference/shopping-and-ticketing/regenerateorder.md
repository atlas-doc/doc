---
description: >-
  This function is to help you regenerate the order by one single call with the
  latest fare after the original order has expired or has been cancelled.
---

# RegenerateOrder

{% hint style="info" %}
<mark style="color:red;">**An order can only be regenerated within 24 hours of the original order number.**</mark>
{% endhint %}

## Dependency

Order function should be called in prior to this call.

## Endpoint

[https://sandbox.atlaslovestravel.com/regenerateOrder](https://sandbox.atlaslovestravel.com/regenerateOrder.do)

## Request

{% tabs %}
{% tab title="Schema" %}
*   #### cid                                  <mark style="color:blue;">string</mark>                                                                                                 <mark style="color:green;">Required</mark>

    Identifier of client and user.
*   #### originalOrderNo                       <mark style="color:blue;">string</mark>                                                                                 <mark style="color:green;">Required</mark>

    Original order number which you would like to regenerate.&#x20;
{% endtab %}

{% tab title="Samples" %}
```json
{
    "cid": "XXXXXXXX",
    "originalOrderNo": "ZNMKU20220119160129691"
}             
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
* #### Please click [here](order.md#response) to refer to the response schema of order
{% endtab %}

{% tab title="Samples" %}
Please click [here](order.md#response) to refer to the reponse schema of order
{% endtab %}
{% endtabs %}
