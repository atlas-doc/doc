# Payment

### Dependency

`Order` function should be called in prior to this call.

### Endpoint

[https://sandbox.atlaslovestravel.com/pay.do](https://sandbox.atlaslovestravel.com/pay.do)

## Request

{% tabs %}
{% tab title="Schema" %}
*   #### cid                                  <mark style="color:blue;">string</mark>                                                                                                 <mark style="color:green;">Required</mark>

    Identifier of client and user.
*   #### orderNo                       <mark style="color:blue;">string</mark>                                                                                                 <mark style="color:green;">Required</mark>

    Order number. It can be an order for ticketing, or an order for add bags. The format of each kind of order is different.
*   #### supportCreditTransPayment                       <mark style="color:blue;">int</mark>                                                             <mark style="color:green;">Required</mark>

    1 ：Payment with credit card pass through to the airline

    0 :  Payment with Prepayment
*   #### creditCard                  Object<<mark style="color:blue;">CreditCardElement</mark>>                                                 <mark style="color:blue;"></mark>                                                 <mark style="color:orange;">Optional</mark>

    1 ：Payment with credit card pass through to the airline

    0 :  Payment with Prepayment

    * #### <mark style="color:blue;">CreditCardElement</mark>
      *   #### cardNumber                                  <mark style="color:blue;">string</mark>                                                               <mark style="color:green;">Required</mark>

          Virtual credit card number.
      *   #### cardExpireMonth                       <mark style="color:blue;">string</mark>                                                                <mark style="color:green;">Required</mark>

          Card expire month
      *   #### cardExpireYear                            <mark style="color:blue;">string</mark>                                                                <mark style="color:green;">Required</mark>

          Card expire year
      *   #### cardCVV                                         <mark style="color:blue;">string</mark>                                                               <mark style="color:green;">Required</mark>

          CVV of the credit card
      *   #### cardHolderLastName               <mark style="color:blue;">string</mark>                                                                <mark style="color:green;">Required</mark>

          Last name of the card holder
      *   #### cardHolderFirstName               <mark style="color:blue;">string</mark>                                                               <mark style="color:green;">Required</mark>

          First name of the card holder
      *   #### cardHolderCountry                    <mark style="color:blue;">string</mark>                                                               <mark style="color:orange;">Optional</mark>

          The country code of card holder
      *   #### cardHolderCity                             <mark style="color:blue;">string</mark>                                                               <mark style="color:orange;">Optional</mark>

          The city name of card holder
      *   #### cardHolderPostCode                 <mark style="color:blue;">string</mark>                                                              <mark style="color:orange;">Optional</mark>

          The post code of card holder
      *   #### cardHolderAddress                     <mark style="color:blue;">string</mark>                                                             <mark style="color:orange;">Optional</mark>

          The address of card holder
{% endtab %}

{% tab title="Samples" %}
* Pay with prepayment

```json
{
    "cid": "XXXXXXXX",
    "orderNo": "PSTEV20220119165629057"
}
```

* Pay with credit card pass through

```json
{
    "cid": "XXXXXXXX",
    "orderNo": "PSTEV20220119165629057",
    "supportCreditTransPayment": "1",
    "creditCard": {
        "cardNumber": "0000000000000000",
        "cardExpireMonth": "12",
        "cardExpireYear": "25",
        "cardCVV": "000",
        "cardHolderLastName": "XXXXX",
        "cardHolderFirstName": "XXXXX",
        "cardHolderCountry": null,
        "cardHolderCity": null,
        "cardHolderPostCode": null,
        "cardHolderAddress": null
    }
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
*   #### status                                  <mark style="color:blue;">int</mark>                                                                                                       <mark style="color:green;">Required</mark>

    0: success

    2: System error
*   #### msg                                      <mark style="color:blue;">string</mark>                                                                                                 <mark style="color:green;">Required</mark>

    Error message.
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
