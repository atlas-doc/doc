# Verify

### Dependency

The `search` function should be called prior to this call.

### Endpoint

[https://sandbox.atlaslovestravel.com/verify.do](https://sandbox.atlaslovestravel.com/verify.do)

### Request

{% tabs %}
{% tab title="Schema" %}


*   #### cid                                  <mark style="color:blue;">string</mark>                                                                                                 <mark style="color:green;">Required</mark>

    Identifier of client and user.
*   #### routingIdentifier      <mark style="color:blue;">string</mark>                                                                                                 <mark style="color:green;">Required</mark>

    The unique identifier for a particular route.

    It is got from search response.
*   #### requestSource         <mark style="color:blue;">string</mark>                                                                                                 <mark style="color:green;">Required</mark>

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
*   #### status                    <mark style="color:blue;">int</mark>                                                                                                         &#x20;

    0: success

    1: request data format error

    2: route is forbidden

    3: unauthorized access
*   #### msg                         <mark style="color:blue;">string</mark>                                                                                                  &#x20;

    Error message
*   #### sessionId              <mark style="color:blue;">string</mark>                                                                                                  &#x20;

    The unique identifier for this verification.

    It is required when you call order function to make a reservation to identify which flight and fare the client is choosing.
*   #### maxSeats              <mark style="color:blue;">int</mark>                                                                                                        &#x20;

    Remaining seats for the fare;

    Please refer this element and prevent the end-users to choose more passengers than seat count.
*   #### routing                    Object<[RouteElement](broken-reference)> <mark style="color:blue;"></mark>                                                           &#x20;

    Route and fare details. The structure is also Routing Elements, same as search response
{% endtab %}

{% tab title="Samples" %}
```
{
    "status": 0,
    "msg": "success",
    "sessionId": "6e22869e-be61-4f78-b618-6b0319877db9",
    "maxSeats": 4,
    "routing":{
            "routingIdentifier":"K7jWWc8Rq4ETSMWRHlhxhAMDhwUTz1Ty46VwnmDdMe8ZPZQyz3X0KkJxlQV1LwyENuuoYtO28B5k0QK+Vd8Ib4BmiiHQLzX9R7e0VPq8abH5gxFLgeOVQuerBxMqkOi239OWHU/iXVuggQcrbUJ3uxbMNdvNbRECTVvwV3xXgXl07i/72WQoPpN8EA8lik2pKNEtHMsuVpQDk6Wry7MaHQeNspRYJwDEY7i5tKVoTua5c8VEC8fd0g\u003d\u003d",
            "supportCreditTransPayment":"0",
            "currency":"USD",
            "adultPrice":16.46,
            "adultTax":10.98,
            "childPrice":16.46,
            "childTax":10.98,
            "InfantPrice":0,
            "InfantTax":0,
            "transactionFeePerPax":2,
            "nationalityType":0,
            "nationality":"",
            "suitAge":"",
            "PaxType":"ADT",
            "fromSegments":[
                {
                    "carrier":"IW",
                    "flightNumber":"IW1848",
                    "depAirport":"DPS",
                    "depTime":"202202041210",
                    "arrAirport":"LOP",
                    "arrTime":"202202041250",
                    "stopCities":"",
                    "duration":40,
                    "codeShare":false,
                    "cabin":"",
                    "cabinClass":1,
                    "seatCount":4,
                    "aircraftCode":"",
                    "depTerminal":"",
                    "arrTerminal":"",
                    "operatingCarrier":"",
                    "operatingFlightnumber":""
                }
            ],
            "retSegments":[

            ],
            "combineIndexs":[

            ],
            "rule":{
                "hasBaggage":0,
                "baggageElements":[
                    {
                        "segmentNo":1,
                        "passengerType":0,
                        "baggagePiece":0,
                        "baggageWeight":0
                    }
                ],
                "refundRules":[
                    {
                        "refundType":0,
                        "refundStatus":"T",
                        "refundFee":0,
                        "currency":"CNY",
                        "refNoshow":"T",
                        "refNoShowCondition":48,
                        "refNoshowFee":0
                    }
                ],
                "changesRules":[
                    {
                        "changesType":0,
                        "changesStatus":"T",
                        "changesFee":0,
                        "currency":"CNY",
                        "revNoshow":"T",
                        "revNoShowCondition":48,
                        "revNoshowFee":0,
                        "ruleList":[

                        ]
                    }
                ]
            },
            "ancillaryProductElements":[
                {
                    "segmentIndex":1,
                    "productCode":"BAG_IW_1_1P_10KG",
                    "productName":"Baggage",
                    "productType":1,
                    "price":18.61,
                    "currency":"USD",
                    "auxBaggageElement":{
                        "piece":1,
                        "weight":10,
                        "isAllWeight":true
                    }
                },
                {
                    "segmentIndex":1,
                    "productCode":"BAG_IW_1P_15KG",
                    "productName":"Baggage",
                    "productType":1,
                    "price":26.8,
                    "currency":"USD",
                    "auxBaggageElement":{
                        "piece":1,
                        "weight":15,
                        "isAllWeight":true
                    }
                },
                {
                    "segmentIndex":1,
                    "productCode":"BAG_IW_1_1P_20KG",
                    "productName":"Baggage",
                    "productType":1,
                    "price":37.22,
                    "currency":"USD",
                    "auxBaggageElement":{
                        "piece":1,
                        "weight":20,
                        "isAllWeight":true
                    }
                }
            ],
            "vendorFare":null
        }
}
```


{% endtab %}
{% endtabs %}
