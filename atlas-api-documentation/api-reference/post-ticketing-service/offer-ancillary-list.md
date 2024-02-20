# Search Ancillary

### Dependency

No preceding function needs to be carried out.
The order should be ticketed and the departure date should be in the future.

### Endpoint {% debug uid="searchAncillary_1.0" %}{% enddebug %}


[http://sandbox.atlaslovestravel.com/secondAdditionSearch.do](http://sandbox.atlaslovestravel.com/secondAdditionSearch.do)

## Request

{% tabs %}
{% tab title="Schema" %}
*   **ticketOrderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Order number. It is an order for ticketing.

*   **ancillaryCategory **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Ancillary Category. Different categories of ancillaries need to be separately requested. Currently we only supports "Seats".
    
{% endtab %}

{% tab title="Samples" %}
```json
{
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

    The 'msg' element is for the description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to check the result.
*   **status **<mark style="color:blue;">**int**</mark>

    0: success

    2: System error

*   **sessionId **<mark style="color:blue;">**int**</mark>

    The unique identifier for this search.

    It is required when you call order function to make a reservation to identify which ancillary the client is choosing.

*   **ticketOrderNo **<mark style="color:blue;">**string**</mark>

    Order number. 
    
*   **supportCreditTransPayment **<mark style="color:blue;">**int**</mark>

    This tag is used to identify if the fare needs to be paid using the client's credit card.

    0: The credit card details will not be passed through and only pre-payment is allowed.

    1: The API will allow you to pass through client’s credit card details for payment. The customer can also use pre-payment as a method of payment.
    
*   **currency **<mark style="color:blue;">**string**</mark>

    The currency in which Atlas settles transactions with you.

*   **fromSegment Array **<mark style="color:blue;">**AncillaryElement**</mark>

    For outbound segments, same as search response.

*   **retSegment Array **<mark style="color:blue;">**AncillaryElement**</mark>

    For inbound segments, same as search response.

*   **ancillaries Array **<mark style="color:blue;">**AncillaryElement**</mark>

    Ancillary list provided for this order

    * **AncillaryProductElements**
      *   **segmentIndex **<mark style="color:blue;">**int**</mark>

          Segment sequence. It starts from 1. If it is round trip, the outbound and inbound sequence would be together.

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

          Currency for this ancillary price.

      *   **vendorPrice **<mark style="color:blue;">**string**</mark>

          The price charged by the vendor for the ancillary.  Only when supportCreditTransPayment=1, there is a value.

      *   **vendorCurrency **<mark style="color:blue;">**string**</mark>

          The currency in which the vendor charges for the ancillary.

      *   **canPurchaseWithTicket **<mark style="color:blue;">**int**</mark>

          This ancillary product can be purchased during the booking flow.

          1=Yes

          0=No

      *   **canPurchasePostTicket **<mark style="color:blue;">**int**</mark>

          This ancillary product can be purchased in the post-ticketing flow.

          1=Yes

          0=No

      *   **offerId **<mark style="color:blue;">**string**</mark>

          Reserved field, temporarily null
          
      *   **maxQty **<mark style="color:blue;">**int**</mark>

          Maximum purchase quantity per product
  
      *   **minQty **<mark style="color:blue;">**int**</mark>

          Minimum purchase quantity per product
          
      *   **categoryCode **<mark style="color:blue;">**string**</mark>

          Ancillary category code.
          
      *   **categoryCode **<mark style="color:blue;">**string**</mark>

          Ancillary code.

      *   **auxBaggageElement Array**

          Baggage information.(Temporarily not supported)

      *   **auxSeatElement Array**

          Seat information.

          *   **`rowNo`  **<mark style="color:blue;">**int**</mark>
     
          Row number of the seat.

          *   **`seatNo`  **<mark style="color:blue;">**string**</mark>
     
          Seat Number
          
          *   **`status`  **<mark style="color:blue;">**boolean**</mark>
     
          true: Available seat.
          
          false: Unavailable seat.

          *   **`seatInfo Array`  **<mark style="color:blue;">**
     
          Seat information description

          Seat position information：

          window

          aisle

          middle

          Required. This can be used to draw seat maps.

          other information. For example; "exit".

          *   **` passengerType`  **<mark style="color:blue;">**

          Passenger types supported by seats.


{% endtab %}

{% tab title="Samples" %}
```json
{
    "status": 0,
    "msg": "success",
    "sessionId": "46869eec-d9b2-4e43-84eb-54651309f80c",
    "ticketOrderNo": "TESTG20230719153539616",
    "supportCreditTransPayment": "0",
    "currency": "USD",
    "fromSegments": [
        {
            "segmentIndex": 1,
            "carrier": "JT",
            "flightNumber": "JT656",
            "depAirport": "CGK",
            "depTime": "202308050500",
            "arrAirport": "LOP",
            "arrTime": "202308050800",
            "stopCities": "",
            "duration": 120,
            "codeShare": false,
            "cabin": "",
            "cabinClass": 1,
            "seatCount": 4,
            "aircraftCode": "",
            "depTerminal": "",
            "arrTerminal": "",
            "operatingCarrier": "",
            "operatingFlightnumber": "",
            "fareFamily": "Economy"
        },
        {
            "segmentIndex": 2,
            "carrier": "JT",
            "flightNumber": "JT645",
            "depAirport": "LOP",
            "depTime": "202308050845",
            "arrAirport": "SUB",
            "arrTime": "202308050850",
            "stopCities": "",
            "duration": 65,
            "codeShare": false,
            "cabin": "",
            "cabinClass": 1,
            "seatCount": 4,
            "aircraftCode": "",
            "depTerminal": "",
            "arrTerminal": "",
            "operatingCarrier": "",
            "operatingFlightnumber": "",
            "fareFamily": "Economy"
        }
    ],
    "retSegments": [],
    "ancillaryProductElements": [
        {
            "segmentIndex": 1,
            "endSegmentIndex": null,
            "productCode": "AD_SEAT_1A_JT656",
            "productName": "Seat",
            "productType": 6,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 3.50,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 1.50,
            "clientTechnicalServiceFeeMode": "PER_SEGMENT",
            "auxBaggageElement": null,
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "Seat",
            "ancillaryCode": "AD_SEAT_1A_JT656",
            "auxSeatElement": {
                "rowNo": "1",
                "seatNo": "1A",
                "status": true,
                "seatInfo": [
                    "window",
                    "exit"
                ],
                "passengerType": [
                    "ADT",
                    "CHD"
                ]
            }
        },
        {
            "segmentIndex": 1,
            "endSegmentIndex": null,
            "productCode": "AD_SEAT_2A_JT656",
            "productName": "Seat",
            "productType": 6,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 62.45,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 1.50,
            "clientTechnicalServiceFeeMode": "PER_SEGMENT",
            "auxBaggageElement": null,
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "Seat",
            "ancillaryCode": "AD_SEAT_2A_JT656",
            "auxSeatElement": {
                "rowNo": "2",
                "seatNo": "2A",
                "status": true,
                "seatInfo": [
                    "window",
                    "exit"
                ],
                "passengerType": [
                    "ADT",
                    "CHD"
                ]
            }
        },
        {
            "segmentIndex": 1,
            "endSegmentIndex": null,
            "productCode": "AD_SEAT_3A_JT656",
            "productName": "Seat",
            "productType": 6,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 54.29,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 1.50,
            "clientTechnicalServiceFeeMode": "PER_SEGMENT",
            "auxBaggageElement": null,
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "Seat",
            "ancillaryCode": "AD_SEAT_3A_JT656",
            "auxSeatElement": {
                "rowNo": "3",
                "seatNo": "3A",
                "status": true,
                "seatInfo": [
                    "window",
                    "exit"
                ],
                "passengerType": [
                    "ADT",
                    "CHD"
                ]
            }
        },
        {
            "segmentIndex": 1,
            "endSegmentIndex": null,
            "productCode": "AD_SEAT_4A_JT656",
            "productName": "Seat",
            "productType": 6,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 9.53,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 1.50,
            "clientTechnicalServiceFeeMode": "PER_SEGMENT",
            "auxBaggageElement": null,
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "Seat",
            "ancillaryCode": "AD_SEAT_4A_JT656",
            "auxSeatElement": {
                "rowNo": "4",
                "seatNo": "4A",
                "status": true,
                "seatInfo": [
                    "window",
                    "exit"
                ],
                "passengerType": [
                    "ADT",
                    "CHD"
                ]
            }
        },
        {
            "segmentIndex": 2,
            "endSegmentIndex": null,
            "productCode": "AD_SEAT_1A_JT645",
            "productName": "Seat",
            "productType": 6,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 17.16,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 1.50,
            "clientTechnicalServiceFeeMode": "PER_SEGMENT",
            "auxBaggageElement": null,
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "Seat",
            "ancillaryCode": "AD_SEAT_1A_JT645",
            "auxSeatElement": {
                "rowNo": "1",
                "seatNo": "1A",
                "status": true,
                "seatInfo": [
                    "window",
                    "exit"
                ],
                "passengerType": [
                    "ADT",
                    "CHD"
                ]
            }
        },
        {
            "segmentIndex": 2,
            "endSegmentIndex": null,
            "productCode": "AD_SEAT_2A_JT645",
            "productName": "Seat",
            "productType": 6,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 3.38,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 1.50,
            "clientTechnicalServiceFeeMode": "PER_SEGMENT",
            "auxBaggageElement": null,
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "Seat",
            "ancillaryCode": "AD_SEAT_2A_JT645",
            "auxSeatElement": {
                "rowNo": "2",
                "seatNo": "2A",
                "status": true,
                "seatInfo": [
                    "window",
                    "exit"
                ],
                "passengerType": [
                    "ADT",
                    "CHD"
                ]
            }
        },
        {
            "segmentIndex": 2,
            "endSegmentIndex": null,
            "productCode": "AD_SEAT_3A_JT645",
            "productName": "Seat",
            "productType": 6,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 19.64,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 1.50,
            "clientTechnicalServiceFeeMode": "PER_SEGMENT",
            "auxBaggageElement": null,
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "Seat",
            "ancillaryCode": "AD_SEAT_3A_JT645",
            "auxSeatElement": {
                "rowNo": "3",
                "seatNo": "3A",
                "status": true,
                "seatInfo": [
                    "window",
                    "exit"
                ],
                "passengerType": [
                    "ADT",
                    "CHD"
                ]
            }
        },
        {
            "segmentIndex": 2,
            "endSegmentIndex": null,
            "productCode": "AD_SEAT_4A_JT645",
            "productName": "Seat",
            "productType": 6,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 7.28,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 1.50,
            "clientTechnicalServiceFeeMode": "PER_SEGMENT",
            "auxBaggageElement": null,
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "Seat",
            "ancillaryCode": "AD_SEAT_4A_JT645",
            "auxSeatElement": {
                "rowNo": "4",
                "seatNo": "4A",
                "status": true,
                "seatInfo": [
                    "window",
                    "exit"
                ],
                "passengerType": [
                    "ADT",
                    "CHD"
                ]
            }
        }
    ]
}
```
{% endtab %}
{% endtabs %}


