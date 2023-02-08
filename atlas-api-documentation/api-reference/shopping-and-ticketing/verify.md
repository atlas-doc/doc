# Verify

### Dependency

The `search` function should be called prior to this call.

### Endpoint {% debug uid="verify_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/verify.do](https://sandbox.atriptech.com/verify.do)

### Request

{% tabs %}
{% tab title="Schema" %}
*   **cid **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Identifier of client and user.
*   **routingIdentifier **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    The unique identifier for a particular route.

    It is got from search response.
*   **requestSource **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    The tag to identify which channel does this traffic come from.

    For example: SkyScanner,Google,Oganic search,etc…
{% endtab %}

{% tab title="Samples" %}
```
{
    "cid": "XXXXXXXX",
    "routingIdentifier": "Nvm0BG9VCGJRUPzvRCF2hU1okLJgXsVU46VwnmDdMe/JgpxanH/Xja3hYaj9X/EHLiR7QMsFKwl97AMIwqGNDbcG9kV3bXzylDL2dNM3c07PTcQ67WyTJvK9ITR1HmHC2t2K1gUJztkSI4hVwhMjOGZUlo8qqzhJ8N3Bzta2M87ijqfQHCXkoLAseTdGienIy33IOIIHB6aknLdpZrvz8tCOBxWuNSYc0RRhtNsZ2n31GEmT5TthTQ\u003d\u003d"
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
*   **status **<mark style="color:blue;">**int**</mark>

    0: success

    1: request data format error 

    2: route is forbidden

    3: unauthorized access
*   **msg **<mark style="color:blue;">**string**</mark>

    Error message
    
    The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to         check the result.
*   **sessionId **<mark style="color:blue;">**string**</mark>

    The unique identifier for this verification.

    It is required when you call order function to make a reservation to identify which flight and fare the client is choosing.
*   **maxSeats **<mark style="color:blue;">**int**</mark>

    Remaining seats for the fare;

    Please refer this element and prevent the end-users to choose more passengers than seat count.
*   **routing Object<**[**Routing Element**](search.md#route-element-schema)**>**

    Route and fare details. The structure is also Routing Elements, same as search response
*   **bookingRequirement**                    **Object**<[<mark style="color:blue;">**Booking**</mark>](order.md#paxticketinfo-schema)<mark style="color:blue;">**Requirement**</mark>> <mark style="color:blue;"></mark>                                                           &#x20;

    The description for booking info schema.

    * [<mark style="color:blue;">**Booking**</mark>](search.md#2.-route-element-schema)<mark style="color:blue;">**Requirement**</mark>
      * #### <mark style="color:blue;">passenger</mark>                  Object<[PassengerRequirement](search.md#2.-route-element-schema)>&#x20;
        *   **passengerType        Object<**<mark style="color:blue;">**RequirementSchema**</mark>**>**

            *   **type**                   <mark style="color:blue;">**int**</mark>

            &#x20;    The data type of this element
            * **required**             <mark style="color:blue;">**boolean**</mark>

            &#x20;             Identify if this element is required during booking

            * **decription** <mark style="color:blue;">**string**</mark>

            &#x20;      The remark of this element for this booking
        * **name                         Object<**<mark style="color:blue;">**[RequirementSchema](verify.md#RequirementSchema)**</mark>**>**
        * **gender                      Object<**<mark style="color:blue;">**[RequirementSchema](verify.md#RequirementSchema)**</mark>**>**
        * **birthday                    Object<**<mark style="color:blue;">**[RequirementSchema](verify.md#RequirementSchema)**</mark>**>**
        * **nationality                 Object<**<mark style="color:blue;">**[RequirementSchema](verify.md#RequirementSchema)**</mark>**>**
        * **cardType                   Object<**<mark style="color:blue;">**[RequirementSchema](verify.md#RequirementSchema)**</mark>**>**
        * **cardNum                   Object<**<mark style="color:blue;">**[RequirementSchema](verify.md#RequirementSchema)**</mark>**>**
        * **cardExpired              Object<**<mark style="color:blue;">**[RequirementSchema](verify.md#RequirementSchema)**</mark>**>**
        * **cardIssuePlace         Object<**<mark style="color:blue;">**[RequirementSchema](verify.md#RequirementSchema)**</mark>**>**    


### ReqiurementSchema
*   **type**                   <mark style="color:blue;">**String**</mark>

     &#x20;    The data type of this element
*   **required**             <mark style="color:blue;">**boolean**</mark>

     &#x20;             Identify if this element is required during booking
*   **decription** <mark style="color:blue;">**string**</mark>

     &#x20;      The remark of this element for this booking
{% endtab %}

{% tab title="Samples" %}
```
{
    "sessionId": "70012c8d-0e7e-4ee0-8034-ec3225179305",
    "maxSeats": 4,
    "routing": {
        "fid": "AIDIrbQ3OX7HX-gmIOH6Yv9YVq7VrCuQHz1CA_e5-cKRIzFZ6tuKSMZxixULZg1Ca3fTjvydztOSztK3oRaB1HLLzdB3vMdQYgmy25bzCio.",
        "routingIdentifier": "vh1ju448WDqRwVOmddjsEfPVUteTB0NP7EiDkCP1TsHjpXCeYN0x76HYd/kBZ63cEuwWQD3jEoWNSFcSCD7DjOKnI2zzhv40QAP9Bt94QNr3aOP3oGIcHbD8mCg901Xq34IgnTypoUluQlyTX0UqW4RXI8L3Z0BkPFeJT5Pdk3FVcf/rEPlleMS0sXpZwui9Z2BG0scx/0bHPhBdiYv9iTEWH1xtt7ZEViQN9nNejuPN9l3fphsa5n+GH7ehkAgI0IJ6mDBmBLjot+w8sBs3JkeNcFNfnFY2rAKhr4XZncZEoTyXpxupa2rdh76WCvq2EjxMsKDtQF8u0ZRZPejpwnuO7LodJGHH3T19kRjmiV/ERoOscktwFuj6J7GWuv65+pDS1OBp59SNc/082KQB2OFUSgG/+XBXVsl0DwwUtr1WfWHiwpa9dY6oe3rt5ZiTEVB6eRMyKLuXi/pt4e67KT8A9x/K0dGB",
        "supportCreditTransPayment": "1",
        "currency": "USD",
        "adultPrice": 113.10,
        "adultTax": 0.88,
        "childPrice": 113.10,
        "childTax": 0.88,
        "infantPrice": 71.12,
        "infantTax": 0.00,
        "infantAllowed": true,
        "transactionFeePerPax": 10.00,
        "transactionFee": 5.00,
        "transactionFeeMode": "PER_TICKET",
        "nationalityType": 0,
        "nationality": "",
        "suitAge": "",
        "PaxType": "ADT",
        "fromSegments": [
            {
                "carrier": "U2",
                "flightNumber": "U22441",
                "depAirport": "LTN",
                "depTime": "202302221840",
                "arrAirport": "CDG",
                "arrTime": "202302222055",
                "stopCities": "",
                "duration": 75,
                "codeShare": false,
                "cabin": "",
                "cabinClass": 1,
                "seatCount": 4,
                "aircraftCode": "",
                "depTerminal": "",
                "arrTerminal": "",
                "operatingCarrier": "",
                "operatingFlightnumber": "",
                "fareFamily": "Standard"
            }
        ],
        "retSegments": [
            {
                "carrier": "EC",
                "flightNumber": "EC2436",
                "depAirport": "CDG",
                "depTime": "202302260735",
                "arrAirport": "LTN",
                "arrTime": "202302260755",
                "stopCities": "",
                "duration": 80,
                "codeShare": false,
                "cabin": "",
                "cabinClass": 1,
                "seatCount": 4,
                "aircraftCode": "",
                "depTerminal": "",
                "arrTerminal": "",
                "operatingCarrier": "",
                "operatingFlightnumber": "",
                "fareFamily": "Standard"
            }
        ],
        "combineIndexs": [],
        "rule": {
            "hasBaggage": 0,
            "baggageElements": [
                {
                    "segmentNo": 1,
                    "baggageType": "StandardCheckInBaggage",
                    "passengerType": 0,
                    "baggagePiece": 0,
                    "baggageWeight": 0
                },
                {
                    "segmentNo": 2,
                    "baggageType": "StandardCheckInBaggage",
                    "passengerType": 0,
                    "baggagePiece": 0,
                    "baggageWeight": 0
                }
            ],
            "refundRules": [
                {
                    "refundType": 0,
                    "refundStatus": "T",
                    "refundFee": 0.0,
                    "currency": "CNY",
                    "refNoshow": "T",
                    "refNoShowCondition": 48,
                    "refNoshowFee": 0.0,
                    "ruleList": []
                },
                {
                    "refundType": 0,
                    "refundStatus": "T",
                    "refundFee": 0.0,
                    "currency": "CNY",
                    "refNoshow": "T",
                    "refNoShowCondition": 48,
                    "refNoshowFee": 0.0,
                    "ruleList": []
                }
            ],
            "changesRules": [
                {
                    "changesType": 0,
                    "changesStatus": "T",
                    "changesFee": 0.0,
                    "currency": "CNY",
                    "revNoshow": "T",
                    "revNoShowCondition": 48,
                    "revNoshowFee": 0.0,
                    "ruleList": []
                },
                {
                    "changesType": 0,
                    "changesStatus": "T",
                    "changesFee": 0.0,
                    "currency": "CNY",
                    "revNoshow": "T",
                    "revNoShowCondition": 48,
                    "revNoshowFee": 0.0,
                    "ruleList": []
                }
            ]
        },
        "ancillaryProductElements": [
            {
                "segmentIndex": 1,
                "endSegmentIndex": null,
                "productCode": "SCI_BAG_1PC_15KG",
                "productName": "StandardCheckInBaggage",
                "productType": 1,
                "canPurchaseWithTicket": 1,
                "canPurchasePostTicket": 1,
                "price": 31.89,
                "currency": "USD",
                "vendorPrice": 28.99,
                "vendorCurrency": "GBP",
                "clientTechnicalServiceFee": 0,
                "auxBaggageElement": {
                    "piece": 1,
                    "weight": 15,
                    "isAllWeight": true
                },
                "offerId": null,
                "ancillaryCode": "SCI_BAG_1PC_15KG"
            },
            {
                "segmentIndex": 1,
                "endSegmentIndex": null,
                "productCode": "SCI_BAG_1PC_23KG",
                "productName": "StandardCheckInBaggage",
                "productType": 1,
                "canPurchaseWithTicket": 1,
                "canPurchasePostTicket": 1,
                "price": 37.94,
                "currency": "USD",
                "vendorPrice": 34.49,
                "vendorCurrency": "GBP",
                "clientTechnicalServiceFee": 0,
                "auxBaggageElement": {
                    "piece": 1,
                    "weight": 23,
                    "isAllWeight": true
                },
                "offerId": null,
                "ancillaryCode": "SCI_BAG_1PC_23KG"
            },
            {
                "segmentIndex": 2,
                "endSegmentIndex": null,
                "productCode": "SCI_BAG_1PC_15KG",
                "productName": "StandardCheckInBaggage",
                "productType": 1,
                "canPurchaseWithTicket": 1,
                "canPurchasePostTicket": 1,
                "price": 59.07,
                "currency": "USD",
                "vendorPrice": 53.70,
                "vendorCurrency": "GBP",
                "clientTechnicalServiceFee": 0,
                "auxBaggageElement": {
                    "piece": 1,
                    "weight": 15,
                    "isAllWeight": true
                },
                "offerId": null,
                "ancillaryCode": "SCI_BAG_1PC_15KG"
            },
            {
                "segmentIndex": 2,
                "endSegmentIndex": null,
                "productCode": "SCI_BAG_1PC_23KG",
                "productName": "StandardCheckInBaggage",
                "productType": 1,
                "canPurchaseWithTicket": 1,
                "canPurchasePostTicket": 1,
                "price": 67.83,
                "currency": "USD",
                "vendorPrice": 61.66,
                "vendorCurrency": "GBP",
                "clientTechnicalServiceFee": 0,
                "auxBaggageElement": {
                    "piece": 1,
                    "weight": 23,
                    "isAllWeight": true
                },
                "offerId": null,
                "ancillaryCode": "SCI_BAG_1PC_23KG"
            }
        ],
        "vendorFare": null,
        "bundleOptions": [],
        "links": [],
        "separateBookings": false
    },
    "bookingRequirement": {
        "passenger": {
            "cardIssuePlace": {
                "type": "string",
                "required": false,
                "description": null
            },
            "birthday": {
                "type": "string",
                "required": true,
                "description": null
            },
            "cardNum": {
                "type": "string",
                "required": false,
                "description": null
            },
            "passengerType": {
                "type": "int",
                "required": true,
                "description": null
            },
            "nationality": {
                "type": "string",
                "required": false,
                "description": null
            },
            "gender": {
                "type": "string",
                "required": true,
                "description": null
            },
            "cardExpired": {
                "type": "string",
                "required": false,
                "description": null
            },
            "cardType": {
                "type": "string",
                "required": false,
                "description": null
            },
            "name": {
                "type": "string",
                "required": true,
                "description": null
            }
        }
    },
    "status": 0,
    "msg": "success"
}
```
{% endtab %}
{% endtabs %}
