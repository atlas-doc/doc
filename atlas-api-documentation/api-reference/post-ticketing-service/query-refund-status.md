# Query Refund Status 

### Dependency

No preceding function needs to be carried out.

### Endpoint {% debug uid="RefundQuery_1.0" %}{% enddebug %}
    
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
*   **refundOrders **<mark style="color:green;">**Required**</mark>

*   **orderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Original order number.

*   **refundCode **<mark style="color:blue;">**int**</mark>

    Refund order number generated for this refund request.

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

      *    **refundReason string **Optional

           0: Involuntary

           1: Voluntary

           2: Tax refund after departure for non-refundable tickets (Only available for limited airlines, please contact the account    managers if you are interested in this option)     
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
     *    **ruleType **<mark style="color:blue;">**string**</mark>

           Refund rule types (for the most restrictive condition):

           T: Non refundable

           H: Refundable with restrictions

           F: Free for refund  
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
      *    **startMinute **<mark style="color:blue;">**int**</mark>

           Starting time of rule application. Positive numbers represent XXX minutes before departure. Negative numbers represent XXX minutes after departure.
      *    **endMinute **<mark style="color:blue;">**int**</mark>

           Ending time of rule application. Positive numbers represent XXX minutes before departure. Negative numbers represent XXX minutes after departure.
      *   **refundStatus **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          The present status of the refund.

          The options are:

          0: Submitted (The customer has submitted to Atlas)

          1: Airline processing (Submitted to airline by Atlas)

          2: Refunded

          3: Rejected  
      *   **cancelReason **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

      The different reasons why the refund can be rejected are:

      Does not match airline policy.

      There is no schedule change from the airline side. Please refer the ticket Fare Rules available in ATRIP flight deck for cancellation charges.

      Voluntary Cancellation - Non-Refundable

      As per airline policy, only voucher refund is available for the ticket.

      Refund request cancelled by the user.

      Travel has been completed by the passenger.

      Refund not yet received from the airline. Please try again later.   
      *   **refundOfferId **<mark style="color:blue;">**string**</mark>

           Refund offer id for this quotation which can be used for the coming refund call.
      *   **status **<mark style="color:blue;">**int**</mark>

          0: success

          2: System error
    
      *   **msg **<mark style="color:blue;">**string**</mark>

          Error message.
    
          The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to check the result.
{% endtab %}

{% tab title="Samples" %}
```json
{
    "refundOrders": [
        {
            "orderNo": "TESTA20240725164512131",
            "refundCode": "202408-0006",
            "currency": "USD",
            "originalTotalFareAmount": 141.19,
            "originalTotalAncillaryAmount": 381.00,
            "originalTotalAmount": 522.19,
            "airlinePenaltyAmountForFare": 66.20,
            "airlinePenaltyAmountForAncillaries": 381.00,
            "airlinePenaltyAmount": 447.20,
            "estimatedRefundAmount": 74.99,
            "transactionFee": 2.00,
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
                    "ruleType": "1",
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
                    "ruleType": "1",
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
                    "ruleType": "1",
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
                    "ruleType": "1",
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
                    "ruleType": "1",
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
                },
                {
                    "airline": "LJ",
                    "ruleType": "1",
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
            "refundStatus": 0,
            "cancelReason": "",
            "refundOfferId": "q_9e08be9b670c4ba590704d99b3650113"
        }
    ],
    "status": 0,
    "msg": null
}


```
{% endtab %}
{% endtabs %}
