---
description: Create an order request to search for flights with multiple farefamilies.
---

# Search

### Dependency

No preceding function needs to be called before `Search`, if you want to return all flights and all farefamilies prices at once.

The search function can be called prior to this call, if you want to first obtain the lowest price for all flights at once, and then specify flights to return the prices for farefamilies.

### Endpoint {% debug uid="search_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/multipleFareFamilySearch.do](https://sandbox.atriptech.com/multipleFareFamilySearch.do)

### Request

{% tabs %}
{% tab title="Schema" %}

**`cid`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

Identifier of client and user.

**`tripType`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

1: Oneway

2: Return Trip

**`adultNum`  **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

Adult passenger count, the number can be 1-9

**`childNum`  **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

Child passenger count, the number can be 0-8

**`infantNum`  **<mark style="color:blue;">**int**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Infant passenger count, no more than the number of adult

**`fromCity`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

IATA Code of departure city or airport

**`toCity`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

IATA Code of arrival city or airport

**`fromDate`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

Departure date, the format is YYYYMMDD

**`retDate`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Return date, the format is YYYYMMDD

Must not be earlier than fromDate. And it can be blank if tripType=1.

**`airlines`  **<mark style="color:blue;">**array**</mark>**  **<mark style="color:orange;">**Optional**</mark>

An array of IATA Codes of airlines. The result will only contain the airlines specified in the search request.

**`fromFlightNumbers`  **<mark style="color:blue;">**array**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Outbound Flight Numbers. The result will only contain the flight numbers specified in the search request. The format of connection flights should be "VJ904,VJ938".

**`retFlightNumbers`  **<mark style="color:blue;">**array**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Inbound Flight Numbers. The result will only contain the flight numbers specified in the search request. The format of connection flights should be "VJ904,VJ938".

**`requestSource`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Identify the source of the search traffic, E.g. Google Flights, Oganic Search, SkyScanner.

{% endtab %}

