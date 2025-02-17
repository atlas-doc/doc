# Refund Quotation

### Dependency

No preceding function needs to be carried out.

### Endpoint {% debug uid="RefundQuotation_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/refundQuotation.do](https://sandbox.atriptech.com/refundQuotation.do)

{% hint style="info" %}
Please note the below while initiating a refund transaction.

1. **Refund of either inbound or outbound sector:** The full ticket needs to be refunded. Only outbound OR inbound sector cannot be refunded. Please contact the airline for the same.

2. **Refund for a partially used itinerary:** Partially used itinerary cannot be refunded. Please contact the airline for the same.

3. **Refund for a specific passenger:** We support the refund of a specific passenger in an itinerary. For example, if there are 3 passengers and only one of them is to be refunded, please send us your refund request.

4. The customer is responsible to check whether the traveler has already made ancillary purchase in the transaction. 

5. No email notifications will be sent for refunds rejected by Atlas.

{% endhint %}

## Request

{% tabs %}
{% tab title="Schema" %}
*   **orderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Original order number.
*   **airlinePNR **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    The record locator of the airline.
*   **carrier **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    2 character IATA airline code.
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

    2: Tax refund after departure for non-refundable tickets (Only available for limited airlines, please contact the account managers if you are interested in this option)

    If this field has not been populated, the default of "Voluntary (1)" refund will be used.

    
{% endtab %}

{% tab title="Samples" %}
```json
{
    "orderNo":"TESTA20240725164512131",
    "airlinePNR":"S24933",
    "carrier":"G9",
    "refundRequestList":[
        {
            "lastName":"ZHANG",
            "firstName":"SAN",
            "segments":[
                {
                    "depDate":"20240827",
                    "flightNo":"LJ820",
                    "depAirport":"PVG",
                    "arrAirport":"CJU"
                },
                {
                    "depDate":"20240828",
                    "flightNo":"LJ819",
                    "depAirport":"CJU",
                    "arrAirport":"PVG"
                }
                ],
            "refundReason":"1"
        }
    ]
}

```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
*   **orderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Original order number.
*   **status **<mark style="color:blue;">**int**</mark>

    0: success

    2: System error
    
*   **msg **<mark style="color:blue;">**string**</mark>

    Error message.
    
    The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to check the result.

*   **RefundResponse **<mark style="color:green;">**Required**</mark>

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
*   **refundTickets Array **<mark style="color:green;">**Required**</mark>

    The refund calculation for each of the passengers whose refund quote has been requested.
  *   **Journey **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>
  
      Each node denotes the direction of the journey. The first node is the outbound direction and the second node is the inbound direction.
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
      *    **originalTotalAmount **<mark style="color:blue;">**decimal**</mark>

           \= originalTotalFareAmount + originalTotalAncillaryAmount
      *    **refundableAmountForFare **<mark style="color:blue;">**decimal**</mark>

           The amount refundable from the fare.
      *    **refundableAmountForAncillaries **<mark style="color:blue;">**decimal**</mark>

           The amount refundable from the ancillaries.           
      *    **airlinePenaltyAmountForFare **<mark style="color:blue;">**decimal**</mark>

           Airline's penalty amount for the fare
      *    **airlinePenaltyAmountForAncillaries **<mark style="color:blue;">**decimal**</mark>

           Airline's penalty amount for the ancillaries
      *    **airlinePenaltyAmount **<mark style="color:blue;">**decimal**</mark>

           \= airlinePenaltyAmountForFare + airlinePenaltyAmountForAncillaries
      *    **estimatedRefundAmount **<mark style="color:blue;">**decimal**</mark>

           Estimated amount which can be got back for this refund.
