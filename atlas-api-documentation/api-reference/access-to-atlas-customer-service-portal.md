# Access to Atlas Customer Service Portal

## Description

This method is to give client the access to Atlas customer service portal with SSO in client's own system.&#x20;

## Dependency

No preceding function needs to be carried out.

## Endpoint

[https://sandbox.atlaslovestravel.com/toOrderDetailWeb.do](https://sandbox.atlaslovestravel.com/toOrderDetailWeb.do)

## Request

{% tabs %}
{% tab title="Schema" %}
*   #### cid                                  <mark style="color:blue;">string</mark>                                                                                                 <mark style="color:green;">Required</mark>

    Identifier of client and user.
*   #### orderNo                       <mark style="color:blue;">string</mark>                                                                                                 <mark style="color:green;">Required</mark>

    Order number. It can be an order for ticketing, or an order for add bags. The format of each kind of order is different.
*   #### userName                   <mark style="color:blue;">string</mark>                                                                                                 <mark style="color:green;">Required</mark>

    This is to identifier the operator's name in client's system, Atlas will grant access to this operator and track his/her actions in Atlas customer service portal.
*   #### role                                <mark style="color:blue;">string</mark>                                                                                                 <mark style="color:green;">Required</mark>

    This is to identifier the operator's role, Atlas will grant access to this operator according to the role client send here. Here're the acceptable options &#x20;

    TICKETING : Access to manage orders and request post ticketing services

    FINANCE : Access to manage the balance and check statements

    TECH : Access to manage the system configurations

    ADMIN : All access


{% endtab %}

{% tab title="Samples" %}
```json
{
    "cid":"xxxxxx", 
    "orderNo": "XXXXXXXXXXXXXXXXXXX",
    "userName": "tony.kal",
    "role": "TICKETING"
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
*   #### msg                                      <mark style="color:blue;">string</mark>                                                                                                &#x20;

    Error message.
*   #### status                                  <mark style="color:blue;">int</mark>                                                                                                      &#x20;

    0: success

    2: System error

    3: unauthorized access
*   #### url                                      <mark style="color:blue;">string</mark>                                                                                                &#x20;

    A url with token to access to Atlas customer service portal.
{% endtab %}

{% tab title="Samples" %}
```json
{
    "url": "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
    "status": 0
}
```
{% endtab %}
{% endtabs %}

###
