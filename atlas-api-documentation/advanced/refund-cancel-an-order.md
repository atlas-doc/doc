# Refund/Cancel an Order

To process a cancellation request, you need to provide the `OrderNo` of the order you'd like to cancel. Please note, not all airlines will offer cancellation services.

![](../../.gitbook/assets/FlowChart\_4\_Refund\_CancelOrder.png)

## 1. Refund Quotation

Send the `orderNo`, along with the passengers' names and segment information such as `depAirport`, `arrAirport`, `depDate` and `flightNo`. Atlas charges a transaction fee on top of the amount deducted by airlines for every refund request.

EndPoint ：  [https://sandbox.atlaslovestravel.com/refundQuotation.do](https://sandbox.atlaslovestravel.com/refundQuotation.do)

Method : Post

Header:

```
x-atlas-client-id ： <Your clientid>
x-atlas-client-secret : <Your client secretid>
Content-Type: application/json
Accept-Encoding: gzip
```

{% tabs %}
{% tab title="Request" %}
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

{% tab title="Response" %}
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

## 2. Refund

When your customer confirms the refund quote, send the request schema with `refundOfferID` to the refund endpoint to confirm the refund request.

EndPoint ：  [https://sandbox.atlaslovestravel.com/refund.do](https://sandbox.atlaslovestravel.com/refund.do)

Method : Post

Header:

```
x-atlas-client-id ： <Your clientid>
x-atlas-client-secret : <Your client secretid>
Content-Type: application/json
Accept-Encoding: gzip
```

{% tabs %}
{% tab title="Request" %}
```json
{
    "cid": "XXXXXXXX",
    "orderNo": "XPFIW20220209163159425",
    "refundOfferId":"xxxxxxxxxxxxxxxxxxxxx"
}
```
{% endtab %}

{% tab title="Response" %}
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

## 3. Refund Status Notification

With Atlas, you can configure webhooks to automatically receive notifications for ticket cancellations/refunds along with the amount refunded. Once you receive `order.refundCompleted` notification on the server for a cancelled booking, you can take action as needed.

EndPoint : The URL you configured to receive notifications&#x20;

Method : Post

{% tabs %}
{% tab title="Samples" %}
```json
{
    "cid":"XXXXXXXX",
    "type":"order.refundComplete",
    "data":{
         "orderNo":"PSTEV20220119165629057",
         "refundStatus":"2",
         "currency": "USD",
         "originalTotalFare": 37.32,
         "originalTotalAncillaryAmount": 10,
         "originalTotalAmount": 47.32,
         "airlinePenaltyAmountForFare": 5,
         "airlinePenaltyAmountForAncillaries": 0,
         "airlinePenaltyAmount":0,
         "finalRefundAmount":37.32,
         "transactionFee": 2
    }
}    
```
{% endtab %}
{% endtabs %}

