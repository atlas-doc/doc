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
            "actualRefundAmount": 0.00,
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
