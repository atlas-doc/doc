# Refund Complete Notification

### Refund Complete Notification Webhook

When a ticket or ancillary service is cancelled, you will receive the `order.refundComplete` notification on your server.

EndPoint ： The URL you configured to receive notifications

Method : Post

{% tabs %}
{% tab title="Schema" %}
*   #### msg                                                                        <mark style="color:blue;">string</mark>                                                                                                

    Error message.
*   #### status                                                                    <mark style="color:blue;">int</mark>                                                                                                      

    0: success

    2: System error
*   #### currency                                                                <mark style="color:blue;">string</mark>                                                                               

    currency
*   #### originalTotalFare                                               <mark style="color:blue;">decimal</mark>                                                                               

    Original fare of the selected passengers and flights
*   #### originalTotalAncillaryAmount                     <mark style="color:blue;">decimal</mark>                                                                               

    Original amount of ancillaries related to the selected passengers and flights
*   #### airlinePenaltyAmountForFare                     <mark style="color:blue;">decimal</mark>                                                                               

    Airline's penalty amount for the fare
*   #### airlinePenaltyAmountForAncillaries        <mark style="color:blue;">decimal</mark>                                                                               

    Airline's penalty amount for the ancillaries
*   #### finalRefundAmount                                         <mark style="color:blue;">string</mark>                                                                               

    Final refund amount.
*   #### transactionFee                                                   <mark style="color:blue;">decimal</mark>                                                                               

    Technical service fee for this transaction
*   #### refundStatus                                                       <mark style="color:blue;">int</mark>                                                                               

    2:  Completed(Means the refund amount has credted on your account)
{% endtab %}

{% tab title="Samples" %}
```
{
    "cid": "XXXXXXXX",
    "orderNo": "ZNMKU20220119160129691",
    "currency": "USD",
    "originalTotalFare": 37.32,
    "originalTotalAncillaryAmount": 10,
    "originalTotalAmount": 47.32,
    "airlinePenaltyAmountForFare": 5,
    "airlinePenaltyAmountForAncillaries": 0,
    "airlinePenaltyAmount":0,
    "finalRefundAmount":37.32,
    "transactionFee": 2,
    "refundStatus": 2
}
```


{% endtab %}
{% endtabs %}
