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

    This is received from search response.

    Validity: 6 hrs
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

    * [<mark style="color:blue;">**Booking**</mark>](order.md#paxticketinfo-schema)<mark style="color:blue;">**Requirement**</mark>
      * #### <mark style="color:blue;">passenger</mark>                  Object<[PassengerRequirement](order.md#PassengerElement)>&#x20;
        *   **passengerType        Object<**<mark style="color:blue;">**RequirementSchema**</mark>**>**

            *   **type**                   <mark style="color:blue;">**int**</mark>

            &#x20;    The data type of this element
            * **required**             <mark style="color:blue;">**boolean**</mark>

            &#x20;             Identify if this element is required during booking

            * **decription** <mark style="color:blue;">**string**</mark>

            &#x20;      The remark of this element for this booking
        * **name                         Object<**<mark style="color:blue;">**RequirementSchema**</mark>**>**
        * **gender                      Object<**<mark style="color:blue;">**RequirementSchema**</mark>**>**
        * **birthday                    Object<**<mark style="color:blue;">**RequirementSchema**</mark>**>**
        * **nationality                 Object<**<mark style="color:blue;">**RequirementSchema**</mark>**>**
        * **cardType                   Object<**<mark style="color:blue;">**RequirementSchema**</mark>**>**
        * **cardNum                   Object<**<mark style="color:blue;">**RequirementSchema**</mark>**>**
        * **cardExpired              Object<**<mark style="color:blue;">**RequirementSchema**</mark>**>**
        * **cardIssuePlace         Object<**<mark style="color:blue;">**RequirementSchema**</mark>**>**    



*   **priceChange**                    **Object**<mark style="color:blue;"></mark>

    **IsPriceChange **<mark style="color:blue;">**boolean**</mark>

    true: there is price change
    
    false: there is no price change
    
    **originalAdultPrice  **<mark style="color:blue;">**decimal**</mark>
    
    Original adult fare price returned in search response
    
    **originalAdultTax  **<mark style="color:blue;">**decimal**</mark>
    
    Original adult tax returned in search response
    
    **originalChildPrice  **<mark style="color:blue;">**decimal**</mark>
    
    Original child fare price returned in search response
    
    **originalChildTax  **<mark style="color:blue;">**decimal**</mark>
    
    Original child tax returned in search response
    
    **originalInfantPrice  **<mark style="color:blue;">**decimal**</mark>
    
    Original infant fare price returned in search response
    
    **originalInfantTax  **<mark style="color:blue;">**decimal**</mark>
    
    Original infant tax returned in search response

    **newAdultPrice  **<mark style="color:blue;">**decimal**</mark>
    
    Adult fare with price change (if any) returned in verify response
    
    **newAdultTax  **<mark style="color:blue;">**decimal**</mark>
    
    Adult tax with price change (if any) returned in verify response
    
    **newChildPrice  **<mark style="color:blue;">**decimal**</mark>
    
    Child fare with price change (if any) returned in verify response
    
    **newChildTax  **<mark style="color:blue;">**decimal**</mark>
    
    Child tax with price change (if any) returned in verify response
    
    **newInfantPrice  **<mark style="color:blue;">**decimal**</mark>
    
    Infant fare with price change (if any) returned in verify response
    
    **newInfantTax  **<mark style="color:blue;">**decimal**</mark>
    
    Infant tax with price change (if any) returned in verify response
    
{% hint style="info" %}

* When there is no price change, the "original" and the "new" price and tax will always be the same.
* When there is price change, there will be some difference between the "original" and the "new" price and tax.

{% endhint %}

{% endtab %}

{% tab title="Samples" %}
```
{
    "sessionId": "a72ec919-1aca-4a85-98c1-995c57022ae0",
    "maxSeats": 4,
    "routing": {
        "fid": "y2yLoRAscltEl8AFnPEHBM7XdoRc1WHsnQpcPU1QXUG6ZLJ0vSaswQ..",
        "routingIdentifier": "kAPir1gptfa5xmCdsTZkH3md2e6FFsBnGLICoNRk9jKjtYDn0cD+IDpVpRQq8k7IHlDfvWU6CYW9A95DoiwOWbX2M65Q2y253iFBnmnd6xSXlY16a2N8IXF2rJglXJ0yIEdByMvEOt3zh9clbKPRbYKoIoMpSEo9aqOGcm2h0u0U4/BYNSbM+8aH9Lavob+A/2yy+3VlhITdZYWZJaG7heiSG/R/VPb53iNAqSK3rhctDbT29/qIDtqObED5af8wvkDNE5vxorxFqHf2vguzo4vmvrmyx26agBr9GN8Ooe67Y/uw5b7Cjv4cUsQz5IlOI/JvWnrsBNQAQ+hli/kIsg==",
        "supportCreditTransPayment": "0",
        "supportPaymentMethods": [
            1
        ],
        "currency": "USD",
        "adultPrice": 30.05,
        "adultTax": 0.43,
        "childPrice": 30.05,
        "childTax": 0.43,
        "infantPrice": 0.00,
        "infantTax": 0.00,
        "infantAllowed": false,
        "transactionFeePerPax": 0.00,
        "transactionFee": 0.00,
        "transactionFeeMode": "PER_PAX",
        "nationalityType": 0,
        "nationality": "",
        "suitAge": "",
        "PaxType": "ADT",
        "fromSegments": [
            {
                "segmentIndex": 1,
                "carrier": "W4",
                "flightNumber": "W42849",
                "depAirport": "VIE",
                "depTime": "202309230605",
                "arrAirport": "NCE",
                "arrTime": "202309230755",
                "stopCities": "",
                "duration": 110,
                "codeShare": false,
                "cabin": "",
                "cabinClass": 1,
                "seatCount": 4,
                "aircraftCode": "",
                "depTerminal": "",
                "arrTerminal": "",
                "operatingCarrier": "",
                "operatingFlightnumber": "",
                "fareFamily": "Basic"
            }
        ],
        "retSegments": [],
        "combineIndexs": [],
        "rule": {
            "hasBaggage": 1,
            "baggageElements": [
                {
                    "segmentNo": 1,
                    "baggageType": "CabinBaggageUnderSeat",
                    "passengerType": 0,
                    "baggagePiece": 1,
                    "baggageWeight": -1,
                    "baggageSize": "40*30*20cm"
                },
                {
                    "segmentNo": 1,
                    "baggageType": "StandardCheckInBaggage",
                    "passengerType": 0,
                    "baggagePiece": 0,
                    "baggageWeight": 0,
                    "baggageSize": ""
                }
            ],
            "refundRules": [
                {
                    "refundType": 0,
                    "refundStatus": "T",
                    "refundFee": 0.0,
                    "currency": "EUR",
                    "refNoshow": "T",
                    "refNoShowCondition": 0,
                    "refNoshowFee": 0.0,
                    "ruleDetailList": [
                        {
                            "ruleId": 3036,
                            "status": "H",
                            "startMinute": 525600,
                            "endMinute": 20160,
                            "amount": 65.0,
                            "currency": "EUR"
                        },
                        {
                            "ruleId": 3038,
                            "status": "H",
                            "startMinute": 20160,
                            "endMinute": 180,
                            "amount": 85.0,
                            "currency": "EUR"
                        },
                        {
                            "ruleId": 3041,
                            "status": "T",
                            "startMinute": 180,
                            "endMinute": 0,
                            "amount": 0.0,
                            "currency": "EUR"
                        },
                        {
                            "ruleId": 3044,
                            "status": "T",
                            "startMinute": 0,
                            "endMinute": -525600,
                            "amount": 0.0,
                            "currency": "EUR"
                        }
                    ],
                    "ruleList": null
                }
            ],
            "changesRules": [
                {
                    "changesType": 0,
                    "changesStatus": "T",
                    "changesFee": 0.0,
                    "currency": "EUR",
                    "revNoshow": "T",
                    "revNoShowCondition": 0,
                    "revNoshowFee": 0.0,
                    "ruleList": null,
                    "ruleDetailList": [
                        {
                            "ruleId": 3047,
                            "status": "H",
                            "startMinute": 525600,
                            "endMinute": 43200,
                            "amount": 35.0,
                            "currency": "EUR"
                        },
                        {
                            "ruleId": 3049,
                            "status": "H",
                            "startMinute": 43200,
                            "endMinute": 10080,
                            "amount": 40.0,
                            "currency": "EUR"
                        },
                        {
                            "ruleId": 3051,
                            "status": "H",
                            "startMinute": 10080,
                            "endMinute": 180,
                            "amount": 45.0,
                            "currency": "EUR"
                        },
                        {
                            "ruleId": 3054,
                            "status": "T",
                            "startMinute": 180,
                            "endMinute": 0,
                            "amount": 0.0,
                            "currency": "EUR"
                        },
                        {
                            "ruleId": 3057,
                            "status": "T",
                            "startMinute": 0,
                            "endMinute": -525600,
                            "amount": 0.0,
                            "currency": "EUR"
                        }
                    ]
                }
            ]
        },
        "ancillaryProductElements": [],
        "vendorFare": null,
        "bundleOptions": [],
        "links": [],
        "separateBookings": false,
        "refreshTime": null
    },
    "bookingRequirement": {
        "passenger": {
            "birthday": {
                "type": "string",
                "required": true,
                "description": null,
                "maxLength": null
            },
            "cardIssuePlace": {
                "type": "string",
                "required": false,
                "description": null,
                "maxLength": null
            },
            "cardNum": {
                "type": "string",
                "required": false,
                "description": null,
                "maxLength": null
            },
            "passengerType": {
                "type": "int",
                "required": true,
                "description": null,
                "maxLength": null
            },
            "gender": {
                "type": "string",
                "required": true,
                "description": null,
                "maxLength": null
            },
            "nationality": {
                "type": "string",
                "required": false,
                "description": null,
                "maxLength": null
            },
            "cardExpired": {
                "type": "string",
                "required": false,
                "description": null,
                "maxLength": null
            },
            "name": {
                "type": "string",
                "required": true,
                "description": null,
                "maxLength": null
            },
            "cardType": {
                "type": "string",
                "required": false,
                "description": null,
                "maxLength": null
            }
        }
    },
    "priceChange": {
        "isPriceChange": false,
        "originalAdultPrice": 30.05,
        "originalAdultTax": 0.43,
        "originalChildPrice": 30.05,
        "originalChildTax": 0.43,
        "originalInfantPrice": 38.12,
        "originalInfantTax": 0.00,
        "newAdultPrice": 30.05,
        "newAdultTax": 0.43,
        "newChildPrice": 30.05,
        "newChildTax": 0.43,
        "newInfantPrice": 0.00,
        "newInfantTax": 0.00
    },
    "status": 0,
    "msg": "success"
}
```
{% endtab %}
{% endtabs %}
