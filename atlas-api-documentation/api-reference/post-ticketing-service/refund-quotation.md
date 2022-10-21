# Refund Quotation

### Dependency

No preceding function needs to be carried out.

### Endpoint

[https://sandbox.atlaslovestravel.com/RefundQuotation.do](https://sandbox.atlaslovestravel.com/getTicketRefundFee.do)

## Request

{% tabs %}
{% tab title="Schema" %}
*   #### cid                                  <mark style="color:blue;">string</mark>                                                                                                 <mark style="color:green;">Required</mark>

    Identifier of client and user.
*   #### orderNo                       <mark style="color:blue;">string</mark>                                                                                                  <mark style="color:green;">Required</mark>

    Original order number.
*   #### refundRequestList                    Array<<mark style="color:blue;">RefundRequest</mark>>                                          <mark style="color:blue;"></mark>                                          <mark style="color:green;">Required</mark>

    Ticket selection of the passengers and flights which is going to refund.

    * #### <mark style="color:blue;">RefundRequest</mark>        <mark style="color:blue;"></mark>                                                                                                       <mark style="color:green;">Required</mark>
      *   #### lastName                       <mark style="color:blue;">string</mark>                                                                                 <mark style="color:green;">Required</mark>

          Last name of the passenger who wants to refund
      *   #### firstName                       <mark style="color:blue;">string</mark>                                                                                <mark style="color:green;">Required</mark>

          First name of the passenger who wants to refund
      * **segments**                   **Array<**<mark style="color:blue;">**SegmentElement**</mark>**>                                      **<mark style="color:blue;">****</mark>**                                      **<mark style="color:green;">**Required**</mark>
        * <mark style="color:blue;">**SegmentElement**</mark>
          *   #### depAirport                     <mark style="color:blue;">string</mark>                                                                 <mark style="color:green;">Required</mark>

              Departure airport of the segment which the passenger wants to refund
          *   #### arrAirport                       <mark style="color:blue;">string</mark>                                                                 <mark style="color:green;">Required</mark>

              Arrival airport of the segment which the passenger wants to refund
          *   #### depDate                          <mark style="color:blue;">string</mark>                                                                  <mark style="color:green;">Required</mark>

              Departure date of the segment which the passenger wants to refund
          *   #### flightNo                           <mark style="color:blue;">string</mark>                                                                  <mark style="color:green;">Required</mark>

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
*   #### msg                                                                          <mark style="color:blue;">string</mark>                                                                                                &#x20;

    Error message.
*   #### status                                                                      <mark style="color:blue;">int</mark>                                                                                                      &#x20;

    0: success

    2: System error
*   #### isRefundable                                                       <mark style="color:blue;">boolean</mark>                                                                               &#x20;

    True : Refundable

    False: Non-Refundable
*   #### currency                                                                <mark style="color:blue;">string</mark>                                                                               &#x20;

    The currency of the fares and amount below.
*   #### originalTotalFareAmount                              <mark style="color:blue;">decimal</mark>                                                                               &#x20;

    Original fare of the selected passengers and flights
*   #### originalTotalAncillaryAmount                     <mark style="color:blue;">decimal</mark>                                                                               &#x20;

    Original amount of ancillaries related to the selected passengers and flights
*   #### originalTotalAmount                                       <mark style="color:blue;">decimal</mark>                                                                               &#x20;

    \= originalTotalFareAmount + originalTotalAncillaryAmount
*   #### airlinePenaltyAmountForFare                     <mark style="color:blue;">decimal</mark>                                                                               &#x20;

    Airline's penalty amount for the fare
*   #### airlinePenaltyAmountForAncillaries        <mark style="color:blue;">decimal</mark>                                                                               &#x20;

    Airline's penalty amount for the ancillaries
*   #### airlinePenaltyAmount                                     <mark style="color:blue;">decimal</mark>                                                                               &#x20;

    \= airlinePenaltyAmountForFare + airlinePenaltyAmountForAncillaries
*   #### estimatedRefundAmount                             <mark style="color:blue;">string</mark>                                                                               &#x20;

    Estimated amount which can be got back for this refund.
*   #### transactionFee                                                   <mark style="color:blue;">decimal</mark>                                                                               &#x20;

    The transaction fees for this refund.
*   #### refundOfferId                                                      <mark style="color:blue;">string</mark>

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
