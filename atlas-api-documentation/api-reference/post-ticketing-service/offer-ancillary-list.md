# Offer Ancillary List

### Dependency

No preceding function needs to be carried out.

### Endpoint

[https://sandbox.atlaslovestravel.com/searchAncillary.do](https://sandbox.atlaslovestravel.com/searchAncillary.do)

## Request

{% tabs %}
{% tab title="Schema" %}
*   #### cid                                  <mark style="color:blue;">string</mark>                                                                                                 <mark style="color:green;">Required</mark>

    Identifier of client and user.
*   #### orderNo                       <mark style="color:blue;">string</mark>                                                                                                 <mark style="color:green;">Required</mark>

    Order number. It can be an order for ticketing, or an order for add bags. The format of each kind of order is different.
{% endtab %}

{% tab title="Samples" %}
```json
{
    "cid": "XXXXXXXX",
    "orderNo": "GXFDU20220117075403790"
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
*   #### msg                                      <mark style="color:blue;">string</mark>                                                                                                &#x20;

    Error message.
*   #### status                                  <mark style="color:blue;">int</mark>                                                                                                      &#x20;

    0: success

    2: System error
*   #### orderNo                                      <mark style="color:blue;">string</mark>                                                                                                &#x20;

    Error message.
*   #### ancillaries                                 Array\<AncillaryElement>                                                                     <mark style="color:blue;"></mark>                                                                    &#x20;

    Ancillary list provided for this order

    * #### AncillaryElement
      *   #### segmentIndex                                      <mark style="color:blue;">int</mark>                                           &#x20;

          Segment sequence, start from 1. If it is round trip, sequence outbond and inbound together
      *   #### productCode                                      <mark style="color:blue;">string</mark>                                                &#x20;

          Unique identifier for the ancillary product.
      *   #### productName                                      <mark style="color:blue;">string</mark>                                             &#x20;

          Ancillary product name.
      *   #### productType                                      <mark style="color:blue;">string</mark>                                                &#x20;

          Ancillary product type.

          1: baggage

          Currently only baggage is available
      *   #### price                                      <mark style="color:blue;">string</mark>                                              &#x20;

          Price for this ancillary.
      *   #### currency                                      <mark style="color:blue;">string</mark>                                        &#x20;

          Currency for this price.
      *   #### auxBaggageElement                                     <mark style="color:blue;"></mark>                                         &#x20;

          Baggage information

          *   #### piece                                      <mark style="color:blue;">string</mark>                                               &#x20;

              0：No Limitation about piece;

              \>0 : Maximum pieces.
          *   #### weight                                      <mark style="color:blue;">string</mark>                                                    &#x20;

              Maximum weight for ancillary baggage, should be greater than 0.
          *   #### isAllWeight                                      <mark style="color:blue;">string</mark>                                              &#x20;

              True：The weight is for all the pieces;

              False：The weight is for each piece.
      *   #### offerId                                      <mark style="color:blue;">string</mark>                                       &#x20;

          unique identifier for this ancillary's offer, used for the following order ancillary function.
{% endtab %}

{% tab title="Samples" %}
```json
{
    "status": 0,
    "msg": "success",
    "orderNo": "GXFDU20220117075403790",
    "ancillaries": [
        {
            "segmentIndex": 1,
            "productCode": "SCI_BAG_ID_10KG_AABBBB",
            "productName": "Baggage",
            "productType": 1,
            "price": 195.40,
            "currency": "USD",
            "auxBaggageElement": {
                "piece": 0,
                "weight": 10,
                "isAllWeight": true
            },
            "offerId": "25abbe50aaaf4d559fd7e2d21667d337"
        },
        {
            "segmentIndex": 1,
            "productCode": "SCI_BAG_ID_20KG_AABBBB",
            "productName": "Baggage",
            "productType": 1,
            "price": 233.17,
            "currency": "USD",
            "auxBaggageElement": {
                "piece": 0,
                "weight": 20,
                "isAllWeight": true
            },
            "offerId": "67c54bade38d40fd9ad8bfbddef5d5da"
        },
        {
            "segmentIndex": 1,
            "productCode": "SCI_BAG_ID_25KG_AABBBB",
            "productName": "Baggage",
            "productType": 1,
            "price": 270.94,
            "currency": "USD",
            "auxBaggageElement": {
                "piece": 0,
                "weight": 20,
                "isAllWeight": true
            },
            "offerId": "3007ca5972b6499e9a3d189c68155420"
        }
    ]
}
```
{% endtab %}
{% endtabs %}

###
