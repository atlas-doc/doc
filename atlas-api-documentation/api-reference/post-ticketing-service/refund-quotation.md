# Refund Quotation

### Dependency

No preceding function needs to be carried out.

### Endpoint {% debug uid="RefundQuotation_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/refundQuotation.do](https://sandbox.atriptech.com/refundQuotation.do)

## Request

{% tabs %}
{% tab title="Schema" %}
*   **cid **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Identifier of client and user.
*   **orderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Original order number.
*   **refundRequestList Array<**<mark style="color:blue;">**RefundRequest**</mark>**> **<mark style="color:green;">**Required**</mark>

    Ticket selection of the passengers and flights which is going to refund.

    * <mark style="color:blue;">**RefundRequest**</mark>**  **<mark style="color:green;">**Required**</mark>
      *   **lastName **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          Last name of the passenger who wants to refund
      *   **firstName **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          First name of the passenger who wants to refund
      * **segments** **Array<**<mark style="color:blue;">**SegmentElement**</mark>\*\*> <mark style="color:blue;">**\*\*\*\***</mark> \*\*<mark style="color:green;">**Required**</mark>
        * <mark style="color:blue;">**SegmentElement**</mark>
          *   **depAirport **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

              Departure airport of the segment which the passenger wants to refund
          *   **arrAirport **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

              Arrival airport of the segment which the passenger wants to refund
          *   **depDate **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

              Departure date of the segment which the passenger wants to refund
          *   **flightNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

              Flight number of the segment which the passenger wants to refund
{% endtab %}

{% tab title="Samples" %}
```json
{
    "cid":"XXXXXXXX",
    "orderNo":"XPFIW20220209163159425",
    "refundRequestList":[
        {
            "lastName":"TEST",
            "firstName":"ONE",
            "segments":[
                {
                    "depDate":"20220302",
                    "flightNo":"5J562",
                    "depAirport":"CEB",
                    "arrAirport":"MNL"
                }
            ]
        },
        {
            "lastName":"TEST",
            "firstName":"THREE",
            "segments":[
                {
                    "depDate":"20220302",
                    "flightNo":"5J562",
                    "depAirport":"CEB",
                    "arrAirport":"MNL"
                }
            ]
        }
    ]
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
*   **status **<mark style="color:blue;">**int**</mark>

    0: success

    2: System error
    
*   **msg **<mark style="color:blue;">**string**</mark>

    Error message.
    
    The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to         check the result.

*   **isRefundable **<mark style="color:blue;">**boolean**</mark>

    True : Refundable

    False: Non-Refundable
*   **currency **<mark style="color:blue;">**string**</mark>

    The currency of the fares and amount below.
*   **originalTotalFareAmount **<mark style="color:blue;">**decimal**</mark>

    Original fare of the selected passengers and flights
*   **originalTotalAncillaryAmount **<mark style="color:blue;">**decimal**</mark>

    Original amount of ancillaries related to the selected passengers and flights
*   **originalTotalAmount **<mark style="color:blue;">**decimal**</mark>

    \= originalTotalFareAmount + originalTotalAncillaryAmount
*   **airlinePenaltyAmountForFare **<mark style="color:blue;">**decimal**</mark>

    Airline's penalty amount for the fare
*   **airlinePenaltyAmountForAncillaries **<mark style="color:blue;">**decimal**</mark>

    Airline's penalty amount for the ancillaries
*   **airlinePenaltyAmount **<mark style="color:blue;">**decimal**</mark>

    \= airlinePenaltyAmountForFare + airlinePenaltyAmountForAncillaries
*   **estimatedRefundAmount **<mark style="color:blue;">**string**</mark>

    Estimated amount which can be got back for this refund.
    
{% hint style="info" %}
Estimated amount is calculated using the current time+12 hours to match airline rules. This is to reserve time for Atlas to go to the airline to process the refund.
{% endhint %}

    
*   **transactionFee **<mark style="color:blue;">**decimal**</mark>

    The transaction fees for this refund.
*   **refundOfferId **<mark style="color:blue;">**string**</mark>

    Refund offer id for this quotation which can be used for the coming refund call.

    
 
{% endtab %}

{% tab title="Samples" %}
```
{
    "status": 0,
    "msg": "success",
    "isRefundable": true,
    "currency": "USD",
    "originalTotalFareAmount": 37.14,
    "originalTotalAncillaryAmount": 8.12,
    "originalTotalAmount": 45.26,
    "airlinePenaltyAmountForFare": 0.00,
    "airlinePenaltyAmountForAncillaries": 0.00,
    "airlinePenaltyAmount": 0.00,
    "estimatedRefundAmount": 45.26,
    "transactionFee": 2.00,
    "refundOfferId": "7961ab5b202642628e9595498ffea083"   
}
```
{% endtab %}
{% endtabs %}
