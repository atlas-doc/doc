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
*  **refundStatus **<mark style="color:blue;">**int**</mark>

   The present status of the refund.

    The options are:

    0: Submitted (The customer has submitted to Atlas)

    1: Airline processing (Submitted to airline by Atlas)

    2: Refunded

    3: Rejected

*   **status **<mark style="color:blue;">**int**</mark>

    0: success

    2: System error
    
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
*   **estimatedRefundAmount **<mark style="color:blue;">**decimal**</mark>

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

    Does not match airline policy

    There is no schedule change from the airline side. Please refer the ticket Fare Rules available in ATRIP flight deck for cancellation charges.

    Voluntary Cancellation - Non-Refundable

    As per airline policy, only voucher refund is available for the ticket

    Refund request cancelled by the user

    Travel has been completed by the passenger

    Refund not yet received from the airline. Please try again later.
    
{% endtab %}

{% tab title="Samples" %}
```
{
    "refundStatus": 0,
    "refundCode": "202408-0006",
    "cancelReason": "",
    "currency": "USD",
    "originalTotalFareAmount": 141.19,
    "originalTotalAncillaryAmount": 381.00,
    "originalTotalAmount": 522.19,
    "airlinePenaltyAmountForFare": 66.20,
    "airlinePenaltyAmountForAncillaries": 381.00,
    "airlinePenaltyAmount": 447.20,
    "estimatedRefundAmount": 74.99,
    "transactionFee": 2.00,
    "refundOfferId": "q_9e08be9b670c4ba590704d99b3650113",
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
            "startMinute": 0,
            "endMinute": -525600
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
