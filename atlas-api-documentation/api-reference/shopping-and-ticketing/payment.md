# Payment

### Dependency

`Order` function should be called in prior to this call.

### Endpoint {% debug uid="pay_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/pay.do](https://sandbox.atriptech.com/pay.do)

{% hint style="info" %}
- Atlas provides the information from the search.do API response itself whether VCC can be accepted as a mode of payment for an order. Please read the "supportCreditTransPayment" field in the search.do and verify.do responses. When this field is equal to "0" (zero), it means that only "deposit" mode of payment can be used and when this field is equal to "1" (one), it means that both the "deposit" as well as the "VCC" mode of payment can be used.
- For VCC payment, you can use any fictitious card number.

{% endhint %}

## Request

{% tabs %}
{% tab title="Schema" %}

### Deposit Mode of Payment

*   **orderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Order number. It can be an order for ticketing, or an order for add bags. The format of each kind of order is different.

### VCC Mode of Payment 

*   **orderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Order number. It can be an order for ticketing, or an order for add bags. The format of each kind of order is different.
*   **supportCreditTransPayment **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

    1 ：Payment with credit card pass through to the airline

    0 : Payment with Prepayment

*   **maxAcceptedAmount **<mark style="color:blue;">**int**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    Certain airlines may experience fare change after payment submission due to their inability to hold seat reservations. You can use this parameter to set a maximum acceptable payment amount threshold. This is the maximum amount which can be used to create the booking using a VCC.

    If this parameter is 'null', our system will automatically set the maximum acceptable amount as the greater of either 5% of the order price or 5 USD (converted to the transacting currency) per passenger. When the amount entered by the customer is lower than 5% of the order price or 5 USD (converted to the transacting currency) per passenger, the information sent to Atlas by the customer will be used.    

*   **creditCard Object< **<mark style="color:blue;">**CreditCardElement**</mark>** > **<mark style="color:green;">**Required**</mark>

   * <mark style="color:blue;">**CreditCardElement**</mark>
      *   **cardNumber **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          Virtual credit card number.
      *   **cardExpireMonth **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          Card expire month
      *   **cardExpireYear **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          Card expire year
      *   **cardCVV **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          CVV of the credit card
      *   **cardHolderLastName **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          Last name of the card holder
      *   **cardHolderFirstName **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          First name of the card holder
      *   **cardHolderCountry **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          The country code of card holder
          
      *   **cardHolderProvince **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          The province or state of the card holder. This field is mandatory for US addresses. For addresses outside the US, this field can be left "blank". Only use 2-letter US state codes and not full names. For example; use "CA" and not "California".
      *   **cardHolderCity **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          The city name of card holder
      *   **cardHolderPostCode **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          The post code of card holder
      *   **cardHolderAddress **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          The address of card holder
{% endtab %}

{% tab title="Samples" %}
* Pay with prepayment

```json
{
   "orderNo": "PSTEV20220119165629057"
}
```

* Pay with credit card pass through

```json
{
    "orderNo": "PSTEV20220119165629057",
    "supportCreditTransPayment": "1",
    "creditCard": {
        "cardNumber": "0000000000000000",
        "cardExpireMonth": "12",
        "cardExpireYear": "25",
        "cardCVV": "000",
        "cardHolderLastName": "XXXXX",
        "cardHolderFirstName": "XXXXX",
        "cardHolderCountry": "XXXXX",
        "cardHolderProvince": "XXXXX",
        "cardHolderCity": "XXXXX",
        "cardHolderPostCode": "XXXXX",
        "cardHolderAddress": "XXXXX",
        "maxAcceptedAmount": "105"
    }
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %} 
      
**Order Number **<mark style="color:blue;">**string**</mark>

Order number

**pnrCode **<mark style="color:blue;">**string**</mark>
    
The pnrCode is the single reference for the booking. This is the Atlas PNR. 

**`paymentMethod`  **<mark style="color:blue;">**string**</mark>

This tag shows the form of payment used. 

1: Pre-payment

3: VCC

**`airlines`  **<mark style="color:blue;">**array**</mark>**  **<mark style="color:orange;">**Optional**</mark>

IATA Code of the airline.
*   **status **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

0: success

2: System error
*   **msg **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

Error message.
    
The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to         check the result.
{% endtab %}

{% tab title="Samples" %}
```
{
  "orderNo": "ANRUE20230906141814490",
  "pnrCode": "ZMPB8O",
  "paymentMethod": 1,
  "airlines": [
    "5W"
  ],
  "status": 0,
  "msg": null
}
```
{% endtab %}
{% endtabs %}