{% tab title="Samples" %}
```
{
  "cid": "XXXXXXXXX",
  "tripType": 2,
	"adultNum": 1,
	"childNum": 1,
	"infantNum": 1,
	"fromCity": "BKK",
	"toCity": "OSA",
	"fromDate": "20231118",
	"retDate": "20231128",
        "fromFlightNumbers": ["VJ904,VJ938"],
        "retFlightNumbers": ["VZ567"],
	"requestSource": "Organic"
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
**`status`  **<mark style="color:blue;">**int**</mark>

0: success

1: request data format error

2: route is forbidden

3: unauthorized access

**`msg`  **<mark style="color:blue;">**string**</mark>

Error message

The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to check the result.

**`routings` Array <**[**Routing Element**](search.md#route-element-schema)**>**

The array of the routings include suitable flights, farefamiles and fares. Click [<mark style="color:red;">here</mark> ](search.md#route-element-schema)to check the schema. 

{% endtab %}

{% tab title="Samples" %}
```
{
    "routings": [
        {
            "fid": "JvsjEt5YS9EoZBDz1oRpAq37MPKc1_ZIqKe6qgn7t_nFYWgS4KoIhg..",
            "routingIdentifier": "jDz+Q7rv49PE0f68QezYmro9p12LzYHkuStUoglV39DtfjGC/0or8TUEtBTe6naJLCICv3xg6dxpiTd4xcbhJxoieVkynpV0ImUT8swnZ9XjGNQNskH8xNjwjq40hisk+Mr78mRfKfUTKsuYirYZEVOdqmKToDG7bQY8Lfhj0y9d/pautqK5eRoT6GCxM6HFnHotcLzJx/M1BLQU3up2iSwiAr98YOncaYk3eMXG4SeHbID1Be7feUT7ViotVwCxSXNoaWoyHTTygc4yVwfC010ATlXiEkg5cnDmXKvaXuvGgEv747CbzXHDkEtWJAe0WmQj2gFMC+VbZ/9K3azaJU1UxEZyXO1N",
            "supportCreditTransPayment": "1",
            "currency": "USD",
            "adultPrice": 28.71,
            "adultTax": 19.13,
            "childPrice": 28.71,
            "childTax": 19.13,
            "infantPrice": 37.14,
            "infantTax": 0.00,
            "infantAllowed": true,
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
                    "carrier": "U2",
                    "flightNumber": "U2321",
                    "depAirport": "EDI",
                    "depTime": "202311231455",
                    "arrAirport": "BRS",
                    "arrTime": "202311231610",
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
                        "baggageWeight": 15,
                        "baggageSize": "45*36*20cm"
                    },
                    {
                        "segmentNo": 1,
                        "baggageType": "CabinBaggageUnderSeat",
                        "passengerType": 1,
                        "baggagePiece": 1,
                        "baggageWeight": 15,
                        "baggageSize": "45*36*20cm"
                    },
                    {
                        "segmentNo": 1,
                        "baggageType": "CabinBaggageUnderSeat",
                        "passengerType": 2,
                        "baggagePiece": 0,
                        "baggageWeight": 0,
                        "baggageSize": "45*36*20cm"
                    },
                    {
                        "segmentNo": 1,
                        "baggageType": "StandardCheckInBaggage",
                        "passengerType": 0,
                        "baggagePiece": 0,
                        "baggageWeight": 0,
                        "baggageSize": ""
                    },
                    {
                        "segmentNo": 1,
                        "baggageType": "StandardCheckInBaggage",
                        "passengerType": 1,
                        "baggagePiece": 0,
                        "baggageWeight": 0,
                        "baggageSize": ""
                    },
                    {
                        "segmentNo": 1,
                        "baggageType": "StandardCheckInBaggage",
                        "passengerType": 2,
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
                        "currency": "GBP",
                        "refNoshow": "T",
                        "refNoShowCondition": 0,
                        "refNoshowFee": 0.0,
                        "ruleDetailList": [
                            {
                                "ruleId": 1825,
                                "status": "T",
                                "startMinute": 525600,
                                "endMinute": 0,
                                "amount": 0.0,
                                "currency": "GBP"
                            },
                            {
                                "ruleId": 1827,
                                "status": "T",
                                "startMinute": 0,
                                "endMinute": -525600,
                                "amount": 0.0,
                                "currency": "GBP"
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
                        "currency": "GBP",
                        "revNoshow": "T",
                        "revNoShowCondition": 0,
                        "revNoshowFee": 0.0,
                        "ruleList": null,
                        "ruleDetailList": [
                            {
                                "ruleId": 3406,
                                "status": "H",
                                "startMinute": 525600,
                                "endMinute": 86400,
                                "amount": 25.0,
                                "currency": "GBP"
                            },
                            {
                                "ruleId": 3408,
                                "status": "H",
                                "startMinute": 86400,
                                "endMinute": 120,
                                "amount": 49.0,
                                "currency": "GBP"
                            },
                            {
                                "ruleId": 3410,
                                "status": "T",
                                "startMinute": 120,
                                "endMinute": 0,
                                "amount": 0.0,
                                "currency": "GBP"
                            },
                            {
                                "ruleId": 3412,
                                "status": "T",
                                "startMinute": 0,
                                "endMinute": -525600,
                                "amount": 0.0,
                                "currency": "GBP"
                            }
                        ]
                    }
                ],
                "serviceElements": [
                    {
                        "hasFreeSeat": 0,
                        "hasFreeMeal": 0
                    }
                ]
            },
            "ancillaryProductElements": [
                {
                    "segmentIndex": 1,
                    "endSegmentIndex": null,
                    "productCode": "SCI_1PC_15KG",
                    "productName": "StandardCheckInBaggage",
                    "productType": 1,
                    "canPurchaseWithTicket": 1,
                    "canPurchasePostTicket": 1,
                    "price": 27.49,
                    "currency": "USD",
                    "vendorPrice": 24.99,
                    "vendorCurrency": "GBP",
                    "clientTechnicalServiceFee": 0,
                    "clientTechnicalServiceFeeMode": null,
                    "auxBaggageElement": {
                        "piece": 1,
                        "weight": 15,
                        "isAllWeight": false,
                        "size": ""
                    },
                    "offerId": null,
                    "maxQty": 1,
                    "minQty": 1,
                    "categoryCode": "StandardCheckInBaggage",
                    "ancillaryCode": "SCI_1PC_15KG",
                    "auxSeatElement": null
                },
                {
                    "segmentIndex": 1,
                    "endSegmentIndex": null,
                    "productCode": "SCI_1PC_23KG",
                    "productName": "StandardCheckInBaggage",
                    "productType": 1,
                    "canPurchaseWithTicket": 1,
                    "canPurchasePostTicket": 1,
                    "price": 39.59,
                    "currency": "USD",
                    "vendorPrice": 35.99,
                    "vendorCurrency": "GBP",
                    "clientTechnicalServiceFee": 0,
                    "clientTechnicalServiceFeeMode": null,
                    "auxBaggageElement": {
                        "piece": 1,
                        "weight": 23,
                        "isAllWeight": false,
                        "size": ""
                    },
                    "offerId": null,
                    "maxQty": 1,
                    "minQty": 1,
                    "categoryCode": "StandardCheckInBaggage",
                    "ancillaryCode": "SCI_1PC_23KG",
                    "auxSeatElement": null
                },
                {
                    "segmentIndex": 1,
                    "endSegmentIndex": null,
                    "productCode": "SCI_1PC_26KG",
                    "productName": "StandardCheckInBaggage",
                    "productType": 1,
                    "canPurchaseWithTicket": 1,
                    "canPurchasePostTicket": 1,
                    "price": 56.09,
                    "currency": "USD",
                    "vendorPrice": 50.99,
                    "vendorCurrency": "GBP",
                    "clientTechnicalServiceFee": 0,
                    "clientTechnicalServiceFeeMode": null,
                    "auxBaggageElement": {
                        "piece": 1,
                        "weight": 26,
                        "isAllWeight": false,
                        "size": ""
                    },
                    "offerId": null,
                    "maxQty": 1,
                    "minQty": 1,
                    "categoryCode": "StandardCheckInBaggage",
                    "ancillaryCode": "SCI_1PC_26KG",
                    "auxSeatElement": null
                },
                {
                    "segmentIndex": 1,
                    "endSegmentIndex": null,
                    "productCode": "SCI_2PC_30KG",
                    "productName": "StandardCheckInBaggage",
                    "productType": 1,
                    "canPurchaseWithTicket": 1,
                    "canPurchasePostTicket": 1,
                    "price": 54.98,
                    "currency": "USD",
                    "vendorPrice": 49.98,
                    "vendorCurrency": "GBP",
                    "clientTechnicalServiceFee": 0,
                    "clientTechnicalServiceFeeMode": null,
                    "auxBaggageElement": {
                        "piece": 2,
                        "weight": 30,
                        "isAllWeight": true,
                        "size": ""
                    },
                    "offerId": null,
                    "maxQty": 1,
                    "minQty": 1,
                    "categoryCode": "StandardCheckInBaggage",
                    "ancillaryCode": "SCI_2PC_30KG",
                    "auxSeatElement": null
                },
                {
                    "segmentIndex": 1,
                    "endSegmentIndex": null,
                    "productCode": "SCI_2PC_46KG",
                    "productName": "StandardCheckInBaggage",
                    "productType": 1,
                    "canPurchaseWithTicket": 1,
                    "canPurchasePostTicket": 1,
                    "price": 79.18,
                    "currency": "USD",
                    "vendorPrice": 71.98,
                    "vendorCurrency": "GBP",
                    "clientTechnicalServiceFee": 0,
                    "clientTechnicalServiceFeeMode": null,
                    "auxBaggageElement": {
                        "piece": 2,
                        "weight": 46,
                        "isAllWeight": true,
                        "size": ""
                    },
                    "offerId": null,
                    "maxQty": 1,
                    "minQty": 1,
                    "categoryCode": "StandardCheckInBaggage",
                    "ancillaryCode": "SCI_2PC_46KG",
                    "auxSeatElement": null
                },
                {
                    "segmentIndex": 1,
                    "endSegmentIndex": null,
                    "productCode": "SCI_2PC_52KG",
                    "productName": "StandardCheckInBaggage",
                    "productType": 1,
                    "canPurchaseWithTicket": 1,
                    "canPurchasePostTicket": 1,
                    "price": 112.18,
                    "currency": "USD",
                    "vendorPrice": 101.98,
                    "vendorCurrency": "GBP",
                    "clientTechnicalServiceFee": 0,
                    "clientTechnicalServiceFeeMode": null,
                    "auxBaggageElement": {
                        "piece": 2,
                        "weight": 52,
                        "isAllWeight": true,
                        "size": ""
                    },
                    "offerId": null,
                    "maxQty": 1,
                    "minQty": 1,
                    "categoryCode": "StandardCheckInBaggage",
                    "ancillaryCode": "SCI_2PC_52KG",
                    "auxSeatElement": null
                }
            ],
            "vendorFare": {
                "vendorAdultPrice": 26.10,
                "vendorAdultTax": 17.39,
                "vendorChildPrice": 26.10,
                "vendorChildTax": 17.39,
                "vendorInfantPrice": 33.76,
                "vendorInfantTax": 0.00,
                "vendorCurrency": "GBP"
            },
            "bundleOptions": [],
            "links": null,
            "separateBookings": false,
            "refreshTime": "2023-11-10T08:15:34Z"
        },
        {
            "fid": "os-DZRSBTIXIcKG_s6V38gyw1is51Q8_RHfTRexlJM7eQVH0snup0_UYSZPlO2FN",
            "routingIdentifier": "jDz+Q7rv49PE0f68QezYmro9p12LzYHkuStUoglV39CjtYDn0cD+IP1Mw3CZJeeVPttqw3KoP9q0vJT0Ez1EjyczuinN/W9Uq7EaxbT4Zj4/pB/pIorkW0Vi4JCFqVkVzYLDWAmYfrU/ZJBz+DjcqQosTCYE4pKB47mlMM8YlIvwG+fVRIN8hR06qsuvi81rJoIOz3Rh430SzVHCKiGNBTta8tabv1UmGkFVttWsjnfyx77gamdVhjC+QAxLxHWYjWz0GLemfrO+LcraXELrzbEBe2TVx6sM+xeRT05uLJ7yZpCjKPtb8E4DD6+L3xpNruf6apUTGjY4Gk+j5zSNW9+JHhhjzxyG",
            "supportCreditTransPayment": "1",
            "currency": "USD",
            "adultPrice": 110.55,
            "adultTax": 73.69,
            "childPrice": 110.55,
            "childTax": 73.69,
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
                    "carrier": "U2",
                    "flightNumber": "U2321",
                    "depAirport": "EDI",
                    "depTime": "202311231455",
                    "arrAirport": "BRS",
                    "arrTime": "202311231610",
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
                    "fareFamily": "Flexi"
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
                        "baggageWeight": 15,
                        "baggageSize": "45*36*20cm"
                    },
                    {
                        "segmentNo": 1,
                        "baggageType": "CabinBaggageUnderSeat",
                        "passengerType": 1,
                        "baggagePiece": 1,
                        "baggageWeight": 15,
                        "baggageSize": "45*36*20cm"
                    },
                    {
                        "segmentNo": 1,
                        "baggageType": "StandardCheckInBaggage",
                        "passengerType": 0,
                        "baggagePiece": 0,
                        "baggageWeight": 0,
                        "baggageSize": ""
                    },
                    {
                        "segmentNo": 1,
                        "baggageType": "StandardCheckInBaggage",
                        "passengerType": 1,
                        "baggagePiece": 0,
                        "baggageWeight": 0,
                        "baggageSize": ""
                    },
                    {
                        "segmentNo": 1,
                        "baggageType": "CabinBaggageOverheadLocker",
                        "passengerType": 0,
                        "baggagePiece": 1,
                        "baggageWeight": 15,
                        "baggageSize": "56*45*25cm"
                    },
                    {
                        "segmentNo": 1,
                        "baggageType": "CabinBaggageOverheadLocker",
                        "passengerType": 1,
                        "baggagePiece": 1,
                        "baggageWeight": 15,
                        "baggageSize": "56*45*25cm"
                    }
                ],
                "refundRules": [
                    {
                        "refundType": 0,
                        "refundStatus": "T",
                        "refundFee": 0.0,
                        "currency": "GBP",
                        "refNoshow": "T",
                        "refNoShowCondition": 0,
                        "refNoshowFee": 0.0,
                        "ruleDetailList": [
                            {
                                "ruleId": 1824,
                                "status": "T",
                                "startMinute": 525600,
                                "endMinute": 0,
                                "amount": 0.0,
                                "currency": "GBP"
                            },
                            {
                                "ruleId": 1826,
                                "status": "T",
                                "startMinute": 0,
                                "endMinute": -525600,
                                "amount": 0.0,
                                "currency": "GBP"
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
                        "currency": "GBP",
                        "revNoshow": "T",
                        "revNoShowCondition": 0,
                        "revNoshowFee": 0.0,
                        "ruleList": null,
                        "ruleDetailList": [
                            {
                                "ruleId": 3405,
                                "status": "H",
                                "startMinute": 525600,
                                "endMinute": 86400,
                                "amount": 25.0,
                                "currency": "GBP"
                            },
                            {
                                "ruleId": 3407,
                                "status": "H",
                                "startMinute": 86400,
                                "endMinute": 120,
                                "amount": 49.0,
                                "currency": "GBP"
                            },
                            {
                                "ruleId": 3409,
                                "status": "T",
                                "startMinute": 120,
                                "endMinute": 0,
                                "amount": 0.0,
                                "currency": "GBP"
                            },
                            {
                                "ruleId": 3411,
                                "status": "T",
                                "startMinute": 0,
                                "endMinute": -525600,
                                "amount": 0.0,
                                "currency": "GBP"
                            }
                        ]
                    }
                ],
                "serviceElements": [
                    {
                        "hasFreeSeat": 0,
                        "hasFreeMeal": 0
                    }
                ]
            },
            "ancillaryProductElements": [],
            "vendorFare": {
                "vendorAdultPrice": 100.50,
                "vendorAdultTax": 66.99,
                "vendorChildPrice": 100.50,
                "vendorChildTax": 66.99,
                "vendorInfantPrice": 0,
                "vendorInfantTax": 0,
                "vendorCurrency": "GBP"
            },
            "bundleOptions": [],
            "links": null,
            "separateBookings": false,
            "refreshTime": "2023-11-10T08:15:34Z"
        }
    ],
    "status": 0,
    "msg": null
}
```
{% endtab %}
{% endtabs %}


