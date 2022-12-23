# Make a Refund

### Dependency

Refund quotation function should be called in prior of this call

### Endpoint {% debug uid="refund_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/refund.do](https://sandbox.atriptech.com/refund.do)

## Request

{% tabs %}
{% tab title="Schema" %}
*   **cid **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Identifier of client and user.
*   **orderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Original order number.
*   **refundOfferId **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Get this from the refund quotation response.
{% endtab %}

{% tab title="Samples" %}
```json
{
    "cid": "XXXXXXXX",
    "orderNo": "ZNMKU20220119160129691",
    "refundOfferId":"7961ab5b202642628e9595498ffea083"
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
    
    **msg **<mark style="color:blue;">**string**</mark>

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
*   **transactionFee **<mark style="color:blue;">**decimal**</mark>

    The transaction fees for this refund.
*   **refundOfferId **<mark style="color:blue;">**string**</mark>

    Refund offer id for this quotation which can be used for the coming refund call.
*   **refundStatus **<mark style="color:blue;">**int**</mark>

    0 : InProcessing

    1: Processed

    2: Completed(Means the money back or the voucher forwarded)
{% endtab %}

{% tab title="Samples" %}
```
{
    "status": 0,
    "msg": "success"
    "refundStatus": 0,
    "currency": "USD",
    "originalTotalFareAmount": 37.14,
    "originalTotalAncillaryAmount": 8.12,
    "originalTotalAmount": 45.26,
    "airlinePenaltyAmountForFare": 0.00,
    "airlinePenaltyAmountForAncillaries": 0.00,
    "airlinePenaltyAmount": 0.00,
    "estimatedRefundAmount": 45.26,
    "transactionFee": 2.00,
    "refundOfferId": "7961ab5b202642628e9595498ffea083",
    "isRefundable": true   
}
```
{% endtab %}
{% endtabs %}
