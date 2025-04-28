# Payment

### Dependency

`Order` function should be called in prior to this call.

### Endpoint {% debug uid="pay_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/pay.do](https://sandbox.atriptech.com/pay.do)

{% hint style="info" %}
- Atlas provides the information from the search.do API response itself whether VCC can be accepted as a mode of payment for an order. Please read the "supportCreditTransPayment" field in the search.do and verify.do responses. When this field is equal to "0" (zero), it means that only "deposit" mode of payment can be used and when this field is equal to "1" (one), it means that both the "deposit" as well as the "VCC" mode of payment can be used.
- For VCC payments, the Test Cards to be used for testing in SANDBOX:

    Visa
    - 4532015112830366
    - 4916931584764308
    - 4485275742308327
    - 4556737586899855
    - 4532644189324563

    Mastercard
    - 5555555555554444
    - 5105105105105100
    - 5223456789012346
    - 5301250070000191
    - 5454545454545454

    American Express
    - 378282246310005
    - 371449635398431
    - 340000000000009
    - 370000000000002
    - 375987654321001

    Discover 
    - 6011111111111117 
    - 6011000990139424 
    - 6011987612345678

    JCB
    - 3566002020360505

{% endhint %}

## Request

{% tabs %}
{% tab title="Schema" %}

### Deposit Mode of Payment

*   **orderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Order number. It can be an order for ticketing, or an order for add bags. The format of each kind of order is different.

### VCC Mode of Payment 

Cardholder country, province, city, postcode and address are required only for a select few airlines as per the table provided below:

| Airline Code | Airline Name | cardHolderCountry | cardHoldProvince | cardHolderCity | cardHolderPostCode | cardHolderAddress |
| ---- | -------- | -----------------| ----------------- | ------------- | ----------------- | ------------------ |
| 4N | Air North | Required| Required | Required | Required | Required |
| 5J | Cebu Pacific Air | Required| Required | Required | Required | Required |
| 8P | Pacific Coastal | Required| Required | Not Required | Required | Required |
| 9M | Central Mountain Air | Required| Required | Not Required | Required | Required |
| A3 | Aegean Airlines | Required| Required | Required | Required | Required |
| AN | Advanced Airlines | Required| Required | Required | Required | Required |
| AS | Alaska Airlines | Not Required| Required | Required | Required | Required |
| BT | Air Baltic | Required| Not Required | Required | Required | Required |
| BV | TOKI AIR | Required| Required | Required | Required | Required |
| D8 | Norwegian Air Sweden | Required| Not Required | Required | Required | Required |
| DE | Condor | Not Required| Not Required | Required | Not Required | Not Required |
| DG | Cebgo | Required| Required | Required | Required | Required |
| DI | Cebu Pacific Air | Not Required| Not Required | Required | Not Required | Not Required |
| DM | Arajet | Required| Required | Required | Required | Required |
| DY | Norwegian Air Shuttle ASA | Not Required| Required | Required | Required | Required |
| E6 | Eurowings Europe | Required| Required | Required | Required | Required |
| EI | Aer Lingus | Required| Required | Required | Required | Required |
| EW | Eurowings | Required| Required | Required | Required | Required |
| F9 | Frontier Airlines (US Address) | Required | Not Required | Required | Required | Required |
| F9 | Frontier Airlines (Non-US Address) | Not Required | Not Required | Not Required | Not Required | Not Required |
| FA | Fly Safair | Required| Required | Required | Required | Required |
| G4 | Allegiant Air | Required| Required | Required | Required | Required |
| GE | Lift Airline | Required| Required | Required | Required | Required |
| GQ | Skyexpress | Required| Required | Required | Required | Required |
| H4 | HiSky | Required| Not Required | Not Required | Not Required | Not Required |
| H7 | HiSky | Required| Not Required | Not Required | Not Required | Not Required |
| JV | Perimeter | Required| Required | Required | Not Required | Not Required |
| KM | AirMalta | Required| Not Required | Required | Not Required | Required |
| LJ | Jin Air | Required| Required | Not Required | Required | Required |
| MM | Peach Aviation | Not Required| Not Required | Required | Required | Required |
| MO | Calm Air | Not Required| Not Required | Not Required | Not Required | Required |
| NK | Spirit Airlines | Required| Required | Required | Required | Required |
| OA | Olympic Air | Required| Required | Required | Required | Required |
| OG | PLAY | Required| Required | Required | Required | Required |
| P6 | Pascan | Required| Required | Required | Required | Required |
| PB | PAL Airlines | Required| Required | Required | Required | Required |
| RW | Royal Air Philippines | Not Required| Not Required | Not Required | Not Required | Required |
| SY | Sun Country Airlines | Required| Required | Required | Required | Required |
| TR | Scoot Tiger Air | Required| Not Required | Required | Required | Required |
| VY | Vueling Airlines | Required| Not Required | Required | Required | Required |


*   **orderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Order number. It can be an order for ticketing, or an order for add bags. The format of each kind of order is different.
*   **supportCreditTransPayment **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

    1 ：Payment with credit card pass through to the airline

    0 : Payment with Prepayment

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
      *   **cardHolderCountry **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

          The country code of card holder
          
      *   **cardHolderProvince **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

          Only use 2-letter US state codes and not full names. For example; use "CA" and not "California".
      *   **cardHolderCity **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

          The city name of card holder
      *   **cardHolderPostCode **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

          The post code of card holder
      *   **cardHolderAddress **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

          The address of card holder
      *   **reusable **<mark style="color:blue;">**boolean**</mark>**  **<mark style="color:green;">**Optional**</mark>

          Valid values:
          - true: multiple-use card
          - false: single-use card
       
          Default: false: single-use card
    
          Do note that when encountering unknown errors in payment to the airline, Atlas will not easily attempt to retry, as this may result in multiple deductions. 
      *   **paymentLimit **<mark style="color:blue;">**int**</mark>**  **<mark style="color:orange;">**Optional**</mark>

          Certain airlines may experience fare change after payment submission due to their inability to hold seat reservations. You can use this parameter to set a maximum acceptable payment amount threshold. This is the maximum amount which can be used to create the booking using a VCC.

          If this parameter is 'null', our system will automatically set the maximum acceptable amount as the greater of either 5% of the order price or 5 USD (converted to the transacting currency) per passenger. When the amount entered by the customer is lower than 5% of the order price or 5 USD (converted to the transacting currency) per passenger, the information sent to Atlas by the customer will be used.  
         
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
      
**orderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

Order number. 

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
