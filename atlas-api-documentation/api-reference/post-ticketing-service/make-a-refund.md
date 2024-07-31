# Make a Refund

### Dependency

Refund quotation function should be called in prior of this call

### Endpoint {% debug uid="refund_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/refund.do](https://sandbox.atriptech.com/refund.do)

## Request

{% tabs %}
{% tab title="Schema" %}
*   **orderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Original order number.
*   **refundOfferId **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Get this from the refund quotation response.
{% endtab %}

{% tab title="Samples" %}
```json
{
    "orderNo": "ZNMKU20220119160129691",
    "refundOfferId":"7961ab5b202642628e9595498ffea083"
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
*   **refundStatus **<mark style="color:blue;">**int**</mark>

   The present status of the refund.

    The options are:

    0: Submitted (The customer has submitted to Atlas)

    1: Airline processing (Submitted to airline by Atlas)

    2: Refunded

    3: Rejected
    
    **msg **<mark style="color:blue;">**string**</mark>

    Error message.
    
    The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to check the result.
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
*   **transactionFee **<mark style="color:blue;">**decimal**</mark>

    The transaction fees for this refund.
*   **refundOfferId **<mark style="color:blue;">**string**</mark>

    Refund offer id for this quotation which can be used for the coming refund call.
*   **refundStatus **<mark style="color:blue;">**int**</mark>

    0 : InProcessing

    1: Processed

    2: Completed(Means the money back or the voucher forwarded)
*   **refundCode **<mark style="color:blue;">**int**</mark>

    Refund order number generated for this refund request.
*   **cancelReason **<mark style="color:blue;">**string**</mark>

    The reason why the refund was cancelled.

    The refund reasons are:

    Not satisfy the condition

    Booking not flight changed

    Voluntary non-refundable

    Fare rules are non-refundable

    Only vendor refunds available

    Only voucher refunds available

    The user cancels the refund

    Ticket already used

    Excel refund

    Reapply

    Refund by yourself

    Need contact airline yourself

    Checked in

    No money to return

    Payment with client VCC

    Eng - voluntary cancellation
    
{% endtab %}

{% tab title="Samples" %}
```
{
    "refundStatus": 0,
    "refundCode": "202407-0028",
    "cancelReason": "",
    "currency": "USD",
    "originalTotalFareAmount": 103.66,
    "originalTotalAncillaryAmount": 0.00,
    "originalTotalAmount": 103.66,
    "airlinePenaltyAmountForFare": 5.86,
    "airlinePenaltyAmountForAncillaries": 0.00,
    "airlinePenaltyAmount": 5.86,
    "estimatedRefundAmount": 97.80,
    "transactionFee": 2.23,
    "refundOfferId": "q_7dd86f06ce794a0bb1ed8a22eca2167d",
    "isRefundable": true,
    "refundTickets": [
        {
            "lastName": "222",
            "firstName": "222",
            "ticketNo": "S15051",
            "currency": "USD",
            "originalFareAmount": 103.66,
            "originalAncillaryAmount": 0.00,
            "originalTotalAmount": 103.66,
            "refundableAmountForFare": 97.80,
            "refundableAmountForAncillaries": 0.00,
            "actualRefundAmount": 0.00,
            "refundReason": "1",
            "airlinePenaltyAmountForFare": 5.86,
            "airlinePenaltyAmountForAncillaries": 0.00,
            "airlinePenaltyAmount": 5.86,
            "estimatedRefundAmount": 97.80
        }
    ],
    "refundRules": [
        {
            "airline": "LJ",
            "ruleType": "1",
            "passengerType": "",
            "penaltyAmount": "1000.00 KRW",
            "penaltyPercent": 0,
            "penaltyPercentBase": null,
            "airlineFee": "0",
            "taxRefundable": true,
            "fareRefundable": true,
            "refundableAncillaries": [],
            "startMinute": 525600,
            "endMinute": 87840,
            "status": "H"
        },
        {
            "airline": "LJ",
            "ruleType": "1",
            "passengerType": "",
            "penaltyAmount": "3000.00 KRW",
            "penaltyPercent": 0,
            "penaltyPercentBase": null,
            "airlineFee": "0",
            "taxRefundable": true,
            "fareRefundable": true,
            "refundableAncillaries": [],
            "startMinute": 87840,
            "endMinute": 44640,
            "status": "H"
        },
        {
            "airline": "LJ",
            "ruleType": "1",
            "passengerType": "",
            "penaltyAmount": "4000.00 KRW",
            "penaltyPercent": 0,
            "penaltyPercentBase": null,
            "airlineFee": "0",
            "taxRefundable": true,
            "fareRefundable": true,
            "refundableAncillaries": [],
            "startMinute": 44640,
            "endMinute": 21600,
            "status": "H"
        },
        {
            "airline": "LJ",
            "ruleType": "1",
            "passengerType": "",
            "penaltyAmount": "8000.00 KRW",
            "penaltyPercent": 0,
            "penaltyPercentBase": null,
            "airlineFee": "0",
            "taxRefundable": true,
            "fareRefundable": true,
            "refundableAncillaries": [],
            "startMinute": 21600,
            "endMinute": 2880,
            "status": "H"
        },
        {
            "airline": "LJ",
            "ruleType": "1",
            "passengerType": "",
            "penaltyAmount": "10000.00 KRW",
            "penaltyPercent": 0,
            "penaltyPercentBase": null,
            "airlineFee": "0",
            "taxRefundable": true,
            "fareRefundable": true,
            "refundableAncillaries": [],
            "startMinute": 2880,
            "endMinute": 50,
            "status": "H"
        },
        {
            "airline": "LJ",
            "ruleType": "1",
            "passengerType": "",
            "penaltyAmount": "25000.00 KRW",
            "penaltyPercent": 0,
            "penaltyPercentBase": null,
            "airlineFee": "0",
            "taxRefundable": true,
            "fareRefundable": true,
            "refundableAncillaries": [],
            "startMinute": 50,
            "endMinute": 0,
            "status": "H"
        },
        {
            "airline": "LJ",
            "ruleType": "1",
            "passengerType": "",
            "penaltyAmount": "25000.00 KRW",
            "penaltyPercent": 0,
            "penaltyPercentBase": null,
            "airlineFee": "0",
            "taxRefundable": true,
            "fareRefundable": true,
            "refundableAncillaries": [],
            "startMinute": 0,
            "endMinute": -525600,
            "status": "H"
        }
    ],
    "referenceInformation": {
        "atlasPolicy": null,
        "airline": "LJ",
        "refundReason": "1",
        "airlinePolicy": null,
        "ruleAccuracy": null,
        "atlasFulfillmentDuration": null,
        "airlineRefundDuration": null
    },
    "status": 0,
    "msg": null
}
```
{% endtab %}
{% endtabs %}
