# Offer Ancillary List

### Dependency

No preceding function needs to be carried out.

### Endpoint {% debug uid="searchAncillary_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/searchAncillary.do](https://sandbox.atriptech.com/searchAncillary.do)

## Request

{% tabs %}
{% tab title="Schema" %}
*   **cid **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Identifier of client and user.
*   **ticketOrderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Order number. It is an order for ticketing.

*   **ancillaryCategory **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Ancillary Category. Different categorys of ancillary need to be separate requested. Currently only supports [SEAT]
    
{% endtab %}

{% tab title="Samples" %}
```json
{
    "cid": "XXXXXXXX",
    "ticketOrderNo": "GXFDU20220117075403790",
    "ancillaryCategory": "SEAT"
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
*   **msg **<mark style="color:blue;">**string**</mark>

    The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to         check the result.
*   **status **<mark style="color:blue;">**int**</mark>

    0: success

    2: System error

*   **sessionId **<mark style="color:blue;">**int**</mark>

    The unique identifier for this search.

    It is required when you call order function to make a reservation to identify which ancillary the client is choosing.

*   **ticketOrderNo **<mark style="color:blue;">**string**</mark>

    Order number. It is an order for ticketing.
    
*   **supportCreditTransPayment **<mark style="color:blue;">**int**</mark>

    This tag is used to identify if the fare needs to be paid using the client's credit card.

    0: The credit card details will not be passed through and only pre-payment is allowed.

    1: The API will allow you to pass through client’s credit card details for payment. The customer can also use pre-payment as a method of payment.
    
*   **currency **<mark style="color:blue;">**string**</mark>

    The currency in which Atlas settles transactions with you.

*   **fromSegment Array **<mark style="color:blue;">**AncillaryElement**</mark>

    For outbound segments, click [<mark style="color:red;">**here**</mark> ](search.md#segment-element-schema)to check the schema.

*   **retSegment Array **<mark style="color:blue;">**AncillaryElement**</mark>

    For inbound segments, click [<mark style="color:red;">**here**</mark> ](search.md#segment-element-schema)to check the schema.

*   **ancillaries Array **<mark style="color:blue;">**AncillaryElement**</mark>

    Ancillary list provided for this order

    * **AncillaryProductElements**
      *   **segmentIndex **<mark style="color:blue;">**int**</mark>

          Segment sequence, start from 1. If it is round trip, sequence outbond and inbound together

      *   **endSegmentIndex **<mark style="color:blue;">**int**</mark>

          The last segment for which this information is applicable.

      *   **productCode **<mark style="color:blue;">**string**</mark>

          Unique identifier for the ancillary product.
      *   **productName **<mark style="color:blue;">**string**</mark>

          Ancillary product name.
      *   **productType **<mark style="color:blue;">**string**</mark>

          Ancillary product type.

          1: Check-in baggage
          3: Cabin Baggage Overhead Locker
          6: Seat

          Currently only Seat is available.
          
      *   **price **<mark style="color:blue;">**string**</mark>

          Price for this ancillary.
      *   **currency **<mark style="color:blue;">**string**</mark>

          Currency for this price.

      *   **vendorPrice **<mark style="color:blue;">**string**</mark>

          The price charged by the vendor for the ancillary.  Only when supportCreditTransPayment=1, there is a value.

      *   **vendorCurrency **<mark style="color:blue;">**string**</mark>

          The currency in which the vendor charges for the ancillary.

      *   **canPurchaseWithTicket **<mark style="color:blue;">**int**</mark>

          This ancillary product can be purchased during the booking flow.

          1=Yes; 0=No

      *   **canPurchasePostTicket **<mark style="color:blue;">**int**</mark>

          This ancillary product can be purchased in the post-ticketing flow.

          1=Yes; 0=No

      *   **offerId **<mark style="color:blue;">**string**</mark>

          Reserved field, temporarily null
          
      *   **maxQty **<mark style="color:blue;">**int**</mark>

          Maximum purchase quantity per product
  
      *   **minQty **<mark style="color:blue;">**int**</mark>

          Starting purchase quantity per product
          
      *   **categoryCode **<mark style="color:blue;">**string**</mark>

          Ancillary category code.
          
      *   **categoryCode **<mark style="color:blue;">**string**</mark>

          Ancillary code.

      *   **auxBaggageElement Array**

          Baggage information.(Temporarily not supported)

      *   **auxSeatElement Array**

          Seat information.

          *   **`rowNo`  **<mark style="color:blue;">**int**</mark>
     
          Which row are the seat in

          *   **`seatNo`  **<mark style="color:blue;">**string**</mark>
     
          Seat Number
          
          *   **`status`  **<mark style="color:blue;">**boolean**</mark>
     
          true: Available seat.
          false: Unavailable seat.

          *   **`seatInfo Array`  **<mark style="color:blue;">**
     
          Seat information description

          position information：window/aisle/middle  Required, used to draw seat maps.

          other information,such as "exit".

          *   **` passengerType`  **<mark style="color:blue;">**

          Passenger types supported by seats.


          

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
