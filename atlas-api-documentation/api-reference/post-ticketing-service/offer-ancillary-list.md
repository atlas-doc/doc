# Offer Ancillary List

### Dependency

No preceding function needs to be carried out.

### Endpoint {% debug uid="searchAncillary_1.0" %}{% enddebug %}


[http://sandbox.atlaslovestravel.com/secondAdditionSearch.do](http://sandbox.atlaslovestravel.com/secondAdditionSearch.do)

## Request

{% tabs %}
{% tab title="Schema" %}
*   **cid **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Identifier of client and user.
*   **ticketOrderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Order number. It is an order for ticketing.

*   **ancillaryCategory **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Ancillary Category. Different categories of ancillaries need to be separately requested. Currently we only supports "Seats".
    
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

    For outbound segments, click [<mark style="color:red;">**here**</mark> ](offer-ancillary.md#segment-element-schema)to check the schema.

*   **retSegment Array **<mark style="color:blue;">**AncillaryElement**</mark>

    For inbound segments, click [<mark style="color:red;">**here**</mark> ](offer-ancillary.md#segment-element-schema)to check the schema.

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

# Segment Element Schema

{% tabs %}
{% tab title="Schema" %}
**`carrier`  **<mark style="color:blue;">**string**</mark>

IATA code of airline.

**`flightNumber`  **<mark style="color:blue;">**string**</mark>

Value denotes flight number. The format is: CA123 or TR021 or FR1290, the letters denote the carrier and the three/four-digit number that follows is the flight number.

**`depAirport`  **<mark style="color:blue;">**string**</mark>

IATA code of departure airport.

**`depTime`  **<mark style="color:blue;">**string**</mark>

Departure time of the flight. The format is ：yyyyMMddHHmm, 202203100300 means 10MAR2022 03:00

**`arrAirport`  **<mark style="color:blue;">**string**</mark>

IATA code of arrival airport.

**`arrTime`  **<mark style="color:blue;">**string**</mark>

Arrival time of the flight. The format is ：yyyyMMddHHmm, 202203100300 means 10MAR2022 03:00

**`stopCities`  **<mark style="color:blue;">**string**</mark>

Name of cities from where the passengers will take connecting flights. Include IATA code of cities and use a comma in case of multiple cities to separate transfer airports count is higher than 1. For example: CGK, SUB. Blank means non-stop flight.

**`duration`  **<mark style="color:blue;">**int**</mark>

The flying duration in minutes.

**`codeShare`  **<mark style="color:blue;">**boolean**</mark>

True : code share

False : Not code share

**`cabin`  **<mark style="color:blue;">**string**</mark>

Booking code for the fare. For the LCCs which do not provide cabin options, the cabin string will be blank.

**`cabinClass`  **<mark style="color:blue;">**int**</mark>

Service grade of the fare

1 : Economy

2 : Business

3 : First Class

**`seatCount`  **<mark style="color:blue;">**int**</mark>

Remaining seats for the fare.

**`aircraftCode`  **<mark style="color:blue;">**string**</mark>

This value identifies the aircraft model, which is the IATA aircraft code. For example, Airbus A380 = 388, Airbus A350 = 351.

**`depTerminal`  **<mark style="color:blue;">**string**</mark>

Departure terminal.

**`arrTerminal`  **<mark style="color:blue;">**string**</mark>

Arrival terminal.

**`operatingCarrier`  **<mark style="color:blue;">**string**</mark>

Operating carrier. It is blank when `codeshare=false`

\`\`

**`operatingFlightnumber`  **<mark style="color:blue;">**string**</mark>

Operating flight number. It is blank when `codeshare=false`

**`fareFamily`  **<mark style="color:blue;">**string**</mark>

Fare Family as per the information received from the airline.


          

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

###
