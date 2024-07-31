# Query Refund Status 

### Dependency

No preceding function needs to be carried out.

### Endpoint {% debug uid="RefundQuotation_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/queryRefundOrders.do](https://sandbox.atriptech.com/queryRefundOrders.do)

## Request

{% tabs %}
{% tab title="Schema" %}
*   **orderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Original order number.
*   **refundCode **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    The code of the refund transaction received in the refund.do response.
    
{% endtab %}

{% tab title="Samples" %}
```json
{
  "orderNo": "TEST20220209163159425",
  "refundCode": "202407-0028"
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
*   **status **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    The present status of the refund.

    The options are:

    0: Submitted (The customer has submitted to Atlas)

    1: Airline processing (Submitted to airline by Atlas)

    2: Refunded

    3: Rejected
    
{% endtab %}

{% tab title="Samples" %}
```json
{
  "refundStatus": 0,
  "msg": "",
  "refundOrders": [
    {
      "orderNo": "TEST20220209163159425",
      "refundCode": "202407-0028",
      "currency": "USD",
      "originalTotalFareAmount": "500",
      "originalTotalAncillaryAmount": "200",
      "originalTotalAmount": "700",
      
      "airlinePenaltyAmountForFare": "100",
      "airlinePenaltyAmountForAncillaries": "200",
      "airlinePenaltyAmount": "50",
      
      "estimatedRefundAmount": "350",
      
      "transactionFee": "2.50",
      
      "refundTickets": [{
        "firstName": "TEST",
        "lastName": "ONE",
        "ticketNo": "ABXSJI",
        "currency": "USD",
        "originalFareAmount": 600,
        "originalAncillaryAmount": 0,
        "originalTotalAmount": 600,
        "refundableAmountForFare": 10,
        "refundableAmountForAncillaries": 0,
        "actualRefundAmount": 10,
        "refundReason": "1",
        "airlinePenaltyAmountForFare": 250,
        "airlinePenaltyAmountForAncillaries": 0,
        "airlinePenaltyAmount": 250,
        "estimatedRefundAmount": 250
      },
      {
        "firstName": "TEST",
        "lastName": "TWO",
        "ticketNo": "ABXSJI",
        "currency": "USD",
        "originalFareAmount": 600,
        "originalAncillaryAmount": 0,
        "originalTotalAmount": 600,
        "refundableAmountForFare": 10,
        "refundableAmountForAncillaries": 0,
        "actualRefundAmount": 10,
        "refundReason": "1",
        "airlinePenaltyAmountForFare": 250,
        "airlinePenaltyAmountForAncillaries": 0,
        "airlinePenaltyAmount": 250,
        "estimatedRefundAmount": 250
      }
     ],
     "refundRules": [{
        "airline": "RS",
        "startMinute": 525600,
        "endMinute": 0,
        "ruleType": "1", 
        "passengerType": "ADT/CHD/INF",
        "penaltyAmount": "", 
        "penaltyPercent": "", 
        "penaltyPercentBase": "fare+tax", 
        "airlineFee": "", 
        "taxRefundable": true, 
        "refundable": true,    
        "refundableAncillaries": [
          "StandardCheckInBaggage",
          "CabinBaggage",
          "CabinBaggageUnderSeat",
          "CabinBaggageOverheadLocker",
          "Infant"
        ]                                      
      }
    ],
    "actualRefundAmount": 0,
    "cancelReason": "",
    "refundOfferId": "12610f6a-1d00-499e-9fdb-664f4b5ea60b"
    }
  ]
}

```
{% endtab %}
{% endtabs %}