*    **refundRules Array **<mark style="color:green;">**Required**</mark>

     The refund rules for the fare whose refund quote has been requested.
      *    **airline **<mark style="color:blue;">**string**</mark>

           2 character IATA code of the airline.
      *    **status **<mark style="color:blue;">**string**</mark>

           Refund rule types (for the most restrictive condition):

           T: Non refundable

           H: Refundable with restrictions

           F: Free for refund  
      *    **startMinute **<mark style="color:blue;">**int**</mark>

           Starting time of rule application. Positive numbers represent XXX minutes before departure. Negative numbers represent XXX minutes after departure.
      *    **endMinute **<mark style="color:blue;">**int**</mark>

           Ending time of rule application. Positive numbers represent XXX minutes before departure. Negative numbers represent XXX minutes after departure.
      *    **passengerType **<mark style="color:blue;">**string**</mark>

           The passenger types for whom the refund rules apply.
     *    **penaltyAmount **<mark style="color:blue;">**decimal**</mark>

           Airline cancellation fees.
     *    **penaltyPercentBase **<mark style="color:blue;">**string**</mark>

           The calculation on which the penalty percentage is based. The options are 1) fare+tax  2) fare
     *    **airlineFee **<mark style="color:blue;">**decimal**</mark>

           Airline refund fee.
     *    **taxRefundable **<mark style="color:blue;">**boolean**</mark>

           Is tax refund available?
     *    **fareRefundable **<mark style="color:blue;">**boolean**</mark>

           Is the ticket refundable?
     *    **refundableAncillaries **<mark style="color:blue;">**string**</mark>

           The list of ancillaries which are refundable.

           The options are:

           StandardCheckInBaggage

           CabinBaggage

           CabinBaggageUnderSeat

           CabinBaggageOverheadLocker
         
{% endtab %}

{% tab title="Samples" %}
```
{
    "currency": "USD",
    "originalTotalFareAmount": 141.19,
    "originalTotalAncillaryAmount": 381.00,
    "originalTotalAmount": 522.19,
    "airlinePenaltyAmountForFare": 66.20,
    "airlinePenaltyAmountForAncillaries": 381.00,
    "airlinePenaltyAmount": 447.20,
    "estimatedRefundAmount": 74.99,
    "transactionFee": 2.00,
    "refundOfferId": "q_56dec16d1fe2472095426d0286cc1965",
    "isRefundable": true,
    "refundTickets": [
        {
            "lastName": "ZHANG",
            "firstName": "SAN",
            "ticketNo": "S43484",
            "currency": "USD",
            "originalFareAmount": 141.19,
            "originalAncillaryAmount": 381.00,
            "originalTotalAmount": 522.19,
            "refundableAmountForFare": 74.99,
            "refundableAmountForAncillaries": 0.00,
            "refundReason": "1",
            "airlinePenaltyAmountForFare": 66.20,
            "airlinePenaltyAmountForAncillaries": 381.00,
            "airlinePenaltyAmount": 447.20,
            "estimatedRefundAmount": 74.99
        }
    ],
    "refundRules": [
        {
            "airline": "LJ",
            "refundReason": "1",
            "passengerType": "",
            "penaltyAmount": "480.00 CNY",
            "penaltyPercent": 0,
            "penaltyPercentBase": null,
            "airlineFee": "0",
            "taxRefundable": true,
            "fareRefundable": true,
            "refundableAncillaries": [],
            "startMinute": 525600,
            "endMinute": 50
        },
        {
            "airline": "LJ",
            "refundReason": "1",
            "passengerType": "",
            "penaltyAmount": "1280.00 CNY",
            "penaltyPercent": 0,
            "penaltyPercentBase": null,
            "airlineFee": "0",
            "taxRefundable": true,
            "fareRefundable": true,
            "refundableAncillaries": [],
            "startMinute": 50,
            "endMinute": 0
        },
        {
            "airline": "LJ",
            "refundReason": "1",
            "passengerType": "",
            "penaltyAmount": "1280.00 CNY",
            "penaltyPercent": 0,
            "penaltyPercentBase": null,
            "airlineFee": "0",
            "taxRefundable": true,
            "fareRefundable": true,
            "refundableAncillaries": [],
            "startMinute": 0,
            "endMinute": -525600
        }
    ],
    "referenceInformation": {
        "atlasPolicy": null,
        "airline": "LJ",
        "refundReason": "1",
        "airlinePolicy": null
    },
    "orderNo": "TESTA20240903015953777",
    "status": 0,
    "msg": null
}

```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Please note that the refund quote is valid for 2 hrs.
{% endhint %}
