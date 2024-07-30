    # Refund Quotation

### Dependency

No preceding function needs to be carried out.

### Endpoint {% debug uid="RefundQuotation_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/refundQuotation.do](https://sandbox.atriptech.com/refundQuotation.do)

## Request

{% tabs %}
{% tab title="Schema" %}
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
*   **refundReason **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    0: Involuntary

    1: Voluntary

    2: Post-flight tax refund

    
{% endtab %}

{% tab title="Samples" %}
```json
{
  "orderNo": "TEST20220209163159425",
  "refundRequestList": [
    {
      "firstName": "TEST",
      "lastName": "ONE",
      "segments": [
        {
          "depDate": "20220210",
          "flightNo": "RS123",
          "depAirport": "SEL",
          "arrAirport": "TYO"
        }
      ],
      "refundReason": "1"
    },
    {
      "firstName": "TEST",
      "lastName": "TWO",
      "segments": [
        {
          "depDate": "20220210",
          "flightNo": "RS123",
          "depAirport": "SEL",
          "arrAirport": "TYO"
        },
        {
          "depDate": "20220212",
          "flightNo": "RS456",
          "depAirport": "TYO",
          "arrAirport": "SEL"
        }
      ],
      "refundReason": "1"
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
    
    The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to check the result.

*   **RefundResponse**</mark>**> **<mark style="color:green;">**Required**</mark>

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
    
*   **transactionFee **<mark style="color:blue;">**decimal**</mark>

    The transaction fees for this refund.
*   **refundOfferId **<mark style="color:blue;">**string**</mark>

    Refund offer id for this quotation which can be used for the coming refund call.

*   **isRefundable **<mark style="color:blue;">**boolean**</mark>

    True : Refundable

    False: Non-Refundable

*   **refundTickets Array<**<mark style="color:blue;"> **<mark style="color:green;">**Required**</mark>

    The refund calculation for each of the passengers whose refund quote has been requested.
    
          *   **firstName **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

              First name of the passenger who wants to refund
          *   **lastName **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

              Last name of the passenger who wants to refund
          *   **ticketNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

              The PNR received from the airline in the retrieve PNR response.
          *   **currency **<mark style="color:blue;">**string**</mark>

              The currency of the fares and amount below.
          *   **originalTotalFareAmount **<mark style="color:blue;">**decimal**</mark>

              Original fare of the selected passengers and flights
          *   **originalTotalAncillaryAmount **<mark style="color:blue;">**decimal**</mark>

              Original amount of ancillaries related to the selected passengers and flights
          *   **originalTotalAmount **<mark style="color:blue;">**decimal**</mark>

              \= originalTotalFareAmount + originalTotalAncillaryAmount

          *   **refundableAmountForFare **<mark style="color:blue;">**decimal**</mark>

              The amount refundable from the fare.
          *   **refundableAmountForAncillaries **<mark style="color:blue;">**decimal**</mark>

              The amount refundable from the ancillaries.
              
          *   **airlinePenaltyAmountForFare **<mark style="color:blue;">**decimal**</mark>

              Airline's penalty amount for the fare
          *   **airlinePenaltyAmountForAncillaries **<mark style="color:blue;">**decimal**</mark>

              Airline's penalty amount for the ancillaries
          *   **airlinePenaltyAmount **<mark style="color:blue;">**decimal**</mark>

              \= airlinePenaltyAmountForFare + airlinePenaltyAmountForAncillaries
          *   **estimatedRefundAmount **<mark style="color:blue;">**string**</mark>

              Estimated amount which can be got back for this refund.

 *   **refundRules Array<**<mark style="color:blue;"> **<mark style="color:green;">**Required**</mark>

    The refund rules for the fare whose refund quote has been requested.

          
    
{% endtab %}

{% tab title="Samples" %}
```
{
  "status": 0,
  "msg": "success",
  "currency": "USD",
  "originalTotalFareAmount": 1200,
  "originalTotalAncillaryAmount": 0,
  "originalTotalAmount": 1200,
  "airlinePenaltyAmountForFare": 500,
  "airlinePenaltyAmountForAncillaries": 200,
  "airlinePenaltyAmount": 700,
  "estimatedRefundAmount": 500,
  "transactionFee": 1,
  "refundOfferId": "12610f6a-1d00-499e-9fdb-664f4b5ea60b",
  "isRefundable": true,
  "refundTickets": [
    {
      "firstName": "TEST",
      "lastName": "ONE",
      "ticketNo": "ABXSJI",
      "currency": "USD",
      "originalFareAmount": 600,
      "originalAncillaryAmount": 0,
      "originalTotalAmount": 600,
      "refundableAmountForFare": 10,
      "refundableAmountForAncillaries": 0,
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
  "refundRules": [
    {
      "airline": "RS",
      "status": "T",
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
  "referenceInformation": {
    "airline": "RS",
    "refundReason": "1",
    "atlasPolicy": "",
    "airlinePolicy": ""
  }
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
All amounts are calculated using the current time +12 hours. This is to permit the Atlas Operations Team to initiate the refund process with the airline.
Please note that the refund quote is valid for 2 hrs.
{% endhint %}
